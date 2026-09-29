# Digital_Fabrication
Lesson 1
Name: Zeynep Kocatepe

1. Project Overview
For this project, my goal was to connect my computer to GitHub through Terminal and document my design of a toy rocket on Onshape. The rocket is intended to come apart and be rebuilt like LEGO pieces.

3. Connecting My Computer to GitHub
Checking Git and setting my identity
I opened Terminal and checked whether Git was installed:
git --version

I used the Fab Academy 2026 Version Control tutorial as a reference for setting up Git on my computer. It explains SSH authentication, cloning a repository, and saving and uploading changes.
The tutorial uses GitLab, while my project uses GitHub. The examples below therefore use GitHub addresses and account settings. Git is the version-control software on my computer; GitHub and GitLab are services that host Git repositories. Configuring Git and SSH connects my local workflow to an existing account rather than creating an account through Terminal.
Checking Git and setting my identity
I opened Terminal and checked whether Git was installed:
git --version
I then set the name and email attached to my commits:
git config --global user.name "YOUR_NAME"
git config --global user.email "YOUR_EMAIL"
These settings identify the author of my commits. They do not sign me into GitHub.
Setting up SSH authentication
The commands below document the guide’s SSH approach adapted for GitHub. Replace example values with the ones I actually used.
I checked for existing SSH keys before generating a new one:
ls -al ~/.ssh
If I did not already have a suitable key, I generated one with:
ssh-keygen -t ed25519 -C "YOUR_EMAIL"
I used the default file location, provided it would not overwrite an existing key. I then started the SSH agent and added the key:
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
I copied the public key on my Mac:
pbcopy < ~/.ssh/id_ed25519.pub
On GitHub, I opened Settings > SSH and GPG keys > New SSH key and added the public key. The private key stays on my computer and should never be included in my documentation.
Testing the connection
I tested authentication with:
ssh -T git@github.com
If Terminal asked me to trust the host, I checked the fingerprint against GitHub's official documentation before accepting. A successful response identifies my GitHub username and confirms authentication, while explaining that GitHub does not provide shell access.

Working with my repository
For an existing GitHub repository, I could download a local copy using its SSH URL:
git clone git@github.com:YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
After adding this Markdown file to the repository folder, the following commands would record and upload it:
git status
git add digital_fabrication_documentation.md
git commit -m "Add digital fabrication documentation"
git push
git add stages the file, git commit records a local version, and git push uploads the commit to GitHub.

4. Designing the Modular Rocket in Onshape
Design idea
I designed a toy rocket in Onshape with the goal of making it from separate pieces that could be assembled like LEGO. My model has a long purple body, a light purple lower section, a pointed nose cone with a rounded collar, and fins arranged around the base. I wanted the overall shape to remain recognizable when the pieces were put together.
Building the shapes
My feature history includes sketches, planes, Extrude, and Revolve features. These tools allowed me to work with both straight sections and shapes around a central axis. Extrude creates depth from a sketch, while Revolve rotates a profile around an axis.
The design combines a long body with a pointed tip and a rounded transition below the tip. Keeping these sections aligned along the same central axis gives the rocket a consistent overall shape.
Process note: this is a rough summary based on the visible model and feature list, rather than a confirmed step-by-step reconstruction.
Adding the fins
The rocket has flat fins positioned around its lower section. My feature list includes Extrude 4 followed by Circular pattern 1, which is consistent with creating one fin and repeating it around the body. This approach helps keep repeated fins consistent in shape and spacing.
Working with separate parts
The Part Studio shows nine parts. A horizontal boundary is visible near the upper portion of the purple body, and the lower section and nose are visually distinct. Working with multiple parts supports my goal of creating a rocket that can be taken apart and rebuilt.
However, separate CAD parts still need suitable connections to function as an assembly toy.


