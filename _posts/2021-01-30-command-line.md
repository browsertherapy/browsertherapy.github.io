---
title:  "Command Line Basics"
toc: true
categories: Cheatsheet
tags: featured
---

## Terms and Definitions
Command Line Interface (CLI)
: An alternative to Graphical User Interfaces (GUI) that are based on mouse clicks. Terminal apps come in a few flavours; in this course you can use a unix terminal of your choice.</dd>

The Terminal
: A nickname for an application that understands one or more Command Line Interfaces (CLIs).

Workspace
: A dedicated folder(s) on your system for the projects you'll be working on.

Command Prompt
: Usually the last line shown in the terminal where you enter your commands. Often represented by a `$` or `#` in examples online (see warning below).

Option Flag
: A common way to specify options for command-line programs. Usually denoted by either a dash (`-`)immediately followed by a letter. For example, `ls -a` lists _all_ directory contents (including files that are hidden by default).

---

**Notice**: General information will be displayed in boxes such as this one. Warnings will be in red (see below) for information that will help you avoid potential problems. 
{: .notice .notice--info}

**Warning**: There are two flavours of "command line": Windows and Unix. We will be using the latter: Git Bash (installed along with Git) on Windows and Terminal on Mac (Mac is unix-based so almost any terminal app will do; Tony uses [iTerm](https://iterm2.com/)). 
{: .notice .notice--warning}

## Navigating the file system
Most of the command line tools we will be using in this course (like Git, [Node](https://nodejs.org/en/) and [NPM](https://www.npmjs.com/)) will **depend greatly on which directory you are in**. We will cover the three system commands that help up us navigate the file system.

**Notice**: The examples below start with a `$`. Do not include this when typing commands; it's there to represent the command prompt.
{: .notice .notice--info}

## `pwd` - Present working directory
Use the `pwd` command to see where you are when you open the terminal.

    ```shell
    $ pwd
    ```

**Notice**: The starting directory for most systems will be your home directory.
{: .notice .notice--info}

## `ls` - List directory contents
List the contents of your current directory with the ls command:

    ```
    $ ls
    ```

The `-l` **flag** lists extra information about the contents:

    ```
    $ ls -l
    ```

Add the `-a` to list hidden files:

    ```
    $ ls -a
    ```

You can also combine multiple options with a single flag. To list extra information _and_ also all hidden files:

    ```
    $ ls -la
    ```

## `cd` - Change directory
Use the `cd` command to switch to another directory. Assumimg you are currently in your home folder, you can move to your downloads folder with:

    ```
    $ cd Downloads
    ```

OR, move there from anywhere on the system with an absolute path (replace `username` with your login handle):

    ```
    $ cd /Users/username/Downloads
    ```

Move up one directory:

    ```
    $ cd ..
    ```

OR move up many directories

    ```
    $ cd ../../..
    ```

Move multiple directories "downstream":

    ```
    $ cd some/path/relative/to/your/location
    ```

Combine `../` with a relative path for more flexibility. To move to a directory that adjacent to your _present working directory`:

    ```
    $ cd ../adjacent-directory-name
    ```

If you get lost you can always move to your home directory:

    ```
    $ cd
    ```

**Notice**: Below are _Pro-tips_ that will give you some hints on how the pros do things. In this case, there are some _quality of life_ tips that will reduce the grind if using the command line. 
{: .notice .notice--info}

**CLI Quality of Life Tip #1**: The tab key auto-completes file names and directories.
{:  .notice .notice--pro-tip}

**CLI Quality of Life Tip #2**: Use the Up Arrow to browse through the history of last used commands.
{:  .notice .notice--pro-tip}

### Questions to Consider
- What is the starting directory when you open a terminal on your system?
- What files and directories are in this initial directory?
- What file did you last open? Try to find it using only the terminal.
- What's at the top of your directory structure? How do you get there?
- Using the terminal, find the directory you've chosen to store your projects.
