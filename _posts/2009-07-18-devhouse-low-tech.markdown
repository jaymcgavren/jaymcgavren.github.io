---
layout: post
title: DevHouse, low-tech...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1032'
  original_post_id: '1238'
  _wp_old_slug: '1238'
---
Wanted something to run on the projector during Phoenix DevHouse that would give everyone a shared playground.  It had to be simple enough to not interfere with people, though, and I didn't want people to have to download clients or a bunch of other software...

I'd heard about netcat before, but it was only a few days ago that I stumbled across another article on it, including setting it up as a server/listener.  Thought it would be perfect for the job, and it was - as a client.  The listener didn't let people connect concurrently in either TCP or UDP modes, so I simply grabbed a socket example from the Programming Ruby book and fired it up, then posted directions on connecting.  Here's the result...



<!--more-->

<pre>
jay@dandelion:~/Projects
$ echo "Agh, even a ruby UDP listener is blocking the port." | nc localhost 12345
^C punt!
jay@dandelion:~/Projects
$ echo "And though I tried to install MacPorts netcat, it's like there's a conflict with the Apple version." | nc localhost 12345
^C punt!
jay@dandelion:~/Projects
$ nc localhost 12345
Want your text to appear up here? "nc 172.16.1.61 12345"
^C punt!
jay@dandelion:~/Projects
$ nc localhost 12345
But uh, don't forget to ctrl-C to clear the socket.
^C punt!
jay@dandelion:~/Projects
$ ruby udp.rb
add^Cudp.rb:7:in `recvfrom': Interrupt
        from udp.rb:7
        from udp.rb:6:in `loop'
        from udp.rb:6

jay@dandelion:~/Projects
$ ruby udp.rb
adfskh
dfskjh
fdajfads
adsfkj
dfskj
lfkdjsh
tab 1
tab 2
OK, this one doesn't seem to block...
dsafkh
fdksha
#Want your text to appear up here? "nc -u localhost 12121"
adfskj
^Cudp.rb:7:in `recvfrom': Interrupt
        from udp.rb:7
        from udp.rb:6:in `loop'
        from udp.rb:6

jay@dandelion:~/Projects
$ ruby udp.rb
adfshk
afds;kj
nc -u 172.16.1.61 12121
nc -u 172.16.1.61 12121
Want your text to appear up here? "nc -u 172.16.1.61 12121"


Howdy
hi :)
Here's the server code:
require 'socket'
socket = UDPSocket.new
socket.bind("172.16.1.61", 12121)
loop do
  msg, sender = socket.recvfrom(10000)
  host = sender[3]
  print msg
  STDOUT.flush
end
When I bound to '127.0.0.1' I could only connect from localhost, hence the hardcoded IP.
Want your text to appear up here? "nc -u 172.16.1.61 12121"
If you have trouble, ask the nerd with the MacBook.
MCHung in da haus!
Oh, wait, I mean the guy in the GitHub shirt. :)
all weezer, all the time &lt;-- nice


testing
Ok how I do this on a windows machine amrt ass mac users?
like that?
uh, just don&#039;t try
 __________________________

 --------------------------
           ^__^
           (oo)_______
            (__)       )/
                ||----w |
                ||     ||
with lasers attached to it's friggin head!
Want your text to appear up here? "nc -u 172.16.1.61 12121"


                                                     )/_
                                           _.--..---"-,--c_
                                      L..'           ._O__)_
                              ,-.     _.+  _  ..--( /           a:f
                                `.-''__.-'  (     _
                                  `'''       `__   /
                                              ')

     ___          ___          ___          ___
    /  /        /  /        /  /        /  /
   /  /::      /  /::      /  /::      /  /:/
  /  /:/:    /  /:/:    /  /:/:    /  /:/
 /  /:/  :  /  /:/  :  /  /:/  :  /  /:/
/__/:/   :/__/:/ __:/__/:/ __:/__/:/
  :  __/  : /  /:/  : /  /:/  :
   :         :  /:/    :  /:/    :
    :         :/:/      :/:/      :
     :         ::/        ::/        :
    __/        __/        __/        __/
       |
  |
  + 
  \.G_.*=.
   `( '/.|
    .&gt;' (_--.
 _=/d   ,^
~~ )-'   '
   / |
smaller fonts
  '  '   a:f
Want your text to appear up here? "nc -u 172.16.1.61 12121"
 _ _ _  _____  _____  _____  _____   ____
| | | || ___ || ___ |(___  )| ___ | / ___)
| | | || ____|| ____| / __/ | ____|| |
 ___/ |_____)|_____)(_____)|_____)|_|
Better? Or too small?

      ----------.................._____________  _  .-.
                                      _____.. . .   | |
                   _____....------""""             uuuuu
 ____....------""""                                |===|
                                                   |===|
                                                   |===|
                                                   |===|
 _a:f____________________________________________ .[__N]. _______


                                             (
                                            (  )
                      .___.            ,-.  __)      NC + a:f
       |/           //===\        ,-' o `-!|
     .'+^+`.        //=|_|=\    ,-'---------`-.
   .'///|\`.     //=======\    | [+]   [+] |   .-------------.
  //////|\\\   //|||'"`|||\   |    ___    |  
 /((|||^..|||))  |||||.^ |||||   |   |   |  //   `--v----------'
  ((|||(oo)|||)   |||||o) |||||   |   |'  |  |..~~~O
ZZZZ$Z$$$ZZ$$$$$77$777777777777777777777I77II7I?III?IIII???????+++????????++++++=++++++++++++++++++=++======+======+++++
ZZZZZZZZ$$ZZ$77777777777III777777I7777IIIIIIIII??IIIIII???????++++???????++++++++++++?????++++++++++========+===~+=+++++
ZZZZZZ$$$$$$77777$$77I77777777III77IIIIII7IIIII????II????I7$ZZZ$$7I???????++?+++++++++++++++++++++++==+=============++++
$ZZ77$7$$$$$777777777777I7777IIII77I777III?III??????IDNNMNNNNNDDDNNNDDO7????+++++=++=++++++++=++++====+========~~===++++
ZZ$$$7777$$$$$777777777777IIIIIIII7IIIIIIIIII?I??+IZNND8NNNMMMMNNNDDDNND8?+??+?++++++++++++++==+=+===++=======~~~====+++
$$$$$$$$Z$$$$7777777777I7I?II??IIIIII?III???????$DMNN8O8NNNNNNNNMMMMND8DNMD$+++?++==++++++++=======~===========~~======+
$$$$Z$$$$$$$7777I777IIIIII?IIIIIIIII?????+????ZNND8DDZZDDDDDDDNNNNNNMMMMNNNNNZ?++=====+++++++=====~~==~===~==~=~=~======
$$$7$$$7$777III777IIIIIIIIIII??III??III???++?$MNNDDD8$O88DDDNMNNNNNNMMMMMMDNMMN7+=====+++++==========~~~~~~~~~~=~======+
77777777777777IIIII7IIIII????????II?????++++$DN8Z7?+++=++???I$ODNNNMMMMMNNNNNMMM+=+===~==========~==~~~~~~~~~~~~=~======
$$77777777777I77IIIIIIII????II?III?????++++I8N$I?+======++???I$O8DDNNNMMNNNMNMNMZ+=+==~===~~====~==~~~~~~~~~~~~~~~======
$$77777777III77IIIIIIII??????I?I????+++++?I8NOI?=~~~~~~~~~==+?I7$ZDNNNNMMMMNNNMNMO+===~~===~~~~~~~~~~~~~~~~~~::~~=======
$$$$$$77II77IIIIIIIIIII?????????????+++++7NM87+=~:~~:~~~~~~==++I7$8DNNNMNMMMMMNMNMO=~=======~~~~~~~:~~~~~~:::::::~~=====
77777$$7IIII?II??II??????????++++??++===$NMNZI+=~~~~~~~~~~~==+?I7$OO8DNMNNNMNNMMNMM$==+++===~===~~~~~~~~:::::::::~~~====
7II?I7I77III???+????++???????++????+==~+$DMD$I+=======~=====+???I7$ZO8DDNNMMNNMMMMMD???+++++++==~=~~~~=~~~~~:::::~~~==+=
777I777$7II???????++++??????+++???++==+IONM8$I+============+++??II7$ZZODNNNMMMMMMMMM7?I??????+=====~~~~~~~~~~::::~~~===+
$7777$$ZZ7I7I??++?I?++?++???+++++++===7$DNNO7I++===~~=======++++++?I7$Z8NNNNNMNMNMMM8I7IIII7I+=====~+=~~::::~~~::~~~===+
ZZZOOZ8OO$7III?II77I?+++++++++=====+=?78DMMZI?=+===~=~=~==++=+++???II7Z8NMMMMMMMNMNMD7$$$I77I????+++?=~~~~~~~::::::~==++
O8888ZZZ88Z$$$$7777$7?I7?++=+=++====+7$8NMMOI?????+=+===?7$7IIIII77$ZZODNNMMMMMMNNMNN$OZ$7IIII?I??++?+?+=~~:~~:::::===++
O8DD8OOOOOOOZ$$$$$Z$$$Z$7I++++++====?$Z8MMM87?I77$I++++?$ZOZZZZOZ$OOOOO8NNMMMMMMNNNMMOZ$ZZ$$777I??+??+?+=~~:~~~::::~====
DDDD88OOOZZZZOOOZZOOOOZ$ZZ7+?+=++=++IOO8DNMDDDI777$ZI+?ZDDZ7$OOO8DMNO$ZODMMMNNNNMMMNMDOZZZZZ$III?I7$7I??=~~~~~~~:~==++++
888888888OOOO8OZO8OOOZO$7$Z+?+=+++??IZDNNMMOZDIZNDO7I=I8O$I?IOZZZZ???I7O8MMNNMMMMMMMMNOOZZZZZ7$$$77$77I++~:::::~:~====+?
DD8D8O8OOO888OOOZ8D8O88ZZ8+???IZO$???ONNMMMZIIII$Z7?+=7ZZ7??I77$7I++?I7ODMMMMMMMMNNNMMO8OOOZ$7$$$77$777I?=~~~~~~~===+++?
8D88OO88OOO8888OODD888OOO8OZ7$OO$8Z7ZO8NMMN7?+=====+?+I77I?=~~~~~=??I7Z8DMMMMNMMMMMNNMZZZZZ$$777$$$Z$$$7I+==~==~=====++?
8DDDO88888888DDD8DD88DD8O888OZOZ$DO$OO8NMMM$?+====++++?II?+==~~~==?I7$Z8NMMMMNMMMMNNNMZZZZZZ$$Z$$$$ZZZ$7I?==========++??
DD888D8OO8DDD8ODNDD88DDD8D8D8O8OODOO88DNNMM8I+=~==+++=?II?++====++I7$ZODNMMMNMMNMMNNNM77777I??I???????????++++++???????I
NMMNNNNNDDDND8D88DD8DDDDDD8DD8D8D8DNNNNNNMMD7+++==++++II7I?++==++?7$ZO8NNMMMNNNMMMMMNN88OOOOO$$$$$$$7I??I???++??III7$$7I
NMMNDDNNNDDDD88O88888D8DN8DDDDDDNNNMMNNNMMMMZ7++??I?=?777ZI++=+??I$ZOODNNMMMMMMMMMMMMNDD8O8OOOZZZZZZZ$ZZ$7I7777I7I7$$ZZZ
NNNNNDDNNDDDNDNDD888DD88DDDDDDDDDNNNNNMMMMMMD$II?++?$8NMND7++??II7ZO88DNMMMMMMMMMMMMMMNDDD888OOOOOO8OZ$Z$$$ZZZ$$$$$$$$ZZ
MMNMNDDNNNDDNDDDNDD8DD888D88DDDDNNNMNNNMMMMMNZ7II?==?NNN8ZI??III7$$ZO8DNMMMMMMMMMMMMMMN8OOOOOOOOZOOOZOZZZZOZZZZ$$$$$$ZZ$
NNNMMNNDDNDDNDDDNND8DDDDDD88DDDDDNDNMMMMNMMMMO7I77?++I7$$77Z7IIII7ZZO8DNNMMMMMMMMMMMMNND888ZOOOZZZOOOOZZZZ$$77777$$ZZOO8
MNNMNDDDNNNNNDDDDDD8DDNDDDDDDNNDNDDDNMMMNNMMMN7II7I?77$ZOOZ7I??II7ZO8DNNNMMMNNMMMMMMMNNN8OOZOZZZZZZZZZZZZ$$$$$$$$$$ZOOOO
NMMNDNNNNNDDDDDDDNNNNNMNDDDNDNNDD88DNNNNMMMMMMO7I?++IZZZZZ$77II7$$O8DDNNMMMMMMMMMMMMMNND8OOOOZZZOOZZZZZZZZZZZZZOOOZZZZZO
NMMNDNNNNNNDNDDDDNDNNNNNNNNDDDDDD88DNNMMMMMMMMNO$II??$$Z$77$777$ZZ8DDDNNMMMMMMMMMMMMMMDD8ZOO8OZZZ$ZZOOOOZZZZOOOOOOZOOZ$Z
NMMNNNNNNNNNNNNNDNNDDDDDD8D88D8D88O8NDDNMMMMMMMMNO7?+===?I777$ZO88DDDNMMMMMMMMMMMMMMMMND8O$ZZZ$$$$$ZOZOOZZZ$$$Z$$ZZ$ZOZZ
MNNMNNMNNNNNNNNNNNNNNNDDD888888888O8NNNMNNNMMNMMMMNOI++?I77$O88DDDDNNMMMMMMMMMMMMMMMMNNNDOZZZZ$$$$$$ZZZZOZ$$ZZOOO$$ZOZZO
NNMMMNMMMDDNNNNNNNNNDNNDDDDD88O8OOZ$8NNNMMMMMMMMMMMMNZZOO88DDDDDDNMMMNNNMMMNMMMMMMMMNMNNDZOZO8ZOOZZZOOZO8O8OOOOO8OZZZZ$$
MMMNNNMMNNNDNDNNNNNNNDNNDDDDDD88OZZ$OMNMMMMMMMMMMMMMMMMMMMNNNMMMMMNNNNNNNNNMMMMMMMMMMNNNND88O8OOOOOZOOOO8OZO888888OZZZO8
NMNNNMNMMMNDNNNNNNNND88DOO8OOZOOZZZ$ZDNMMMMMMMMMMMMMMMMNNMMMMMMNNNNNNDNDDNNMMMNMMMMMMNMMND88OOZZZZZ$OOO88OO8888O8O888OOO
MMMMMMMNMNNNNDDDDDDD8888D8OZZZZZZOZZO8NMMMMMMMMMMMMMMMN$ZO88DNNNDDD88OOO8DNNMMNMMMMNNNNNN8O8O8OOOO8OOOO8OZZZO88OOZOZZZO8
MMMMMMMMMMNDNNNDD888OOO8OZ8OOOZOZZZZOOONMMNNMMMMMMMMMMMZI7$$OOO888OOZZZZZ8DNMNNNMMMMNNNMMDD8Z$77II7$77$$$$$$$77$7I??7$ZZ
NNMMMMMMMNDDND88D888O8OO8O88OOOOOOOO888NMMMNMMMMMMMMMMMD7II77$ZZZZZZ$$77$Z8NNDNMNNMNDNNMMMN8DD8O8O8OZZ7I77Z$77777$$ZOZ7$
NNNNNNNNNNNND88DNNDDNNNNNOOOOOOOZOZONDDMMMMMMMMMMMMMMMN8$7III777$$777I7I7$Z8NNNNNNNN88MMMMMNMND888DNZOO8DNZ77II777ZZ$7$O
NNNNNNDNDDD88888D8DNNNNNMDD8O8DD8DNDNNMMMMMMMMMMMMMMMDOZ$7II?I7777IIIII?7$$ODNDDDDDN88MNNMMNNND8OO8NODD8DN8O7II77$Z$$7$O
NNNNNNNNDDDDD888D8NDDDO8NMNMNNNMNNMMNNNMMMMMMMMMMMNDO7I?I????????I?++????I7Z8DDNN88N8DMNMNNMNDDNNNND88ZZOOZZ7II?IZ$ZZ7$$
NNNNNNNNNDDDD8DDNNDDDND8NMMMMMMNMNNMMMMMMMMNMMMNNZ$$7???++?+????+++++++++?I$O8NDDZ8D8DNNNNMMNDD8OZZZ7III???III7ZZ$ZOZZZ8
MMNDDNMMNNND8DNDNNNDD8DDNMNDNMMMMNMMMMMMMMMMMM8$7I???=++=++++++++==+==+++I7ZDDDDOZ8D8NNNNNNNNMND8888O7+?I?7$$77$$$$ZOOOO
NMMNNNNMNNNDDDNDDDD8888NMMNDNMMMMMMMMMMMMMMMMMZIII++++++==+=+++++==+++????7Z888DOZ8DDNNNNNNNNMNND88D8$?IIII777$$Z$$$Z$$$
NNNNNNMNNDDDNDDD8O8O8DDNMNNNNMMMMNNNMMMMMMMNNN7I?+++========++========++??I$8OO88O8DNMNNNNMDDNNMNDDDOO$I$7I??II??I777777
NNNMNNNND8DDD8DDO8D8DNDNDDNNDDNMNNNMMMMMMMNNNOI+++++=~~=====+====~=====+?I$$8DO88O8NNMNNNDD88DDDNNNN8OO8Z$77Z7?7O777$O$$
NDNNNDNNND8888O8OO8O8DDDNNDDDNNDNNMMMMMMNDDDO$?+==============~====+++++?I$8O888888MMMNN8ZZZ88DDNMMNND8Z$$IIIIII?IIII???
NNNMNDMMNM8Z8$ZOOO8OODDDDD888DNNMMMMMMMM8OZZO7++======~~~=======~~==++?+?I$ZOO8D88DND888OZOZ7ZZZO8DNMMMND88888Z77777I?I?
NNNNNDMMNMDDN$ZOZZOOZO88DN888DMMMMMMMMMMOZZ$$?=+===========~=====~===+++?I$ZOO8DDD8OOZ$$$7$$$8DDDDNMNNMMMD8O88OZ$$$OO77$
NNNNNNMMNNNDNMN8OZZO88O8D88DNMMMMMMMMMMNZ7II?+==========~======~=~===++??7ZOO888O$7$$$$I?IIII$O8DNMMMMMMMMNDD8ODD88888DO
DDNNDDNDDNNNNNNDNDOOOOOOO88MMMMMMMMMMMN8$III+===~=========~~=~~~==~==++?I$$ZZZZOOOZ7I?7$O888DNNNNNNMMMMMMMMNNDD88DNNDO$I
NNNNDDDNNNDNNNNNN88DDD8OZ$MMMMMMMMMMMMND7?++=======+===~~~~~~~~=~~~~~=+??7$$ZOO$7$ZO8DDNNNMMMMMMMMMMMMMMMMMMMD88DDD8888D
DNNNNNNNDDDDDNDDDDD888OZ$8MMMMMMMMMMMNDD87?++=~~=++++=~~~~~~~:~~~~~~===+?7ZZ$ZZODNNMNNDDNNNNMMMMMMMMMMMMMMMMMNMD8888DND8
DNNNNNNNNND88D8888OZ$ZZZ8NMMMMMMMMMMNNDDDO$I?+===+?++==~~~~~~~~~~~~====?7$ZOO8DDNNNNDDMMMMMMMMMMMMMMMMMMMMMNNNMN888888D8
NNDDND888OOO888OOOOO88DMMMMMMMMMMMMMNDD8DOOOD87I?I?+=~~~~~~=~~~~~===+I$ZOO8DNNMNNNNMMMMMMMMNMMMMMMMMMMMMMMMNMNMNDOOZOZO8
NDND888O8888DO888DDDDMMMMMMMMMMMMMMNND88D8DD8888DDD8O7III?++=+==++I$$Z88ODMMNNNMMMMNNMNDNNNNMMMMMMMMMNMMMMMMMNNMMOOOZZ88
NDDD8D8O8DDDD88888D8MMMMMMMMMMMMMMNDDDDDNNNDD8D8888OOOOOOOOO8OO8OZO8OODMD8NMMMMMMMMNNN8NNNNNMMMMMMMMMMMMMMMMMMMNMDDNDNDD
NNDDDDDD8888OOZOOZZZMMMMMMMMMMMMMNDNDNNDMMD8DD8O8OO8D888888D888888ODMMNDNMNMMMMMMNNNN8NMNNNNMMMMMMMMMMMMMMMMMMMMNNDDDDD8
MMNDDD888888O8OOOZ$$MMMMMMMMMMMMMNDDNNNDMMDDDNDD8OOO88888D8DDD8DD8DNNNNMMMMMMMMMNNNMD8NMDNNNMMNNDNNNMMMMMMMMMMMMNM8O88D8
MMMNNNDDD8888888DDDDMMMMMMMMMMMMMNNNMNDNMNNMNMD8D88DDD88DND8NNNDDNDNMMMMMMMMMMMMNNNNDNNDDNN8OODNDDNDNNMMNMMMMNNNMMNOOO88
MMMNNNNNNDNDDDDDD8DDMMMMMMMMMMMMMNNMMNMMMNMMMNDDDD8DD88NNMNMD8NNDNMMMMMMMMMMMMNNNMNNNMNND88O888NNNNNDNNMMMMMMMNMNNMDOZZZ
MMMMMNNNNNNNNDDDDDDDMMMMMMMMMMMMMMMMMMMMNMMMMMNNNNNMNNNNMMMNNMNNMMMMMMMMMMMMMMMMMMMMMMDNND8O8D8N88DNNMMMMMMMNNNMMMMMNNND
MMMMNNNDDNDNNDDDNNNMMMMMMMMMMMMMMMMMMMMMNMMMMNNNMNNMNNNNMNNNNNMNNMMMMMMMMMMMMMMMMMMMMNNNDDO888O888DNMMMMMMMMNNNNNMNMMMNN
MMMNDD8D8888OOOO8DNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMNMMMMMNNNMNNNMMMMNMMMMMMMMMMMMMMMMNDND888888DNDNMMMNMMMMMMMNNNNNNMMD88
MMD8888OOOO88OO88DNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNNNNMMMMMMMMMMMMMMMMMMMMMMNDDDDD8ODDDNMMMMMMMMMMMMMNNNDNMMMMN88
MD8D888888OOOOOO8NMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNMMMMMMMMMMMMMMMMMMMMMMNNNDNND888DMMMNMMMMMMMMMMMMNNNNNNNNMDO
88DDD88888OOO888MMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMNNMMMMMMMMMMMMMMMMMMMMNMNNNNDDNNDNNNMMNMMMMMMMMMMMMMMNNNNNMNNMN8
DDDDDDDDDD888DDNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMMMMMMMMMMMMMMNNNNDNNNNNMMMMMMMMMMMMMMMMMMMNNNNNNNMMNN
NMMMMMMNNNNNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMMMMNMMMMMMMMMMMMNNNNMMMNNNN
MMMNNMNNNNNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNMMNMMMMMMMMMMMMMMMMMMMMMMMNNNMMMMMMN
NMMMMMNNNNMMMMMMMMMMMMMMMNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNMNNMMMMMMMMMMMMMMMMMMMMMMMMNNNNNNMMMN
NMMMNNMMMMMMMMMMMMMMMMMMMNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMNNNMNNNMMMNNNM
NNMMMMMMMMMMMMMMMMMMMMNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMNMMMMMMMMMMMMMMMNNMMNNMMMNNNN
NMMMMMMMMMMMMMMMMMMMMMMMNNNMMMMMMMMMMMMMMMMMMMMMMMMMMNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMMNMMMMMMNNN
NMMMMMMMMMMMMMMMMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNMMMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMMMNMMNMMMMNN
NMMNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNMMMMMMMMMMMMMMMNNMNN
NMMMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNMMMMMMMMMMMMMMMMMMMNN
NMMMMMMMMMMMMMMNNMMMNDDDNMMMMMMMMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNMMNMNNMNM
MMMMMMMMMMMMMNNND88NMMMMNDDMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNNNNNMMMMNN
NMMMMMMMMMMNNNNNDDMMDDDNNNNNNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNMMMMMMMMMNMMNNNMNNNNNNNNN
MMMMMMMMMMMMMMNNNMNODNND88NODD8DMNMND8OODDNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNNNNNNNMNNN
NMMMMMMMMMMMMMDDNDOOMMND8N8DDODMN8O$III77$Z8DMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNNMNNNNNNMM
NMMMMMMMMMMMMN8NDNNNNDONMNNO8MDZ8IIIIIII77$$$7ZODNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNMNNMNNN
MMMMMMMMMMMMMNMDDMNMODMM8DNMMNOD$777IIII777777$$$$77$DMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNNNMMNNMNN
NMMMMMMMMMMMMNDNMNN8MMMNMNMNMD88$$777777777777777$$77$$8NMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNNNNNMMMNNNNN
NMMMMMMMMMMMMMMMMMDNNMMNMDMNMNNDZ$$$$$$$$7777777777$$$$$ZZZZNMMMMMMNNMMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMMMMMMMNNNMNNNNNNN
NMMMMMMMMMMMMMMMMNNNMMNNNDMMNNM8ZZZZZ$$Z$$777777$$77$$$$77$$Z8NMMMMMNMMMMMMMMMMMMMMMMMMMMMMNMMNMMMMMMMMNMMMMNNNNNNNNMMNN
NNNMMMMMMMMMMMMMMMMMMMNMMMMMNNMND8888OOZZ$$$$$$7777777777777$$ZO88MNMNMMMMMMMMNNNDD8O8NNMMNNNMMMNMMMMMMNNMNNMNNNNNNNNNNN
NMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMDDNDD88ZZZ$$$$$7$$$$77$ZZ$7III$8NDNNMN8ZO8O88NMND888NNND8O88NNMMMMMMMMNMMNNNNNNNNNNNNNN
NNNNMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMNN8ZZZZZ$$$$Z$$$$$ZODD8777$7$D88D8OZZO8DD8O88DND88DNNNNNNNMMMMMMMMMMMNMMNMNNNMMMNNN
NMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMD888OOZZZZZ$$ZZZZ$$ZZ8NNOZ$$$$DDDDDNDOODDDDDDDDDDD8DNNDNNNNNMMMMMMMMMMMMMNNNNNNNMMNN
                                                                                                         GlassGiant.com
CORE DUMP

8888888888 888 88888
88 88 88 88 88 88
8888 88 88 88 88888
88 88 888888888 88 88
88888888 88 88 88 88 888888
88 88 88 888 88888 888888
88 88 88 88 88 88 88 88
88 8888 88 88 88 88888 8888
888 888 888888888 88 88 88
88 88 88 88 88 8888888
dammit i came here to code
Want your text to appear up here? "nc -u 172.16.1.61 12121"

             ______
          ,-'//__\`-.
        ,'  ____      `.
       /   / ,-.-.      
      (/# /__`-'_| || || )
      ||# []/()] O || || |
    __`------------------'__
   |--| ||| |  |
   |  | |   |: _ :|   || |  |
   &gt; _| |___|:===:|   || |__ __ &lt;||:|                            | |
  | |                            |:| /__ |/:|                            | |
 _|_|_                           |: `----&#039;/ :|                           _|_|_
[_____]                          |:  | ,. |  :|                          [_____]
| ::: |                   .------.:  [(  )]  :.------.                   | ::: |
|.===.|                   |      || [| `&#039; |  ||      |                   |.===,|
| ) ( |___________________|::::::|| [|`--&#039;|  ||::::::|___________________| ) ( |
|,===.|__#####________|   |  .. /|| [|  ..|  ||  .. /|   |________#####__|.===.|
||   ||  #####  :.:   |   | ,&#039;&#039;.|| [|:.  |  || ,&#039;&#039;.|   |   :.:  #####  ||   ||
|  / |  #####  :.:   |   | |  | || [|&#039;:. |  || |  | |   |   :.:  #####  |  / |
| [_] |  ######.: :   |   | |  |&lt;|| [| .: |  || |  | .  ,  o&lt;/ 
     |       ___ |  &#039;---&#039;     /    / 
     |_=_________|         __( __ (_  ___
      |_________|         (  _(    _)  __/
                           (___/    U
                                (_/


                       __________________________
               __..--/&quot;.&#039;                        &#039;.
       __..--&quot;&quot;      | |                          |
      /              | |                          |
     /               | |    ___________________   |
    ;                | |   :__________________/:  |
    |                | |   |                 &#039;.|  |
    |                | |   |                  ||  |
    |                | |   |                  ||  |
    |                | |   |                  ||  |
    |                | |   |                  ||  |
    |                | |   |                  ||  |
    |                | |   |                  ||  |
    |                | |   |                  ||  |
    |                | |   |______......-----&quot;|  |
    |                | |   |_______......-----&quot;   |
    |                | |                          |
    |                | |                          |
    |                | |                  ____----|
    |                | |_____.....----|#######|---|
    |                | |______.....----&quot;&quot;&quot;&quot;       |
    |                | |                          |
    |. ..            | |   ,                      |
    |... ....        | |  (c ----- &quot;&quot;&quot;           .&#039;
    |..... ......  ||_|    ____......------&quot;&quot;&quot;|&quot;
    |. .... .......| |&quot;&quot;&quot;&quot;&quot;&quot;                   |
    &#039;... ..... ....| |                         |
      &quot;-._ .....  .| |                         |
          &quot;-._.....| |             ___...---&quot;&quot;&quot;&#039;
              &quot;-._.| | ___...---&quot;&quot;&quot;
                  &quot;&quot;&quot;&quot;&quot;             grp

12345678901234567890123456789012345678901234567890123456789012345678901234567890
                     | |
                     | |
                     | |
                     | |   RUBBER foot on a
                     | |        stick
                 ,-&quot;&quot;; :&quot;&quot;-.
                 |`--...--&#039;J
                 |         J
                 |         J
                 |         J
                 |         |
                 F         |
                 F        J
                 F         7
                J          ;:.
               /   .        ::::...
              J   :             &quot;&quot;::::...
              F   `                    &quot;:::&quot;-..___
              J        ___.....____   Krogg    `&quot;F
    -----------&quot;&quot;----&quot;&quot;            &quot;&quot;&quot;----&quot;&quot;&quot;---&#039;-------
S           .--.                  Try not.
 ::`--._,&#039;.::.`._.--&#039;/::     Do or do not.
 ::::.  ` __::__ &#039;  .::::    There is no try.
 ::::::-:.`&#039;..`&#039;.:-::::::
 :::::::: `--&#039; /::::::::              -Yoda

MMMMMMMMMMMMMMMNNmmhhyssooooooooo+++++oooooooooossssyyhhdmNNMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMNNmmdhyysooooooooooo+++++oooooooosssssssyyyhhdNNNMMMMMMMMMMMMMMM
MMMMMMMMMMMMNmmdhyyyssssssosooooo+++++oooooosssssssssssssyhdmNNMMMMMMMMMMMMMM
MMMMMMMMMMMNmmdhyyyysyssssssoooo+++++++++++++++++oooosssssyhdmmMMMMMMMMMMMMMM
MMMMMMMMMMMNmmhyyyyyssssooo++++++++++++/////////++++oosssssyhdmmMMMMMMMMMMMMM
MMMMMMMMMMNNmdhhyyssssooo++////////////:::////+oossssssyyyhyyhdmNMMMMMMMMMMMM
MMMMMMMMMMNNmdhyyysssyssso++/::::::::::--::://++ooooooooosyyhddmmMMMMMMMMMMMM
MMMMMMMMMNNNmdhhyyyyyssoo+++///::--:-----://++oooo++/////+osyhddmNMMMMMMMMMMM
MMMMMMMMNNNNdhhhyssooossoooo+++/::------:://+++++ooooooosssyhhdmmmNMMMMMMMMMM
NNNNNNNNNNNmmdhsoosoosssssssoo++///::::///+++++oooosooosssooohdmNNNNMMMMMMMMM
NmmddhysdMNmmdhhyssoosssoosssssyssoo++++os++++/+/:/oyys+ohhyosyhdNNNMMMMMMMMM
NNNNNmmmmMNmmdysssyysyso+oooosysyyoo++/+oh+///:::-+oshhsoyhhsoossdmMMMMMMMMMM
NNNNNNNNMMmmmhyhdhsoyhhyo:/+//ssyyyo+//+oho+////+/++++ooooossososhdNMMMMMMMMM
NNNNNNNNNMmmNhyddhsshddhy++oooosyhyo+///+ss+/://///::://++oooooosydmNMMMMMMMM
NNNNNNNNsyNmmhhhhyssso+///+//+osyhyo+///+osoo+////////++++++++oosyhmNMMMMMMMM
hmNNMMNNyyNmdhhhyyso++++////+osshyyo/////+ooo+++////://////+++osssymmMMMMMMMM
NNNmmNNNNNNdhyyssooo+++/////+osyyhyo/:::/+oooo+////////////+++ossyyddMMMMMMMM
MMMMNNmmmNNdhyyssoo++//////++syyyys+/::://+ooo++/:::::::::://++osyyhmMMMMMMMM
MMMMMMMMMMmdhhysoo++///////+osyyyys+/::::/+o+oo+/::::------://++osyhNMMMMMMMM
MMMMMMMMMMmddhyoo+////:::::/oyyssyso/:--::/o++ooo+////:::::::/++osshNMMMMMMMM
MMMMMMMMMMmmdyso++//::::::/oyssooyyo/:..-::+o+++oo++++++//////+++oshmMMMMMMMM
MMNNNMMMMMNmhyso+///::://++yyssssys/:-.`.-:/oo+ooo+//++o++////++osyhdNNNNNMMM
MMMMMMMMMMNmhyso++////++++oyhhyyhhs/:----:+ossssssssso+++++++++oosyhdNNNNNNNN
MMMMMMMMMMMmhyso+++++++ossyyhhhhhddyo+//+ooosyyhhdhhdysssooo+ooossyhdNNNNNNNN
MMMMMMMMMMMmdhysoo+++osyyhdddddhhyyhdhyysossyhddmddhddyyhyyyssoossyhmNNNNNNNN
MMMMMMMMMMMNmdhysooooyhhhddddmdddyyssso+osssyyyyhhhdhhhhhhhhsooossyhmNNNNNNNN
MMMMMMMMMMMMmdhyssyyyhddhhhhhhyyysssso+/++o++ooosssyhhhyyhhhso+osyhdNNNNNNNNN
MMMMMMMMMMMMNddyssyhhhddhhhhhhyyyyyssooo+oossssssyhddhyysyysssooshdmNNNNNNNNN
MMMMMMMMMMMMMmmhysyhhyyyyyyhmmmhssssssooo+//++/+:oyhdysoosyyysoshdmNNNmNNNNNN
MMMNMMNNMMMMMMmdhysyyyssosyyhddho+o/+/:://-:/:/+/oyhysoo+osyysyhdNNNmmNNNNNNN
MMNNMMNNNMMMMMMmdhyyyyyoossyyyhhsoo++/:://:::///syhysooo+ossyyhdmNNNNNNNNNNNN
MNNNMMNNNNMMMMMMNmhhhhyooossyyhhss//+:/::/:/:/ooyyyssooooyyyhddNNNNNNNNNNNmNN
NNNNMNNNNNNNMMMMMNmdddhysosyyyhhhhyssosoossssssssssssoossyhddmNNNNNNNNNNmNNNN
NMMMMNNNNNNNNMMMMMMNmmdhysssyyyyyyyssoo++//++ooooosssoosyhhdmNNNNNNNNmNNNNNNm
MMNMMNNNNMNNNNMMMMMMMNmdhysssyyysssoooo+++++++ooosssoossyhdmNNNNmNNmNNNNNNmmN
MMNMMNNNNMNNNNMNNMMMMMNNmdyssyhyssssssooooossssssssooosyhdmNmmNmNNNNNNNNmmNmN
MNNMMNNNNMNNNNMNNNMMMMMNNdhysyhyhyyyyysssyyyyyyyyysoosyydmmmmNNNNNNNNmmmNNNNN
MNNMMNNNNMNNNNMNNNNMMMMMNNdhyyyyyyyhyysyyhyyhyyysyyssyddmmmmNNNNNNNNmmmNNNNNm
NNMMMNNNNMNNNNMNNNNMMMMMMNmddhyyysyyysyhsyyyyyyhyssyhhdmmmmNNNNNNNNmmmNNNNNNN
O_O
         .&quot;&#039;=-,     ,.,.,_
        (_____ ).&quot;=`      `&quot;=,
       ./_ _  `             `;..
      / (o(o) |=              ; `;
     (_/|     |  |             ;`&quot;`
        |     |  `             ;
         ..  /`,_          _.&#039;
         `---&#039;   `#&quot;#&quot;&quot;&#039;&quot;#&#039;#^
                  # #    # #
                  # #    # #
                  # #    # #
                  # #    # #
                  # #    # #
            jgs  /#|#  /#|#
                 `&quot;`&quot;`  `&quot;`&quot;`

http://www.text-image.com/convert/ascii.html
shp sez moo.
 ______

 ------
           ^__^
           (oo)_______
            (__)       )/
                ||----w |
                ||     ||
    .-.__        .-.  ___
    |_|  '--.-.-(   /;;_ .-._______.-.
    (-)___       .- ;;(           
     Y    '---.__((Q)) ;;\ .-     __(_)
     I           __'-' / .--.((Q))---'    ,
     I     ___.-:    |  |   '-'_          
     A  .-'       .-.        '--.__     '
     |  |____.----((Q))   __|--_           '
        ( )        '-'  _  :  -' '--.___
         Y                           (_)
         I                              ,
         I                                
         A                                 '
         |              snd     __|           '
                               _:.  
                                    
                                     
                                   __|


        __          __
       (,.)   ,.   (,.)   ,.   (,.)   ,.
        ||    ||    ||    ||    ||    ||
        ||    ||    ||    ||    ||    ||
      ,.||..  ||  ,.||..  ||  ,.||..  ||
     //""""\ || //""""\ || //""""\ ||
     ||    || || ||    || || ||    || ||
     ||    || || ||    || || ||    || ||
     ||____|| || ||____|| || ||____|| ||
     `.____.' || `.____.' || `.____.' ||
              ||          ||          ||
              ||          ||          ||
______________||__________||__________||_________
                       .
                       M
                      dM
                      MMr
                     4MMML                  .
                     MMMMM.                xf
     .              "MMMMM               .MM-
      Mh..          +MMMMMM            .MMMM
      .MMM.         .MMMMML.          MMMMMh
       )MMMh.        MMMMMM         MMMMMMM
        3MMMMx.     'MMMMMMf      xnMMMMMM"
        '*MMMMM      MMMMMM.     nMMMMMMP"
          *MMMMMx    "MMMMM    .MMMMMMM=
           *MMMMMh   "MMMMM"   JMMMMMMP
             MMMMMM   3MMMM.  dMMMMMM            .
              MMMMMM  "MMMM  .MMMMM(        .nnMP"
  =..          *MMMMx  MMM"  dMMMM"    .nnMMMMM*
    "MMn...     'MMMMr 'MM   MMM"   .nMMMMMMM*"
     "4MMMMnn..   *MMM  MM  MMP"  .dMMMMMMM""
       ^MMMMMMMMx.  *ML "M .M*  .MMMMMM**"
          *PMMMMMMhn. *x &gt; M  .MMMM**""
             ""**MMMMhx/.h/ .=*"
                      .3P"%....
                    nP"     "*MMnx                DaFreakyG
You put your WEED in there!
now how will you smoke it?
Want your text to appear up here? "nc -u 172.16.1.61 12121"
Want your text to appear up here? "nc -u 172.16.1.61 12121"
Save keystrokes: alias ncu='nc -u 172.16.1.61 12121'
                         /__                       /___    --Unknown




                                     _-~~~~-
                                    -   @  @
"I love you                        '         
 You love me                       |      .. |         |    /|
 We're one big                    ' `. '___/` .`.     | ,,/_/
 happy family                |_  /    `-____--//    __/ /    
 With a nick knack             /    .\     /  _--/     (D)  
 paddy wack                        .'  \     |   -/    (_      
 give the dog                   `.     /'     |   /       _ / ==
 a bone                   __------   |       .'_/         / _ O o)
 this old man            /        _|  /`-__-'/             /   ==/
 went rolling home      /        |                       /
 with a great big      ||         __/                 _/
 hug and a kiss        ||         /              _      /  |
 from me to you        | |      /--______      ___    /  :
 won't you say you     | /   __-  - _/   ------    |  |    
 love me too."          |   -  -   /                | |      )
                        |  |   -  |                 | )     | |
                         | |    | |                 | |    | |
                         | |    &lt; |                 | |   |_/
                         &lt; |    /__                 M  .MMMM**""
             ""**MMMMhx/.h/ .=*"
                      .3P"%....
                    nP"     "*MMnx                DaFreakyG
Want your text to appear up here? "nc -u 172.16.1.61 12121"
I want my text to appear up here
I need my text to appear up here
Plear appear up here
PLEEEEASE
Plear = Please + appear (i'm an idiot)
 |                                                |
 '-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-='
MY ASCII art didn't work :-(





      ___
     //  7
    (_,_/
         
          
      _    __
     (        )
      ______/

kids these days...
Meow
           |`-.._____..-'|
           :  &gt; .  ,   "=._     | )(__/  __)( |     _.="  _.="                            "=._    )  |  _  |  _  =|
     |O      /    /    ee--. [] |  | -| []__    `---'e   |  _  |  -  e|
     |           /   /    |  `  |O |  |_/   `          /      | -    |
     /    //  .-.__   / |     `|  | _ |   /  `-.____.-'     /      ;
    |    ||  /     eee------------_/        /               /      /
   _|_______|______________       || /          /|  | |    /      /
   _|_______|______________       || /          /|  | |    /      /
 /'                     ||``        / / `_             /'      /
|:   ===                -||:  )     `        e-__    __.-e     /'
 .____________________/_||../        `  /   /   eeee |        /'
                                        `-._     |  ||     _.-'
                                            e-..________..-e
Want your text to show up here? Type "rm -rf.... JK
                       ______
                   .-"      "-.
                  /            
                 |              |
                 |,  .-.  .-.  ,|
                 | )(__/  __)( |
                 |/     /     |
       (@_       (_     ^^     _)
  _     ) _________|IIIIII|__/__________________________
 (_)@8@8{}
        )_/                  /
Want your text to appear up here? "nc -u 172.16.1.61 12121"
/______    /______    /______

         ______
          ,-'//__\`-.
        ,'  ____      `.
       /   / ,-.-.      
      (/# /__`-'_| || || )
      ||# []/()] O || || |
    __`------------------'__
   |--| ||| |  |
   |  | |   |: _ :|   || |  |
   &gt; _| |___|:===:|   || |__,(           |
                          _.-|_/,-/   ii  |   |
                           `."' `-/  .-"""||    |
                            /`^"-;   |    ||____|
                           /     /   `.__/  | ||
                                /           | ||
                                            | ||
Want your text to appear up here? "nc -u 172.16.1.61 12121"
bye :)
Gotta bail in a few minutes...
Gonna post all this at http://jay.mcgavren.com
Will try and have something cooler at a future hacknight.
(Collaborative SVG, maybe?)
</pre>
