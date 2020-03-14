---
layout: post
title: 'Templating Plain Text Files With ERB'
tags: []
type: post
published: true
---

I maintain my talk slides in Markdown these days, converting them to PowerPoint using Pandoc. One of my talks includes exercises, all of which need to follow the [same format](https://github.com/jaymcgavren/presentations/blob/master/go/oreilly/2019/slides.md#exercise-go-syntax).

Each exercise has these repeated elements:

* Short URL to exercise on Go Playground
* Long URL in a comment, in case anything ever happens to the short URL
* Exercise preview
* Cheat sheet (with short URL repeated so I can leave it up on the screen)
* Solution

<!--more-->

``` text
## Exercise: Go syntax

`https://is.gd/goex_syntax`

<!-- https://play.golang.org/p/x9BXw0z5LXT -->

## Exercise: Go syntax

    // Replace the blanks ("____") in the below code so that it
    // compiles, runs, and prints the message "Hello, O'Reilly!".
    ____ main
    
    ____ "fmt"
    
    ____ main() {
    	myString ____ "Hello, O'Reilly!"
    	fmt.Println(____)
    }

## Exercise: Go syntax cheat sheet

* Every Go source file is part of a __package__.
* To use code from other packages, you have to __import__ them.
* The `main` function is called when a program first starts.
* Functions are declared using the `func` keyword.
* A function call needs parentheses following the function name: `mypackage.MyFunction("my argument")`

`https://is.gd/goex_syntax`

## Exercise: Go syntax solution

    package main
    
    import "fmt"
    
    func main() {
    	myString := "Hello, O'Reilly!"
    	fmt.Println(myString)
    }
```

Ensuring consistency of these repeated elements is a pain, even in Markdown.

So I converted my .md file to an .md.erb file, and slapped [a method declaration](https://github.com/jaymcgavren/presentations/blob/master/go/oreilly/2019/slides.md.erb#L2) in a `<% %>` tag at the top:

    <%
    def exercise(title:, short_url:, start_code:, cheat_sheet:, solution:, long_url: nil)
        <<-EOD.chomp # "exercise" will return the value of this "here doc"
    ## Exercise: #{title}
    
    `#{short_url}`
    
    <!-- #{long_url} -->
    
    ## Exercise: #{title}
    
    ``` go
    #{start_code}
    ```
    
    ## Exercise: #{title} cheat sheet
    
    #{cheat_sheet}
    
    `#{short_url}`
    
    ## Exercise: #{title} solution
    
    ``` go
    #{solution}
    ```
        EOD
    end
    %>
    
    <!-- Actual Markdown slide content starts here -->
    
    # Introduction to the Go Programming Language
    
    ## About me
    
    * Author, _Head First Ruby_ and _Head First Go_
    * 4 years experience as online software development instructor

Then I just set some instance variables and call the method whenever I want to output a formatted exercise.

``` text
<%
@title = <<-'EOD'.chomp
Go syntax
EOD

@short_url = "https://is.gd/goex_syntax"

@long_url = "https://play.golang.org/p/x9BXw0z5LXT"

@start_code = <<-'EOD'.chomp
// Replace the blanks ("____") in the below code so that it
// compiles, runs, and prints the message "Hello, O'Reilly!".
____ main

____ "fmt"

____ main() {
	myString ____ "Hello, O'Reilly!"
	fmt.Println(____)
}
EOD

@cheat_sheet = <<-'EOD'.chomp
* Every Go source file is part of a __package__.
* To use code from other packages, you have to __import__ them.
* The `main` function is called when a program first starts.
* Functions are declared using the `func` keyword.
* A function call needs parentheses following the function name: `mypackage.MyFunction("my argument")`
EOD

@solution = <<-'EOD'.chomp
package main

import "fmt"

func main() {
	myString := "Hello, O'Reilly!"
	fmt.Println(myString)
}
EOD
%>
<%= exercise(title: @title, short_url: @short_url, start_code: @start_code, cheat_sheet: @cheat_sheet, solution: @solution, long_url: nil) %>
```

If I want to update the exercise format at some point, spreading it out over more slides or adding new elements, I just change the method at the top.

As with any .erb file, you can use the "erb" command-line tool (which is installed along with Ruby) to render it:

``` text
$ erb slides.md.erb > slides.md
```

Or in my case, I just pipe it direct to Pandoc:

``` text
$ erb slides.md.erb | pandoc -o slides.pptx
```

Easy-peasy!

So if you have plain-text files with repeated elements, try slapping an .erb extension on them and throwing some ERB elements in there. You might save yourself a lot of time!

P.S.: I'm not updating this blog much these days, preferring to condense my thoughts into a tweet where I can. But the Twitter platform is failing me more and more as they warp it to favor cat GIFs over technical discussion. Hence this post. You can view the laughable tweet version [here](https://twitter.com/jaymcgavren/status/1238662288015425537).
