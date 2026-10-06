---
title: "Week 03: Setting Up My Documentation Website"
date: 2026-10-06
draft: false
---

# Setting Up My Documentation Website

This week, I created my own documentation website for my Digital Fabrication work. I connected the website to GitHub, installed Hugo and the Mana theme, configured GitHub Pages, and connected the project to Obsidian.

## 1. Installing Hugo

I first installed Hugo on my computer using Homebrew:

```bash
brew install hugo
```

I checked whether Hugo was installed correctly:

````
hugo version
````

The terminal showed the installed Hugo version.


## 2. Creating a Hugo website

I created a new Hugo website inside my FabAcademy folder:

````
cd ~/FabAcademy
hugo new site mywebsite
cd mywebsite
````

This created the main folders needed for the website.

## 3. Initializing Git

I turned the Hugo project into a Git repository:

```
git init
```

## 4. Adding the Mana theme

I added the Mana theme as a Git submodule:


````
git submodule add https://github.com/Livour/hugo-mana-theme.git themes/mana
````

I then selected the theme in the Hugo configuration file:

````
theme = "mana"
````

I also added a title and configured the website avatar in `hugo.toml`.

## 5. Testing the website locally

I started the Hugo development server:

````
hugo server -D
````

I opened the local address shown in the terminal:

````
(http://localhost:1313/)
````

## 6. Adding the website image

The Mana theme needed an avatar image, so I downloaded an image into the `static` folder:

````
curl -L https://managuide.blog/images/transparent-logo.png -o static/astronaut.png
````

I connected the image to the website through `hugo.toml`:

````
[params.avatar.home]
  url = "/astronaut.png"
````

## 7. Creating a GitHub repository connection

I initialized the local project as a Git repository and connected it to my GitHub repository:

````
git remote add origin git@github.com:zeynepkocatepe-blip/Digital_Fabrication.git
````

I checked whether the remote connection was correct:

````
git remote -v
````

I downloaded the existing files from GitHub:

````
git fetch origin
````

Because the GitHub repository already contained a README file, I merged it with my local project:

````
git merge origin/main --allow-unrelated-histories --no-edit
````

## 8. Creating a `.gitignore` file

I created a `.gitignore` file so that unnecessary files would not be uploaded:

````
.DS_Store
.hugo_build.lock
/public/
/resources/_gen/
.obsidian/
````

The `.obsidian` folder was excluded because it contains local Obsidian settings.

## 9. Saving the project to GitHub








````
```bash
````