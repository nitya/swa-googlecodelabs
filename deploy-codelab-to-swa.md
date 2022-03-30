author: Nitya Narasimhan
summary: Create and deploy a Google Codelabs tutorial to Azure Static Web Apps
id: codelab-on-swa-markdown
categories: codelab,markdown,swa,azure
environments: Web
status: Published
feedback link: https://github.com/nitya/swa-googlecodelabs/issues
analytics account:

# Create and deploy a Codelab to Azure Static Web Apps

## CodeLab Overview
Duration: 0:02:00

Are you someone who loves to share what they learn in ways that help others follow along? This codelab will teach you how to author a tutorial in Markdown, and use Azure Static Web Apps for hosting.

Read [this](https://docs.microsoft.com/en-us/azure/static-web-apps/media/overview) for a high-level overview of how Azure Static Web Apps works with your GitHub repo, to automate deployment on every change.

**Resources:**
 * [Google Codelabs Tools](https://github.com/googlecodelabs/tools) - our authoring tool.
 * [Azure Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/) - our hosting service.


## Setup Local Environment
Duration: 0:04:00

This section of the codelab is adapted from this [Create a Codelab tutorial](https://www.marcd.dev/codelab-4-codelab/#0) that is the [default markdown sample](https://github.com/googlecodelabs/tools/blob/main/sample/codelab.md) on Google Codelabs. I followed on a macOS device (tested on Monterey and Big Sur) but you can follow [this](https://github.com/googlecodelabs/tools/tree/main/claat) guidance for other OS.


#### Install Go 

Install [Go](https://golang.org/dl/) if you don't have it.
You can use Homebrew if you have it on mac 
``` bash
$ brew install go
```

Validate the install by checking the version. You should see something like this:
```bash
$ go version
go version go1.18 darwin/amd64
```

#### Setup Go Environment Variables
Below is what I set on mac, but instructions are [here](https://golang.org/doc/install) for other OS options

``` bash
$ export GOPATH=$HOME/Go
$ export GOROOT=/usr/local/opt/go/libexec
$ export PATH=$PATH:$GOPATH/bin
$ export PATH=$PATH:$GOROOT/bin
```

#### Install claat

Install claat using the command below. Note that the older `go get` command is no longer supported outside a module. 

``` bash
$ go install github.com/googlecodelabs/tools/claat@latest
```

You should now have the *claat* command available to you. Use the `-h` option to see documentation. You should see something like this (truncated for clarity)
``` bash
$ claat -h
Usage: claat <cmd> [options] src [src ...]

Available commands are: export, serve, update, version.
..
..
```


## Create your initial CodeLab
Duration: 0:05:00

Since the codelab is in [Markdown]() any text editor or IDE will do. I prefer using [Visual Studio Code](https://code.visualstudio.com/) which comes with built-in Markdown support and will simplify our Azure Static Web Apps setup later.
 * [Setup VS Code](https://code.visualstudio.com/docs) with [command line launch](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line) support.
 * [Learn VS Code basics](https://code.visualstudio.com/docs/getstarted/introvideos) and support for [extensions](https://code.visualstudio.com/docs/editor/extension-marketplace)
 * [Bookmark Azure extensions](https://code.visualstudio.com/docs/azure/extensions) - we'll use that later.

Once setup, simply open a new markdown file as shown. Note the `.md` extension - but customize your filename to something descriptive of your tutorial.

####
``` bash
$ code deploy-codelab-to-swa.md
```

#### Fill-in the header metadata
Copy and paste the headers below into your markdown file and change the values appropriately. 
Guidelines are available below the sample headers. 

``` bash
author: Author Name
summary: Summary of your codelab that is human readable
id: unique-codelab-identifier
categories: codelab,markdown,swa
environments: Web
status: Published
feedback link: A link where users can go to provide feedback (Maybe the git repo)
analytics account: Google Analytics ID
```


Metadata consists of pairs of the form "key: value". 
 * Keys cannot
contain colons, and separate metadata fields must be separated by blank lines. At present, values must all be on one line. 
* All metadata must come before the
title. 
 * Any arbitrary keys and values may be used; however, only the following
will be understood by the renderer:

| | |
|:---|:---|
|Summary | A human-readable summary of the codelab. Defaults to blank.|
| Id| An identifier composed of lowercase letters ideally describing the content of the codelab. This field should be unique among codelabs.|
| Categories | A comma-separated list of the topics the codelab covers.|
| Environments|A list of environments the codelab should be discoverable in. <br> ➡️ Codelabs marked "Web" will be visible at the codelabs index. <br/> ➡️ Codelabs marked "Kiosk" will only be available at codelabs kiosks, which have special equipment attached |
| Status| The publication status of the codelab. Valid values are: `Draft` (not finished), `Published` (finished and visible), `Deprecated` (stale) and `Hidden` (not shown in index).|
|Feedback Link | A link to send users to if they wish to leave feedback on the codelab|
| Analytics Account | A Google Analytics ID to include with all codelab pages|
| | |



#### Add the Title
Next add your title using a single '#' character
```
# Title of codelab
```

#### Add Sections and Durations
Then for each section use Header 2 or '##' and specify an optional duration beneath for time remaining calculations
Optional section times will be used to automatically total and remaining tutorial times
In markdown I've found that the time is formatted hh:mm:ss

Example
``` bash
## Section 1
Duration: 0:10:00

## Section 2
Duration: 0:05:00
```

#### Add Section Content
Now that we have 2 sections to our titled codelab let's go ahead and add some content to each section. 
Make up your own or copy and paste the example below: 

Copy into section 1 (Below Duration and above Section 2):
```
### Info Boxes
Plain Text followed by green and yellow info boxes 

Negative
: This will appear in a yellow info box.

Positive
: This will appear in a green info box.

You created info boxes!

### Bullets
Plain Text followed by bullets
* Hello
* CodeLab
* World

You created bullets!

### Numbered List
1. List
1. Using
1. Numbers

You created a numbered list!

```

Copy into section 2 (Below Duration): 
```
### Add a Link
Adding a link!
[Example of a Link](https://www.google.com)

### Add an Image
Adding an image!
![image_caption](https://googlecloud.tips/img/031/codelabs.png)

### Embed an iframe
![https://codepen.io/tzoght/embed/yRNZaP](https://en.wikipedia.org/wiki/File:Example.jpg "Try Me Publisher")
```

More Markdown Parser examples can be found [here](https://github.com/googlecodelabs/tools/tree/master/claat/parser/md).

## Export and Serve
Duration: 0:02:00

Now that you have an initial codelab defined in your markdown file let's go ahead and generate the static site content. 
We can export and serve the content locally using the `claat` command that we installed earlier. 

``` bash
$ claat export codelab.md
$ claat serve
```

* Your browser should have opened (if it doesn't then try going to localhost:9090 in your browser). 
* Choose the directory that matches your "id" that you put in the headers. 
* Viola! You should have your first codelab!

## Host Your CodeLab
Duration: 0:01:00

When you ran the `claat export` command you created the static web content needed to host your codelab. 
It placed static web content in a directory specified by your unique "id" and you can view it locally by opening the index.html page. 

Negative
: Note that when you view it locally by opening index.html some of the graphics may not show up (such as access_time, Next, Back), but they work once online. 


Now that you have the static content you can host it however you want.
One option is pushing it to github and serving it up from Netlify.  

If you'd like to create your own landing page for codelabs, [like this one](https://codelabs.developers.google.com), there is a tool to do that as well! 
Check it out here: [CodeLabs Site](https://github.com/googlecodelabs/tools/blob/master/site/README.md)