+++
title = "Development Environment as Code"
description = "T"
date = 2021-05-01T08:00:00+00:00
updated = 2021-05-01T08:00:00+00:00
draft = false
weight = 20
sort_by = "weight"


[extra]
toc = true
top = false
+++

The [Visual Studio Code Remote - Containers](https://code.visualstudio.com/docs/remote/containers) extension lets you use a Docker container as a full-featured development environment. This fixes the following problems

* Enables developers other than yourself to get quickly up to speed
* Stops issues such as "It works on my machine"
* Allows you to check your development environment into git.

## Installation

Install the devcontainer extension in VSCode and then setup a Rust environment.

![Creating a vault](/containers-extension.png)

## Install Rust on Nails

We have pre-configured a development environment with all the tools needed to create a full stack rust application.

To get started create a folder for your project. Change directory into that folder then run.

```
mkdir project-name
cd project-name
```

### MacOS and Linux

```sh
curl -L https://github.com/purton-tech/rust-on-nails/archive/main.tar.gz | \
  tar xvz --strip=2 rust-on-nails-main/nails-devcontainer/ \
  && rm devcontainer-template.json
```

## Windows

```sh
curl -L https://github.com/purton-tech/rust-on-nails/archive/main.tar.gz | \
  tar xvz --strip=2 rust-on-nails-main/nails-devcontainer/ \
  && del devcontainer-template.json
```

## VS Code

Load the folder into visual studio code. On the bottom left corner of VS Code you should see a green icon. Click on this and select open in container.

After the container is downloaded you will have a preconfigured development environment with the following folder structure.

How you folder structure will look.

```sh
.
└── .devcontainer/
    ├── .bash_aliases
    ├── .githooks/
    │   └── precommit
    ├── devcontainer.json
    ├── docker-compose.yml
    └── Dockerfile
└── .gitignore
└── README.md
```

## Setting up Git

Open up a terminal in VSCode (CTRL + `) and execute

```sh
$ git init
Initialized empty Git repository in /workspace/.git/
```

## Add a Workspace

We are going to create a workspace for our web application. Create a new `Cargo.toml` file in the root folder and add the following.

```toml
[workspace]
members = [
    "crates/*",
]
```

Open up the terminal in VSCode again and run the following

```
$ cargo new --vcs=none crates/axum-server
     Created binary (application) `crates/axum-server` package
```

You should now have a folder structure like the following.

```sh
├── .devcontainer/
│   └── ...
└── crates/
│         axum-server/
│         │  └── main.rs
│         └── Cargo.toml
├── Cargo.toml
└── Cargo.lock
```

## Testing

Test out you development environment with

```
$ cargo run
   Compiling app v0.1.0 (/workspace/app)
    Finished dev [unoptimized + debuginfo] target(s) in 1.16s
     Running `target/debug/app`
Hello, world!
```

## Commit your code

From the `/workspace` folder

```
$ git add .
$ git commit -m"Initial Commit"
```
