---
parent: "Lab 01: Setup"
title: Setup
nav_order: 1
---

## Install Git

This step will depend on your OS:
 - Windows: 
     - head over the https://git-scm.com/download/ and download the Git for Windows installer.
     - run the installer, using all the recommended/default options
 - MacOS: 
     - install Homebrew: https://brew.sh/
     - In the terminal, install `git` by running `brew install git`
 - Linux/Other:
     - use your system's package manager (apt, dnf, pacman, etc) to install `git`. For example, Ubuntu users should run `sudo apt install git`.

To verify that Git is installed, open up your terminal (Git Bash on Windows), and run `git --version`. You should see something like `git version [numbers]`.

## Install Rust

Follow the instructions at https://www.rust-lang.org/tools/install. It's suggested that you use `rustup`, which will automatically install `cargo` and `rustc` for you.

To verify that Rust is installed, run `rustup --version`. You should see something like
```
rustup 1.25.1 (bb60b1e89 2022-07-12)
info: This is the version for the rustup toolchain manager, not the rustc compiler.
info: The currently active `rustc` version is `rustc 1.65.0 (897e37553 2022-11-02)`
```
but with different numbers.

## Install VSCode

You can use a different text editor if you wish (such as Atom, Sublime, or Neovim), but the rest of this course will assume that you are using VSCode.

Download and install VSCode here: https://code.visualstudio.com/download


## Install the rust-analyzer extension

If you are using VSCode, open the "Extensions" panel in the laft sidebar, and search for the "rust-analyzer" extension. You can also find the extension here: https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer

If you are using a different text editor, you can find instructions to install it here: https://rust-analyzer.github.io/. Any text editor that supports the Language Server Protocol will support rust-analyzer


## Install Python

Download and install Python 3 here: https://www.python.org/downloads/

Python is just used for running local web servers; if you don't want to install Python, you could use an alternative like [http-server](https://crates.io/crates/http-server).

## Set up a local repository

 - If you haven't already, make an account on [Github](https://github.com/). You'll need to create either a personal authentication token or an SSH key for your account; instructions on creating a PAT are [here](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).
 - On github, create a new, **private** repository. You can name it anything.
 - Clone your new repository (`git clone https://github.com/yourusername/example-name.git`). Git may give you a warning ("You appear to have cloned an empty repository"), which is completely fine.
 - In your new repository, add the skeleton repository as a remote:
    ```
    git remote add skeleton https://github.com/sberkun/61b_rust_skeletons.git
    ```
 - Pull code from the skeleton, and push it to your private repo:
    ```
    git pull skeleton main
    git push
    ``` 
 - Open your new repository on Github. If you see the skeleton code, congratulations! You have successfully set up your repository.