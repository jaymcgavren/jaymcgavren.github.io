---
layout: post
title: Rubyscript2exe and NSIS...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '818'
  original_post_id: '907'
  _wp_old_slug: '907'
---
I also said I'd present on rubyscript2exe, which is likely to turn into a NSIS tutorial as well.

Here's a quick copy-paste from a build session...

<!--more-->

<pre>
jay@MINIME:C:\work\zyps_0.7.6
$ rake --rakefile rakefile_windows.rb distribute
(in C:/work/zyps_0.7.6)
Tracing zyps ...
Gathering files...
Copying files...
Creating zyps.exe ...
rake aborted!
Cannot find makensis.  Set MAKENSIS environment variable to full path of makensi
s, and run again.
C:/work/zyps_0.7.6/rakefile_windows.rb:58
(See full trace by running task with --trace)
</pre>

Whoops, forgot to install NSIS on this new laptop!  Let me fix that real quick...

<pre>
jay@MINIME:C:\work\zyps_0.7.6
$ rake --rakefile rakefile_windows.rb distribute
(in C:/work/zyps_0.7.6)
Tracing zyps ...
Gathering files...
Copying files...
Creating zyps.exe ...
</pre>

Here are the resulting files:

<pre>
jay@MINIME:C:\work\zyps_0.7.6
$ ls -l build
total 8864
-rw-rw-rw-  1 jay 0    7804 2008-05-10 12:47 COPYING.LESSER.txt
-rw-rw-rw-  1 jay 0   35821 2008-05-10 12:47 COPYING.txt
-rw-rw-rw-  1 jay 0       0 2008-05-10 12:47 nsis.log
-rw-rw-rw-  1 jay 0    1774 2008-05-10 12:47 README.txt
-rwxrwxrwx  1 jay 0 9023922 2008-05-10 12:47 zyps.exe

jay@MINIME:C:\work\zyps_0.7.6
$ ls -l pkg
total 8800
-rwxrwxrwx  1 jay 0 9007490 2008-05-10 12:47 zyps-setup-0.7.6.exe

jay@MINIME:C:\work\zyps_0.7.6
$
</pre>

Here are the relevant snippets from my Windows rakefile:

<pre>
#Get locations of required compilers.
RUBYSCRIPT2EXE = ENV['RUBYSCRIPT2EXE'] || File.join(Config::CONFIG['bindir'], 'rubyscript2exe')
MAKENSIS = ENV['MAKENSIS'] || File.join(ENV['ProgramFiles'], "nsis", "makensis.exe")
...
desc "Compile a Windows executable"
file WINDOWS_EXECUTABLE => [EXECUTABLE] do |target|
  #Ensure rubyscript2exe is installed.
  unless File.exist?(RUBYSCRIPT2EXE)
    raise "Cannot find rubyscript2exe.  Set RUBYSCRIPT2EXE environment variable to full path of rubyscript2exe, and run again."
  end
  #Compile an executable.
  system %{ruby -I lib #{RUBYSCRIPT2EXE} #{target.prerequisites.join(' ')} --rubyscript2exe-rubyw}
  #Move executable to target location, as it is always placed in current directory.
  mv "#{PRODUCT_NAME.downcase}.exe", target.name
end
...
desc "Create a NSIS installer"
file WINDOWS_INSTALLER => [WINDOWS_EXECUTABLE, NSIS_SCRIPT] do |target|
  #Ensure NSIS is installed.
  unless File.exist?(MAKENSIS)
    raise "Cannot find makensis.  Set MAKENSIS environment variable to full path of makensis, and run again."
  end
  #Run the installer creation script.
  system [
    MAKENSIS,
    "/V2", #Surpress info messages.
    "/Obuild/nsis.log", #Log compiler output instead of outputting to STDOUT.
    "/NOCD", #Do not CD to NSI script directory before running.
    "/DPRODUCT_NAME=#{PRODUCT_NAME}", #Define in-NSI-script variables.
    "/DPRODUCT_NAME_DOWNCASE=#{PRODUCT_NAME.downcase}",
    "/DPRODUCT_VERSION=#{PRODUCT_VERSION}",
    "/DPRODUCT_PUBLISHER=#{AUTHOR}",
    "/DPRODUCT_WEB_SITE=#{WEB_SITE}",
    "/XOutFile #{target.name}",
    NSIS_SCRIPT #Script to run.
  ].map{|v| %("#{v}")}.join(' ')
end
</pre>

And these excerpts are from my 'installer.nsi'...

<pre>
Name "${PRODUCT_NAME} ${PRODUCT_VERSION}"
; OutFile "${PRODUCT_NAME_DOWNCASE}-setup.exe" ;Should be specified on command line via /XOutFile <target>
InstallDir "$PROGRAMFILES\${PRODUCT_NAME}"
InstallDirRegKey HKLM "${PRODUCT_DIR_REGKEY}" ""
...
Section "main" SEC01
  ;Add files to installer
  CreateDirectory "$INSTDIR"
  SetOutPath "$INSTDIR"
  File "build\${PRODUCT_NAME_DOWNCASE}.exe"
  File "build\COPYING.txt"
  File "build\COPYING.LESSER.txt"
  File "build\README.txt"
  ;Start Menu group
  CreateDirectory "$SMPROGRAMS\${PRODUCT_NAME}"
  CreateShortCut "$SMPROGRAMS\${PRODUCT_NAME}\${PRODUCT_NAME}.lnk" "$INSTDIR\${PRODUCT_NAME_DOWNCASE}.exe"
  CreateShortCut "$SMPROGRAMS\${PRODUCT_NAME}\Copying.lnk" "$INSTDIR\COPYING.txt"
  CreateShortCut "$SMPROGRAMS\${PRODUCT_NAME}\Copying.Lesser.lnk" "$INSTDIR\COPYING.LESSER.txt"
  CreateShortCut "$SMPROGRAMS\${PRODUCT_NAME}\Readme.lnk" "$INSTDIR\README.txt"
  ;Desktop shortcut
  CreateShortCut "$DESKTOP\${PRODUCT_NAME}.lnk" "$INSTDIR\${PRODUCT_NAME_DOWNCASE}.exe"
  Push $INSTDIR
SectionEnd

Section -AdditionalIcons
  WriteIniStr "$INSTDIR\${PRODUCT_NAME}.url" "InternetShortcut" "URL" "${PRODUCT_WEB_SITE}"
  CreateShortCut "$SMPROGRAMS\${PRODUCT_NAME}\Website.lnk" "$INSTDIR\${PRODUCT_NAME}.url"
  CreateShortCut "$SMPROGRAMS\${PRODUCT_NAME}\Uninstall.lnk" "$INSTDIR\uninst.exe"
SectionEnd

Section -Post
  WriteUninstaller "$INSTDIR\uninst.exe"
  WriteRegStr HKLM "${PRODUCT_DIR_REGKEY}" "" "$INSTDIR\${PRODUCT_NAME_DOWNCASE}.exe"
  WriteRegStr ${PRODUCT_UNINST_ROOT_KEY} "${PRODUCT_UNINST_KEY}" "DisplayName" "$(^Name)"
  WriteRegStr ${PRODUCT_UNINST_ROOT_KEY} "${PRODUCT_UNINST_KEY}" "UninstallString" "$INSTDIR\uninst.exe"
  WriteRegStr ${PRODUCT_UNINST_ROOT_KEY} "${PRODUCT_UNINST_KEY}" "DisplayIcon" "$INSTDIR\${PRODUCT_NAME_DOWNCASE}.exe"
  WriteRegStr ${PRODUCT_UNINST_ROOT_KEY} "${PRODUCT_UNINST_KEY}" "DisplayVersion" "${PRODUCT_VERSION}"
  WriteRegStr ${PRODUCT_UNINST_ROOT_KEY} "${PRODUCT_UNINST_KEY}" "URLInfoAbout" "${PRODUCT_WEB_SITE}"
  WriteRegStr ${PRODUCT_UNINST_ROOT_KEY} "${PRODUCT_UNINST_KEY}" "Publisher" "${PRODUCT_PUBLISHER}"
SectionEnd
...
Section Uninstall
  Push $INSTDIR
  ;Delete installed files
  Delete "$INSTDIR\${PRODUCT_NAME}.url"
  Delete "$INSTDIR\uninst.exe"
  Delete "$INSTDIR\README.txt"
  ...
SectionEnd
</pre>

These files aren't in Subversion (didn't want to pollute the main source), but I'll send a copy if anyone needs them.
