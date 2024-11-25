---
layout: post
title: Step-by-Step Guide to Setting Up VS Code for R and RMarkdown
date: 2024-10-19 00:32:13
description:  A step-by-step guide to configuring Visual Studio Code for R and RMarkdown files.
tags:  R RMarkdown VSCode
categories:  R RMarkdown VSCode Data-Science Bioinformatics
tabs: true
---


# Introduction

Visual Studio Code (VS Code) is a versatile and lightweight editor that can be customized for R programming and RMarkdown files. This guide will walk you through the process of configuring VS Code for an optimal experience when working with R and RMarkdown.

## Step 1: Collect Required Paths

Before you begin, you will need to obtain following paths set up on your system:

- **1. R terminal path** (e.g., `/usr/bin/R`) using the `which R` command in the terminal
- **2. R library path** (e.g., `/usr/lib/R/library`) using the `.libPaths()` command in the `R terminal`
- **3. radian path** (e.g., `/usr/bin/radian`) using the `which radian` command in the terminal (optional)
  - **Note:** Radian is an alternative R console that provides a more user-friendly interface. install with `pip install radian` if you don't have it.


As you should know by now, R needs to be installed on your system. There are several ways to do this, but using Miniconda is the most recommended option for reproducibility and easier environment management. This approach is far better than the outdated RStudio garbage with its antiquated and rigid features that R users often cling to. Perhaps the Posit team's work on the Positron IDE will drag them into the modern era.

Miniconda is particularly useful for managing different versions of R or installing packages with complex dependencies—something that can be a challenge for those sticking with RStudio. If you already have R installed on your system, you can skip the Miniconda installation steps and move on. If you don’t have R installed yet, just follow the steps at the end of this guide to install R using Miniconda or whichever method you prefer. Just make sure you have R installed and obtain the aboce necessary paths.

## Step 2: Install Required Packages in R 

To work with R and RMarkdown and enhance VS Code functionality, install the necessary packages in R using  `R terminal` or  `RStudio`. You can install the following packages by running the following commands in the R terminal:

```r
install.packages("languageserver") # it is required for R LSP
install.packages("rmarkdown") # for working with RMarkdown files
install.packages("httpgd") # for interactive plots
```

**Install Pandoc** : See the official [Pandoc installation guide](https://pandoc.org/installing.html)  installation is quite simple and straightforward.

## Step 3: Set Up VS Code

To work with R in VS Code, you need to install the **vscode-R Extension**.
Search for 'R' in the Extensions Marketplace and install it.
Link: [vscode-R Extension](https://marketplace.visualstudio.com/items?itemName=REditorSupport.r)


Open your VS Code settings (`settings.json`) and add the following configurations to your VS Code settings file:

> **Note:** 

> 1. Change `"r.rpath.linux"` to the R terminal path obtained in Step 1. 
> 2. Change `"r.libPaths"` to the R library path obtained in Step 1.
> 3. Change `"r.rterm.linux"` to the radian path obtained in Step 1 (if using radian).
> 4. Ensure `"files.associations"` is empty to avoid issues with RMarkdown.


```json
{
  "r.bracketedPaste": true,
  "r.removeLeadingComments": true,

  "editor.wordWrap": "wordWrapColumn",
  "[quarto]": {
      "editor.defaultFormatter": "quarto.quarto",
      "editor.wordWrap": "wordWrapColumn",
      "editor.snippetSuggestions": "top"
    },
    "[rmd]": {
      "editor.defaultFormatter": "REditorSupport.r",
      "editor.wordWrap": "wordWrapColumn",
      "editor.snippetSuggestions": "top"
    },
    "[r]": {
      "editor.defaultFormatter": "REditorSupport.r",
      "editor.wordWrap": "wordWrapColumn",
      "editor.snippetSuggestions": "top"
    },
    "[jsonc]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[md]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode",
      "editor.wordWrap": "wordWrapColumn",
      "editor.snippetSuggestions": "top"
    },
    "[html]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode",
      "editor.wordWrap": "wordWrapColumn",
      "editor.snippetSuggestions": "top"
    },
    "[yaml]": {
      "editor.defaultFormatter": "quarto.quarto"
    },
"r.rmarkdown.codeLensCommands": [
"r.runCurrentChunk",
"r.runAboveChunks",
"r.runNextChunk",
"r.runBelowChunks",
"r.runAllChunks"
],

"workbench.editorAssociations": {
"*.RData": "default"
},
"files.associations": {  // make sure remove any rmd association to markdown , otherwise it will cause some issues with RMarkdown. I personally keep this witout any argument. So, it will be like this: "files.associations": {}

},
"r.helpPanel.cacheIndexFiles": "Workspace",
"r.workspaceViewer.showObjectSize": true,
"r.workspaceViewer.removeHiddenItems": true,
"r.rmarkdown.knit.useBackgroundProcess": false,
"r.plot.useHttpgd": true,
"r.helpPanel.previewLocalPackages": [],
"r.lsp.debug": true,
"r.rpath.linux": "/home/mac/miniconda3/envs/my_r/bin/R", // change this to your R path
"markdown.preview.lineHeight": 1.5,
"markdown.extension.completion.enabled": true,
"r.libPaths": [
"/home/mac/miniconda3/envs/my_r/lib/R/library" // change this to your R library path
],
"r.rterm.option": [],
"r.rterm.linux": "/home/mac/miniconda3/envs/my_r/bin/radian" // change this to your radian path
}
```

**Note:** When you start coding in R in VS Code, you can run `.vsc.attach()` in the R console to attach R to VS Code and benefit from the integrated environment and inspect your variables in the R workspace viewer.


## Conclusion

That's it. Happy coding!



## Appendix: Install R using Miniconda 

> **Note:** This guide is written for Linux users. If you are using Windows or macOS, the steps may vary slightly.



#### Install Miniconda

If you don’t already have Conda installed, you can install Miniconda by running the following commands in the terminal:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh
```

#### Create a Conda Environment for R

Create a new Conda environment named `my_r` with R and essential packages:

```bash
conda create -n my_r r-base r-essentials
```

#### Activate the Conda Environment

Activate the newly created Conda environment:

```bash
conda activate my_r
```

This will set up a new environment named `my_r` with R and essential packages. Nice! You are now ready to use R in your Conda environment. Now continue from Step 1 to obtain the required paths for setting up VS Code for R and RMarkdown.
