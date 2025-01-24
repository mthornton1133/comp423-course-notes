# Setting up a Dev Container for Rust

* Primary author: [Matthew Thornton](https://github.com/mthornton1133)
* Reviewer: [Anish Parepalli](https://github.com/apcodes)

## Prerequisites

Welcome! This tutorial will teach you how to create a Dev Container for the Rust programming language as well as how to begin a basic project in Rust.
Before starting there are some required prerequisites that you must have:

1. A GitHub Account - Sign up at [GitHub](https://github.com/)
2. Git Installed - [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. Visual Studio Code - Download [Here](https://code.visualstudio.com/)
4. Docker Installed - Download [Here](https://www.docker.com/products/docker-desktop)
5. Knowledge of some Command Line Basics - Review your COMP 211 Notes if Necessary!


## Part 1: Project Setup: Creating a Repo
### Step 1: Create a Local Directory and Initialize Git

1. Open you terminal/command prompt.
2. Create a New Directory for your project, you can name this whatever you like:
```
mkdir rust-project
cd rust-project
```
3. Initialize a git repo:

```
git init
```

!!! note "What does git init do?"
    git init initializes a folder as an empty git repository. This basically adds a "hidden" .git folder that houses everything a git repo needs.

4. Create a README.md File:
```
echo "# Rust Starter Project" > README.md
echo "# Tutorial Link [Here](https://mthornton1133.github.io/comp423-course-notes/tutorials/rust-setup/)" >> README.md
git add README.md
git commit -m "Initialized with a README"
```
!!! note
    The first echo makes the README with the title Rust Starter Project and the second provides a link back to this tutorial. The second part stages and commits your changes.
### Step 2: Create a Remote GitHub Repo:
1. Log into your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
2. Fill in the following details:
    * **Repository Name**: rust-project
    * **Description**: “A starter project for learning the Rust programming language”
    * **Visibility**: Public
3. **Do not** initialize the project with a README, .gitignore, or license.
4. Click Create Repository.

### Step 3: Link your Local Repo to GitHub:
1. Add GitHub repo as remote, replace your-username with your actual GitHub username:
```
git remote add origin https://github.com/<your-username>/rust-project.git
```
2. Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: `git branch -M main`. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.
3. Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```
4.  Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Part 2: Setting Up Your Dev Container:

!!! note "What is a Dev Container?"
    A Dev Container ensures that your development process is consistent across different machines. This becomes super important when working in teams. Creating Dev Containers is a way to fix the “It Doesn’t Work on my Machine” problem. It also simplifies onboarding new people to a project. Docker comes into play by specifying a specific image to set up the development environment. The steps below essentially automate the process of setting up a Dev Container.

### Step 1: Add Dev Container Configurations:
1. In Visual Studio Code, open the `rust-project` directory. Do this by clicking File > Open Folder.
2. Install the **Dev Containers** extension for VS Code. This is located on the left column.
3. Create a `.devcontainer` directory in the root of your project with the following file inside this “hidden” directory: `.devcontainer/devcontainer.json`
4. Place the following code inside this newly created file: 
```
{
 "name": "Rust Project”,
 "image": "mcr.microsoft.com/devcontainers/rust:latest",
 "customizations": {
   "vscode": {
     "settings": {},
     "extensions": [“rust-lang.rust-analyzer”]
   }
 },
 "postCreateCommand": "rustc --version"
}
```
!!! note "What does this code do?"
    Name: is a descriptive name for our dev container.

    Image: The docker image to use, here it is the latest rust environment. 

    Customization: installs the rust extension. 

    PostCreateCommand: a command to run after container is created, here it shows the latest rust version.
### Step 2: Reopen the Project in a Dev Container:

1. Press Ctrl + Shift + P (Cmd + Shift + P for mac) then type "Dev Containers: Reopen in Container".
2. You should see the latest Rust version at the bottom in terminal.

!!! note "Dev Containers: Reopen in Container"
    Reopening the Dev Container step is crucial since it activates the desired Dev Container environment. Here it is the Rust environment. 

## Part 3: Creating Your Rust Project:
1. In the terminal below you should see the Rust version. Next we need to create our Rust Project. In the terminal type the following code:
```
cargo new hello-comp423 –vcs none
cd hello-comp423
```
2. Navigate to the `src/main.rs` file and open it. Change the contents of the `println` function to say “Hello COMP423”
3. To print the contents there are two methods:
    * Use `cargo build` in the terminal. This compiles an executable file but does not run it. To run it do `./target/debug/main`. Note this is similar to using C in COMP 211 and running `gcc project-name` and it creates the executable a.out and to run the file you must type `./a.out`. The `cargo build` command is the compile part (`gcc project-name`) and using the ./ at the file location runs it.
    * Alternatively, the command `cargo run` (in terminal) does both in one step simplifying the process.

Congratulations you now have a working Dev Container to create a Rust Project in!
Many parts of this tutorial are inspired by Kris Jordan’s [Starting a Static Website Project with MkDocs](https://comp423-25s.github.io/resources/MkDocs/tutorial/#what-is-a-development-dev-container).