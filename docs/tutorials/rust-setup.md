# **Setting up a Dev Container for Rust**

* Primary author: [Prasun Sapkota](https://github.com/psap2)
* Reviewer: [Ayush Godhani](https://github.com/avgod07)

Hey! This tutorial will walk you through how to set up a dev container for Rust. This tutorial will create a Rust Development Container in VS Code to make cohesive development enviorments.

## **Prerequisites**
1. A GitHub account: If you don’t have one yet, create one at [GitHub](https://github.com).
1. Git installed: [Install Git](https://git-scm.com) if you don’t have one already.
1. Visual Studio Code (VS Code): Download from [here](https://code.visualstudio.com).
1. Docker installed: Required to run the dev container. [Get Docker here](https://www.docker.com).

## Part 1. Project Setup: Creating the Repository
### Step 1. Create a Local Directory and Initialize Git

1. Open your terminal or command prompt
1. Create a new directory for the project. (Note: Of course, if you'd like to organize this tutorial somewhere else on your machine, go ahead and change into that parent directory first. By default this will be in your user's home directory.)

    ```bash
    mkdir rust-tutorial
    cd rust-tutorial
    ```

1. Initialize a new Git repository:
    ```bash
    git init
    ```

1. Create a README file:
    ```bash
    echo "# Setting up Dev Container for Hello World! in Rust" > README.md
    git add README.md
    git commit -m "Initial commit with README"    
    ```

### Step 2. Create a Remote Repository on GitHub

1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
1. Fill in the details as follows:
    * Repository Name: rust-tutorial
    * Description: "Hello World! in Rust setup using Dev container"
    * Visibility: Public
1. Do not initialize the repository with a README, .gitignore, or license.
1. Click Create Repository.

### Step 3. Link your Local Repository to GitHub
1. Add the GitHub repository as a remote:
    ```
    git remote add origin https://github.com/<your-username>/comp423-course-notes.git
    ```
    Replace `<your-username>` with your GitHub username.

1. Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: `git branch -M main`. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

1. Push your local commits to the GitHub repository:

    ```
    git push --set-upstream origin main
    ```

1. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Part 2. Setting Up the Development Environment
### Step 1. Add Development Container Configuration
1. In VS Code, open the rust-tutorial directory.
1. Install the Dev Containers extension for VS Code.
1. Create a .devcontainer directory in the root of your project with the following file inside of this "hidden" configuration directory:

    `.devcontainer/devcontainer.json`

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

* `name`: A descriptive name for your dev container.
* `image`: The Docker image to use, in this case, the latest version of a Rust environment. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!
* `customizations`: Adds useful configurations to VS Code, like installing the Rust extensions that are useful in code analysis and formatting. You can add more of these extensions by searching for VSCode extensions on the marketplace. You can use the string identifier of each extension in its sidebar, and add those extensions here to ensure other developers on your project have them installed in their dev containers automatically to maintain a cohesive enviorment.
* `postCreateCommand`: A command to run after the container is created. This command executes `rustup update` to ensure the Rust's toolchain, a complete set of tools needed to develop Rust programs, is upto date. Then it executes `rustc --version` which checks and displays the installed version of the Rust compiler. With this setup, we can confirm that the Rust environment is ready and is operating correctly when the container is started.

    ```json
    {
        "name": "Hello World! in Rust",
        "image": "mcr.microsoft.com/devcontainers/rust:1-1-bullseye",
        "postCreateCommand": "rustup update && rustc --version",
        "customizations": {
            "vscode": {
                "extensions": [
                    "rust-lang.rust-analyzer",
                    "rust-lang.rust"
                ]
		    }
	    },
    }
    ```