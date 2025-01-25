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