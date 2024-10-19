---
layout: post
title: Step-by-Step Guide to Setting Up VS Code for R and RMarkdown
date: 2024-10-19 00:32:13
description:  A step-by-step guide to configuring Visual Studio Code for R and RMarkdown files.
tags:  R RMarkdown VSCode
categories:  R RMarkdown VSCode Data-Science Bioinformatics
tabs: true
---

{% include figure.liquid loading="eager" path="assets/img/R_programming_in_vscode.png" class="img-fluid rounded z-depth-1" %}


# Introduction

Visual Studio Code (VS Code) is a versatile and lightweight editor that can be customized for R programming and RMarkdown files. This guide will walk you through the process of configuring VS Code for an optimal experience when working with R and RMarkdown.

## Step 1: Collect Required Paths

Before you begin, you will need to obtain following paths set up on your system:

- **1. R terminal path** (e.g., `/usr/bin/R`) using the `which R` command in the terminal
- **2. R library path** (e.g., `/usr/lib/R/library`) using the `.libPaths()` command in the `R terminal`
- **3. radian path** (e.g., `/usr/bin/radian`) using the `which radian` command in the terminal (optional)
  - **Note:** Radian is an alternative R console that provides a more user-friendly interface. install with `pip install radian` if you don't have it.


Therefore we need to have R installed on our system. If you don't have R installed, you can follow the steps at the end of this guide to install R using Miniconda.


## Step 2: Install Required Packages in R 

To work with R and RMarkdown and enhance VS Code functionality, install the necessary packages in R using  `R terminal` or  `RStudio`. You can install the following packages by running the following commands in the R terminal:

```r
install.packages("languageserver") # it is required for R LSP
install.packages("rmarkdown") # for working with RMarkdown files
install.packages("httpgd") # for interactive plots
```

**Pandoc** is automatically installed if you have RStudio on your machine. See the official [Pandoc installation guide](https://pandoc.org/installing.html) if you do not have RStudio. installation is quite simple and straightforward.

## Step 3: Set Up VS Code

To work with R in VS Code, you need to install the **vscode-R Extension**.
Search for 'R' in the Extensions Marketplace and install it.
Link: [vscode-R Extension](https://marketplace.visualstudio.com/items?itemName=REditorSupport.r)


Add the following settings to configure your VS Code environment for optimal use with R and RMarkdown. Open your VS Code settings (`settings.json`) and add the following configurations to your VS Code settings file:

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

**Note:** When you start coding in R in VS Code, you can run `.vsc.attach()` in the R console to attach R to VS Code and benefit from the integrated environment and inspect your variables in the workspace viewer.



## Conclusion

By following these steps, you can set up VS Code for R and RMarkdown, enhancing your coding experience and productivity. With the right configurations and packages, you can leverage the power of VS Code for R programming and data analysis tasks. Happy coding!




-------------------------------------------------------
-------------------------------------------------------
-------------------------------------------------------

## Appendix: Install R using Miniconda (Optional)

> **Note:** This guide is written for Linux users. If you are using Windows or macOS, the steps may vary slightly.

There are several ways to install R, but using **Miniconda** is recommended for reproducibility and easier environment management. This method is particularly useful for maintaining different versions of R or installing packages with complex dependencies. If you already have R installed on your system, you can skip the Miniconda installation steps.

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
