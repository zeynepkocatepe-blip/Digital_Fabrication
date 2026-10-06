---
title: "Week 02: Installing Git and Connecting GitHub"
date: 2026-10-06
draft: false
---

## Learning about Git

I used the Fab Academy version control slides, especially slides 30–35, to learn how Git works. Git is used to track changes, save different versions of files, and synchronize a local project with an online repository.

Source: [Fab Academy Version Control Recitation](https://fabacademy.org/2026/recitation/version-control/?utm_source=chatgpt.com#30)

## Installing Git

I installed Git on my Mac using Homebrew:

```bash
brew install git
```

I checked whether Git was installed correctly:

```bash
git --version
```

## Connecting Git to GitHub

I connected Git on my computer to my GitHub account. This allowed me to upload files from my local computer to my GitHub repository.

I used an SSH connection so that Git could communicate securely with GitHub.

## Creating a local repository

I opened the project folder in Terminal and initialized Git:

```bash
git init
```

This turned my local website folder into a Git repository.

## Connecting the repository

I connected the local repository to my GitHub repository:

```bash
git remote add origin git@github.com:zeynepkocatepe-blip/Digital_Fabrication.git
```

The local project and the GitHub repository were now connected.

## Saving and uploading changes

Git uses three main steps to save changes:

1. Files are changed in the working directory.
2. Selected files are added to the staging area.
3. The staged files are saved as a commit and pushed to GitHub.

The main commands are:

```bash
git status
git add <file>
git commit -m "message"
git push
```

`git status` shows changed files, `git add` prepares files, `git commit` records the changes, and `git push` uploads them to GitHub.

## Result

I installed Git, connected it to my GitHub account, and linked my local Digital Fabrication website project to the GitHub repository. This made it possible to save and upload my documentation files online.