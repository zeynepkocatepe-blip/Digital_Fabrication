---
title: "Assignment 1: Documentation and GitHub Pages Setup"
date: 2026-09-29
draft: false
assignment: "1"
---

This week, I created a documentation website for my Digital Fabrication course. I used GitHub to store my files, Hugo to generate the website, the Mana theme for its design, and Obsidian to write my weekly documentation.

## 1. Installing Homebrew

I first installed Homebrew, which is a package manager for macOS. It allowed me to install Git and Hugo through Terminal.

I used:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After the installation, I navigated to the Homebrew directory:

```bash
cd /opt/homebrew/bin/
```

I then added Homebrew to my Terminal path:

```bash
PATH=$PATH:/opt/homebrew/bin
```

```bash
echo export PATH=$PATH:/opt/homebrew/bin >> ~/.zshrc
```

This made Homebrew commands accessible from Terminal.

## 2. Installing Git

Git is the version control system I used to track changes in my project and send them to GitHub.

I installed Git with:

```bash
brew install git
```

I ran this command more than once because Homebrew was not initially available in my Terminal path. After correcting the path, the installation worked.

## 3. Creating an SSH Key

I needed to connect my computer to a remote Git repository securely. For this, I generated an SSH key:

```bash
ssh-keygen -t ed25519 -C "my-laptop-key-for-gitlab"
```

Although the key label mentions GitLab, the key itself can also be used for GitHub. The label is only a description.

I added the private key to the SSH agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

Then I copied the public key to my clipboard:

```bash
tr -d '\n' < ~/.ssh/id_ed25519.pub | pbcopy
```

I added this public key to my GitHub account.

### Testing the SSH connection

I first tested two incorrect addresses:

```bash
ssh -T git@gitlab.fabcloud.org
```

```bash
ssh -T git@github.fabcloud.org
```

Since I was using GitHub rather than Fab Academy's GitLab system, the correct test was:

```bash
ssh -T git@github.com
```

This confirmed that my computer could authenticate with GitHub.

## 4. Creating the GitHub Repository

I created a GitHub repository named:

```text
Digital_Fabrication
```

The repository address is:

```text
git@github.com:zeynepkocatepe-blip/Digital_Fabrication.git
```

This repository stores the Hugo project, weekly Markdown documentation, images, theme configuration, and GitHub Actions workflow.

## 5. Installing Hugo

I chose Hugo as the static site generator for my documentation website.

I installed it with Homebrew:

```bash
brew install hugo
```

Hugo converts Markdown files into a complete static website.

## 6. Creating the Hugo Project

I created a main folder for my Digital Fabrication work:

```bash
mkdir FabAcademy
```

I entered the folder:

```bash
cd FabAcademy
```

Then I created a new Hugo website called `mywebsite`:

```bash
hugo new site mywebsite
```

I entered the new website folder:

```bash
cd mywebsite
```

This created the basic Hugo folder structure, including folders for content, themes, layouts, static files, and configuration.

## 7. Initializing Git

Inside the website folder, I initialized a Git repository:

```bash
git init
```

This allowed Git to track the files and changes inside the Hugo project.

## 8. Installing the Mana Theme

I selected the Mana theme for my website and added it as a Git submodule:

```bash
git submodule add https://github.com/Livour/hugo-mana-theme.git themes/mana
```

Using a submodule keeps the theme connected to its original GitHub repository.

I opened the Hugo configuration file:

```bash
open -e hugo.toml
```

My configuration included the selected theme, website title, base URL, language, and homepage avatar.

```toml
theme = "mana"
baseURL = "https://zeynepkocatepe-blip.github.io/Digital_Fabrication/"
locale = "en-us"
title = "Zeynep's DigiFab"

[params.avatar.home]
  url = "/astronaut.png"
```

The `baseURL` identifies the final GitHub Pages address of the website.

## 9. Previewing the Website Locally

Before publishing the website, I tested it locally with:

```bash
hugo server
```

I also used:

```bash
hugo server -D
```

The `-D` option allowed Hugo to display draft pages during local testing.

The local server was useful for previewing changes before uploading them to GitHub. However, the final website does not depend on localhost. It is publicly hosted through GitHub Pages.

## 10. Creating a Custom Homepage

I created the layouts folder and a custom homepage file:

```bash
mkdir -p layouts
```

```bash
touch layouts/index.html
```

The custom homepage was stored at:

```text
layouts/index.html
```

This file was used to customize the homepage instead of using only the default homepage provided by the theme.

## 11. Connecting the Local Project to GitHub

I checked the existing remote connection:

```bash
git remote -v
```

I then connected the local Hugo project to my GitHub repository:

```bash
git remote add origin git@github.com:zeynepkocatepe-blip/Digital_Fabrication.git
```

I downloaded information from the remote repository:

```bash
git fetch origin
```

I checked the state of the repository:

```bash
git status
```

I also checked the available branches:

```bash
git branch -a
```

## 12. Creating the `.gitignore` File

Some locally generated files should not be uploaded to GitHub. I added them to `.gitignore` using:

```bash
cat >> .gitignore <<'EOF'
.DS_Store
.hugo_build.lock
/public/
/resources/_gen/
.obsidian/
EOF
```

This prevents generated files, macOS system files, and local Obsidian settings from being unnecessarily added to the repository.

## 13. Committing the Hugo Website

I added the main Hugo files to Git's staging area:

```bash
git add .gitignore .gitmodules archetypes hugo.toml static themes/mana
```

I created a commit:

```bash
git commit -m "Add Hugo site with Mana theme"
```

Since the GitHub repository and local repository had separate histories, I merged them with:

```bash
git merge origin/main --allow-unrelated-histories --no-edit
```

I checked the repository again:

```bash
git status
```

Finally, I pushed the local project to GitHub and connected the local `main` branch to the remote branch:

```bash
git push -u origin main
```

## 14. Setting Up Automatic Publishing

I created a GitHub Actions workflow folder:

```bash
cd ~/FabAcademy/mywebsite
```

```bash
mkdir -p .github/workflows
```

I created the workflow file:

```bash
touch .github/workflows/hugo.yaml
```

I opened it in TextEdit:

```bash
open -e .github/workflows/hugo.yaml
```

The `hugo.yaml` file contains the instructions GitHub Actions uses to build the Hugo website and deploy it to GitHub Pages.

After adding the workflow, I staged the file:

```bash
git add .github/workflows/hugo.yaml
```

I committed it:

```bash
git commit -m "Set up automatic website publishing"
```

I then uploaded it to GitHub:

```bash
git push
```

Every time a new commit is pushed, GitHub Actions now rebuilds and republishes the website automatically.

## 15. Installing and Connecting Obsidian

I installed Obsidian and opened the following existing folder as an Obsidian vault:

```text
/Users/zeynepkocatepe/FabAcademy/mywebsite
```

The vault was named `mywebsite`.

Using the full Hugo project as the vault allows me to edit the website's Markdown content directly from Obsidian.

## 16. Configuring Obsidian Links and Images

In **Settings → Files and links**, I used these settings:

- **Use Wikilinks:** Off
- **New link format:** Path relative to current file
- **Default location for new attachments:** Same folder as current file

I disabled Wikilinks because Hugo works more reliably with standard Markdown links.

Keeping attachments in the same folder as the current file also makes it easier to organize each week's writing and images together.

My weekly content follows this structure:

```text
content/
└── posts/
    ├── week-01/
    │   └── index.md
    ├── week-02/
    │   └── index.md
    ├── week-03/
    │   ├── index.md
    │   └── website-homepage.png
    └── week-04/
        └── index.md
```

Each weekly folder contains an `index.md` file and any images used on that page.

## 17. Installing the Obsidian Git Plugin

I opened **Settings → Community plugins** and installed the Git plugin.

The installed plugin was:

```text
Git v2.41.1 by Vinzent
```

I enabled the plugin and configured its automatic synchronization settings.

Under **Automatic**, I used:

- **Use separate commit and push intervals:** Off
- **Auto commit-and-sync interval:** 5 minutes

Under **Sync**, I enabled:

- **Pull on startup**
- **Push on commit-and-sync**
- **Pull on commit-and-sync**

These settings allow Obsidian to pull new changes, commit my edits, and push them to GitHub.

## 18. Publishing Changes from Obsidian

After writing or editing a documentation page, I can publish it manually without waiting five minutes.

I press:

```text
Command + P
```

Then I search for:

```text
Git: Commit-and-sync
```

When the synchronization succeeds, Obsidian displays messages such as:

```text
Committed 1 file
Pull: Everything is up-to-date
Pushed 1 file to remote
```

After the push, GitHub Actions starts building the website. When the workflow shows a green check mark, the updated page is online.

## 19. Checking the Repository

When I later needed to verify the repository connection, I used:

```bash
cd ~/FabAcademy/mywebsite
```

```bash
pwd
```

```bash
git status
```

```bash
git remote -v
```

```bash
git branch --show-current
```

```bash
git log -5 --oneline
```

```bash
git submodule status
```

```bash
find content -maxdepth 3 -type f | sort
```

These commands confirmed:

- I was working in the correct project folder.
- The active branch was `main`.
- The repository was connected to the correct GitHub address.
- The Mana theme submodule was present.
- The weekly documentation files were inside the correct content folders.

## 20. Fixing the Website Base URL

The initial configuration still contained the example Hugo address. I inspected the file with:

```bash
cat hugo.toml
```

I then changed the example address to my GitHub Pages address:

```bash
sed -i '' 's|https://example.org/|https://zeynepkocatepe-blip.github.io/Digital_Fabrication/|' hugo.toml
```

I checked the result again:

```bash
cat hugo.toml
```

The corrected base URL became:

```text
https://zeynepkocatepe-blip.github.io/Digital_Fabrication/
```

## 21. Fixing the Home Links

The website was hosted inside the `/Digital_Fabrication/` path. However, the original theme links sent visitors directly to the root GitHub address, which resulted in a 404 page.

I first checked the layouts folder:

```bash
find layouts -maxdepth 2 -type f -print
```

The result showed:

```text
layouts/index.html
```

I created a local partials folder and copied the relevant theme files into it:

```bash
mkdir -p layouts/partials && cp themes/mana/layouts/partials/header.html themes/mana/layouts/partials/breadcrumb.html layouts/partials/
```

I replaced the original root links with Hugo's homepage permalink:

```bash
sed -i '' 's#{{ "/" | relLangURL }}#{{ .Site.Home.RelPermalink }}#g' layouts/partials/header.html layouts/partials/breadcrumb.html
```

I verified both changes:

```bash
grep -n "Site.Home.RelPermalink" layouts/partials/*.html
```

This corrected both:

- The purple **Home** link in the breadcrumb
- The **Zeynep's DigiFab** link in the header

After committing and synchronizing these files through Obsidian, GitHub Actions rebuilt the website and the Home links worked correctly.

## Final Result

At the end of this process, I had:

- A GitHub repository for my Digital Fabrication files
- A Hugo website using the Mana theme
- A custom homepage
- Automatic deployment through GitHub Actions
- An Obsidian vault connected to the project
- Automatic Git synchronization every five minutes
- Weekly folders for Markdown documentation and images
- A public website that can be accessed without running localhost

My published website is:

[Zeynep's DigiFab](https://zeynepkocatepe-blip.github.io/Digital_Fabrication/)