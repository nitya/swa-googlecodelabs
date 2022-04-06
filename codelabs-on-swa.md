author: Nitya Narasimhan
summary: Create and deploy a Google Codelabs tutorial to Azure Static Web Apps
id: codelabs-on-swa
categories: codelab,markdown,swa,azure
environments: Web
status: Published
feedback link: https://github.com/nitya/swa-googlecodelabs/issues
analytics account:

# Deploy Codelabs to Static Web Apps

## CodeLab Overview
Duration: 0:02:00

 [Google Codelabs](https://github.com/googlecodelabs/tools) is a tool for authoring and publishing interactive tutorials online - in three steps:
  * Author tutorials using Markdown (see [guidelines](https://github.com/googlecodelabs/tools/tree/main/claat/parser/md)).
  * Export them to create static content (using [claat](https://github.com/googlecodelabs/tools/tree/main/claat) - "Code Labs As A Tool").
  * Deploy them online - e.g., using [one of many options](https://github.com/googlecodelabs/tools#how-do-i-publish-my-codelabs).

In this tutorial, we'll explore [Azure Static Web Apps (SWA)](https://docs.microsoft.com/en-us/azure/static-web-apps/) as our deployment option. Read [this overview](https://docs.microsoft.com/en-us/azure/static-web-apps/overview) to understand how Static Web Apps differs from traditional monolithic web server deployment approaches.

We'll use Visual Studio Code with [this VS Code Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps) to reduce our Static Web Apps setup to just a few clicks. Once done, this setups a GitHub Actions workflow that automatically rebuilds and redeploys the codelab content with every change to the repository. The figure below gives you a high-level view of what that looks like.

![](static/azure-static-web-apps-overview.png)

**Resources:**
 * [Google Codelabs Tools](https://github.com/googlecodelabs/tools) - our authoring tool.
 * [Azure Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/) - our hosting service.


## Setup Local Environment
Duration: 0:04:00

This section of the codelab was adapted from the [Create a Codelab tutorial](https://www.marcd.dev/codelab-4-codelab/#0) and tested in a macOS development device. You can refer to [this](https://github.com/googlecodelabs/tools/tree/main/claat) guidance for other device platforms. Setup involves three steps:


#### 1. Install Go 

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

#### 2. Setup Go Environment Variables
Below is what I set on mac, but instructions are [here](https://golang.org/doc/install) for other OS options

``` bash
$ export GOPATH=$HOME/Go
$ export GOROOT=/usr/local/opt/go/libexec
$ export PATH=$PATH:$GOPATH/bin
$ export PATH=$PATH:$GOROOT/bin
```

#### 3. Install claat

Use this command (instead of the `go get` option that was previously referenced). Validate your installation by using `claat -h` to view the list of supported options. Once set, you can move on to creating your first codelab!

``` bash
$ go install github.com/googlecodelabs/tools/claat@latest
```

## Create your first CodeLab
Duration: 0:01:00

Since the codelab is in [Markdown]() any text editor or IDE will do. 

I am using [Visual Studio Code](https://code.visualstudio.com/) because it is my preferred editor, but also because it will simplify our Azure Static Web Apps setup later. Here are three things you can do to get ready for this exercise:
 * [Setup VS Code](https://code.visualstudio.com/docs) with [command line launch](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line) support.
 * [Learn VS Code](https://code.visualstudio.com/docs/getstarted/introvideos) basics if you're new to the IDE.
 * [Bookmark Extensions Marketplace](https://code.visualstudio.com/docs/editor/extension-marketplace) - we'll use that later.

Have VS Code setup?

Open a new markdown file as shown below, to author your first tutorial!

``` bash
$ code codelabs-on-swa.md
```

## Fill in header metadata
Duration: 0:03:00

Here is the recommended set of metadata (key-value pairs) you need to define in the front-matter of your markdown file. 

``` bash
author: <Author Name>
summary: <Summary of your codelab that is human readable>
id: <unique-codelab-identifier<>
categories: <codelab,markdown,swa>
environments: <Web>
status: <Published>
feedback link: <A link where users can go to provide feedback (Maybe the git repo)>
analytics account: <Google Analytics ID>
```
Copy the above section into your empty Markdown document:
 * Replace the `< >` contents with relevant values for your tutorial.
 * Ensure metadata appears before the title (first-level header) in document. 
 * Ensure each _value_ is written in a single line.

You can add any key-value pairs you want to - however, only the following are interpreted by the Codelabs renderer meaningfully as described below:

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


## Add Content and Durations
Duration: 0:02:00

#### 1. Add Codelab Title
First, add your title using a single '#' character

```
# Title of codelab
```

#### 2. Add Section Duration

Then for each section use Header 2 or '##' and specify an optional _duration_ (in hh:mm:ss format) immediately beneath it. This information will be used to compute and display remaining time to complete the tutorial when the reader reaches that section.

Example
``` bash
## Section 1
Duration: 0:10:00

## Section 2
Duration: 0:05:00
```

#### 3. Add Section Content

Write the body of your section content using [supported Markdown](https://github.com/googlecodelabs/tools/tree/main/claat/parser/md) formats. You can use these to create lists, add embed images or even iFrames.


For instance, the Markdown snippet below:

```
![https://codepen.io/tzoght/embed/yRNZaP](https://en.wikipedia.org/wiki/File:Example.jpg "Try Me Publisher")
```

will be rendered as the content below:

![https://codepen.io/tzoght/embed/yRNZaP](https://en.wikipedia.org/wiki/File:Example.jpg "Try Me Publisher")

Try to keep each section short and focused on a single task.

## Export and Preview
Duration: 0:02:00

Once your Markdown-driven content is complete, export it to static content files using the following command:

``` bash
$ claat export codelabs-on-swa.md
ok	codelabs-on-swa
```

You can preview the generated codelab webpage using this command in the same directory:

```bash
$ claat serve
```

This should automatically launch a browser - else open one manually to `http://localhost:9090` - and display a list of subfolders. Click on the subfolder corresponding to the "id" value in your codelab header.  _You should be looking at your rendered codelab!_.

## Deploy and Serve
Duration: 0:03:00

### Export to static files

The `claat export` command creates static files that represent the codelab. Let's see what those look like - we should have a `codelabs.json` file providing configuration information, an `img` directory with static image assets (if any) and an `index.html` which has the main website content. 

```bash
$ ls codelabs-on-swa
codelab.json	img		index.html
```

Note that this process sets us up with a default Google Analytics ID. You should be able to modify this to reflect your own tracking needs - make sure you update both the JSON and HTML files accordingly.

### Setup Azure Static Web Apps

Let's setup our code repsitory to use [Azure Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/) for automated deployment.

1. Install the [Static Web Apps Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps) in VS Code.
2. Follow the [steps in the above tutorial](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps) to _Create your first static web app_.
3. Specify `codelabs-on-swa` ("id" in header) for your app_location.
4. Specify `""` for your api_location (nothing integrated yet)
5. Specify `codelabs-on-swa` for your output_location

The last step is key since we're currently setting up GitHub Actions to automate the _deploy_ step, but using manual _claat_ commands to create and commit the _build_ step. As a result the app_location and output_location values are identical. 

Once configured, let the SWA Extension setup complete - you should see a notification in your VS Code window indicating that the site was successfully deployed to Azure Static Web Apps - along with a published URL that you can visit to see the site in action.

### Updating the Tutorial
Simply modify the core Markdown file and run the `claat export` command to rebuild the static files. Commit changes to trigger the GitHub Action which will automatically redeploy the site for you. Later, we can explore setting up the `claat` commands via GitHub Actions to automate the build steps as well.


## Next Steps: Landing Page
Duration: 0:02:00

If you'd like to create your own landing page for codelabs, [like this one](https://codelabs.developers.google.com), there is a tool to do that as well! 
Check it out here: [CodeLabs Site](https://github.com/googlecodelabs/tools/blob/master/site/README.md)