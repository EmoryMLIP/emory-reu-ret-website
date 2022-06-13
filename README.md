# Emory REU/RET Computational Mathematics for Data Science Website

This repository holds the source files for our [REU/RET website](www.math.emory.edu/site/cmds-reuret)

From the files in this repository, the website is generated using [hugo](https://gohugo.io/), and then uploaded to the Math/CS server. This last step can only be performed by Lars.  

## Quick overview

The structure of this repository is close the general guidelines of a hugo website. Except for the three folders below, most of the directories control the template and do not to be changed on a regular basis. 
 
1. [content](https://github.com/EmoryMLIP/emory-reu-ret-website/tree/master/content) contains markup files that have the actual content in them. This folder is broken down into several subfolders corresponding to the different pages on our website.
1. [static/img](https://github.com/EmoryMLIP/emory-reu-ret-website/tree/master/static/media) holds data such as images (please make sure to reduce the file size as much as possible before adding images here)
1. [config](https://github.com/EmoryMLIP/emory-reu-ret-website/tree/master/config) is where parameters for the website are configured. You probably won't have to edit any file in this folder.

When you generate the website locally, you will also see that the folders `public` and `resources` will be generated. Please do not add those folders to the repository.

## How do I edit a page?

Let's assume you want to add more details about your project, fix a typo, update your name, or add a reference and description of your new paper. All these things happen mostly in the [contents](https://github.com/EmoryMLIP/emory-reu-ret-website/tree/master/contents)  folder. You have several options to edit the pages:

1. When you are logged in with your github account, navigate in your browser to the file you want to edit and do the changes online. Most likely you will not have push-access to the repository but you should add a pull-request. Your changes will then be merged and updated on the website when that is re-generated. If you made any change that is urgent, please email lruthotto@emory.edu. 
2. For major changes, it may be best to work locally and do some testing in between. Best way is to fork this repository, clone it to your computer and work on the changes until they are ready. When you are done, push your changes and add a pull-request here. 


## Requirements

You will need to use your Github account to do any changes. Also, to work on the website locally, you will need

1. A git client (SourceTree, Github Desktop, or command line)
1. The hugo software must be [installed](https://gohugo.io/getting-started/installing/). On MacOS, I found it convenient to install it using [Homebrew](https://brew.sh/) to preview the website. If you have found a convenient way to install it on Windows PCs, please share it here. 
1. A text editor. Any will work, but it is useful to have one that supports Markdown such as Jupyter, RStudio, PyCharm, ...

 
## About the Wowchemy Template and Getting Started

Our website uses the research group template by  [**Wowchemy**](https://wowchemy.com).  [Check out the latest demo](https://research-group.netlify.app/) of what you'll get in less than 5 minutes, or [view the showcase](https://wowchemy.com/user-stories/) to get ideas.

- 👉 [**Get Started**](https://wowchemy.com/templates/)
- 📚 [View the **documentation**](https://wowchemy.com/docs/)
- 💬 [Chat with the **Wowchemy community**](https://discord.gg/z8wNYzb) or [**Hugo community**](https://discourse.gohugo.io)
- 🐦 Twitter: [@wowchemy](https://twitter.com/wowchemy) [@GeorgeCushen](https://twitter.com/GeorgeCushen) [#MadeWithWowchemy](https://twitter.com/search?q=(%23MadeWithWowchemy%20OR%20%23MadeWithAcademic)&src=typed_query)
- 💡 [Request a **feature** or report a **bug** for _Wowchemy_](https://github.com/wowchemy/wowchemy-hugo-modules/issues)
- ⬆️ **Updating Wowchemy?** View the [Update Guide](https://wowchemy.com/docs/update/) and [Release Notes](https://wowchemy.com/updates/)


## Acknowledgements 

This site is supported by the US National Science foundation awards DMS-2051019 and DMS-1751636. Any opinions, findings, and conclusions or recommendations expressed on this website are those of the author(s) and do not necessarily reflect the views of the funding agency.