# A Brief Intro to Git and GitHub

Here we will walk through some of the basics of Git and GitHub, how to set up a GitHub account, and how to start using Git and GitHub to collaborate on projects.

###### Note
This is very closely drawn (and sometimes directly taken) from the MIT Big Data, Visualization, and Society class' Intro to Git and GitHub [linked here](https://github.com/ericmhuntley/big-data-spring2018/tree/master/github_instructions).

## Meet Git
Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency, according to the [Git website](https://git-scm.com/). Git is a software that tracks changes to text files so that individual contributors to a collaborative project can see historic versions, keep track of changes, and merge multiple versions.

## Meet GitHub
GitHub is a web platform that is built on Git to easily host and edit code, while moving across collaborators and projects. It provides a straightforward way for you to revise and run code on your computer and then sync the code online in your GitHub repository. GitHub is designed to make the collaboration process more transparent, so that once a file is in a GitHub repository, GitHub will flag changes within a file, and let any users know when they are trying to make changes to the same lines in the same file. This is called a **merge conflict**. If GitHub does not find a merge conflict, then the revised version of code is automatically updated on the online version of the repository. (This will make more sense in a moment.)

GitHub has been making the news lately given the recent acquisition by Microsoft. Check out this [article by Bloomberg about Microsoft's new acquisition of GitHub](https://www.bloomberg.com/news/articles/2018-06-06/github-is-microsoft-s-7-5-billion-undo-button) that includes a high-level description of some of the ways in which Github is super-duper useful!  

## The Language of Git

Git and GitHub uses specific terms across their platform and documentation (and these are adopted by the GitHub community). Here are some of the most common/essential terms, all taken from the GitHub Glossary. [For a more complete list of Git and GitHub terms, see the GitHub Glossary](https://help.github.com/articles/github-glossary/).

<dl>
	<dt>Repository</dt>
	<dd>A repository is the most basic element of GitHub. They're easiest to imagine as a project's folder. A repository contains all of the project files (including documentation), and stores each file's revision history. Repositories can have multiple collaborators and can be either public or private.</dd>
	<dt>Clone</dt>
	<dd>A clone is a copy of a repository that lives on your computer instead of on a website's server somewhere, or the act of making that copy. With your clone you can edit the files in your preferred editor and use Git to keep track of your changes without having to be online. It is, however, connected to the remote version so that changes can be synced between the two. You can push your local changes to the remote to keep them synced when you're online.</dd>
  <dt>Remote</dt>
  <dd>This is the version of something that is hosted on a server, most likely GitHub. It can be connected to local clones so that changes can be synced.</dd>
	<dt>Fork</dt>
	<dd>A fork is a personal copy of another user's repository that lives on your account. Forks allow you to freely make changes to a project without affecting the original. Forks remain attached to the original, allowing you to submit a pull request to the original's author to update with your changes. You can also keep your fork up to date by pulling in updates from the original.</dd>
	<dt>Fetch</dt>
	<dd>Fetching refers to getting the latest changes from an online repository without merging them in. Once these changes are fetched you can compare them to your local branches (the code residing on your local machine).</dd>
	<dt>Pull</dt>
	<dd>Pull refers to when you are fetching in changes and merging them. For instance, if someone has edited the remote file you're both working on, you'll want to pull in those changes to your local copy so that it's up to date.</dd>
	<dt>Merge</dt>
	<dd>Merging takes the changes from one branch (in the same repository or from a fork), and applies them into another. This often happens as a pull request (which can be thought of as a request to merge), or via the command line. A merge can be done automatically via a pull request via the GitHub web interface if there are no conflicting changes, or can always be done via the command line. For more information, see ["Merging a pull request."](https://help.github.com/articles/merging-a-pull-request/)</dd>
	<dt>Commit</dt>
	<dd>A commit, or "revision", is an individual change to a file (or set of files). It's like when you save a file, except with Git, every time you save it creates a unique ID (a.k.a. the "SHA" or "hash") that allows you to keep record of what changes were made when and by who. Commits usually contain a commit message which is a brief description of what changes were made.</dd>
	<dt>Push</dt>
	<dd>Pushing refers to sending your committed changes to a remote repository, such as a repository hosted on GitHub. For instance, if you change something locally, you'd want to then push those changes so that others may access them.</dd>
	<dt>Branch</dt>
	<dd>A branch is a parallel version of a repository. It is contained within the repository, but does not affect the primary or `master` branch allowing you to work freely without disrupting the "live" version. When you've made the changes you want to make, you can merge your branch back into the `master` branch to publish your changes.</dd>
</dl>

## Setting up GitHub

Sign up for a Github account on the [GitHub site](http://www.github.com) in which you can host projects and maintain repositories. Once signed up, go to your profile page.

Note: you can use the MIT enterprise account on the [MIT enterprise GitHub page](https://github.mit.edu/) or create your own account on the regular [GitHub site](http://www.github.com). To learn more about the MIT enterprise account, [see here](https://ist.mit.edu/github-enterprise).


### Creating a GitHub repo

To start, we will create a project, or in GitHub speak, a **repositories** on Github (or **repos** for short). Repositories allow you to collaborate, share, and modify scripts, programs, and websites. Project repositories can be named just about anything, but you should pick something relevant to your project. (For example, this file is stored in a repo called **reilab**.) Keep in mind that GitHub can be used to version control just about any textual content written in just about any scripting or markup language.

If you are on the GitHub landing page, start by clicking on `start a project` to create a new repo. If you're on your profile, start by clicking on the 'repositories' tab. In the upper right corner, select ‘new’ to create a new repository. Give your new repository a description, make it public, and initialize it with a README. (Don’t worry about the license, but you can add a .gitignore file using python at this point.) When you're done, click 'create repository.'

Now that we have a repository, we can **clone** copies to local drives, add content, manage files, and make changes. First, though, we need to set up Git on our machine. Once we've done this, we will be able to interact with our remote GitHub repositories using the Git command line utility.

## Getting Started with Git

People work with GitHub in one of two ways: either via command line, or with a Desktop GUI. Here, we will help you get started using the command line.

**Important Note for Windows users:** First, some bad news: coders tend to favor Unix-like operating systems (e.g., OS X or Linux). Windows is **not** a Unix-like operating system! The Windows command prompt is built on DOS. To easily use the command line to interact with Github, you will need to install Git Bash, which is a terminal that emulates essential Unix-like shell functionality and includes the Git command line utility. This can be downloaded from the [Git for Windows project](http://gitforwindows.org/). Once installed, proceed below, noting only that your command line work will be done in the Git Bash shell, not Terminal or Command Prompt.

### Check That Git is Installed

Open Terminal (OS X or Linux) or Git Bash (Windows) and enter the following command:

```sh
git –-version
```

If Git is correctly installed on your machine, you will see the version. If you get an error, or you don’t see the version, you need to install Git. Download Git from the downloads page on the [ Git homepage](https://git-scm.com/). The defaults should be fine. You might need to restart your machine afterwards; at the very least, you'll have to restart Terminal.


### Create a Directory for Github Projects

Setup a local folder to contain local copies of your GitHub repositories. The easiest way to edit code is to work on it locally. You can then sync local clones with the GitHub remote repositories so that others can see and use your changes, and so that you can pull changes others have made.

To create a directory from Terminal or Git Bash, use the `mkdir` command as follows:

```sh
mkdir ~/Desktop/github
```

This will create a folder called 'github' on your Desktop. The tilde character followed by a slash (`~/`) on Unix-like operating systems is a shortcut that refers to your home directory. On OS X, this is equivalent to typing the longer path `/Users/<your username>/Desktop/github`. In Git Bash this is equivalent to `c/Users/<your username>`.

### Change Your Working Directory

Now that you've created a folder to store your Github projects, you'll want to change your working directory to that new folder. You can c-hange your d-irectory with the `cd` command and tell the terminal to p-rint your w-orking d-rectory using the `pwd` command.

```sh
cd ~/Desktop/github
```

The above commands should print your working directory before and after changing it. The ‘github’ folder is now your working directory and commands we run will be happening in this directory. We will work locally on our Github repositories in this space.

For documentation on additional command line commands and shortcuts, [this cheatsheet](https://github.com/0nn0/terminal-mac-cheatsheet) can be very helpful.

### Clone a copy of the repository you want to work on

Create a clone of the website repository on your machine so you can edit code and files. This will allow for pulling, merging, and pushing changes you make to your files.

To access Github commands in the terminal, use the term `git` to begin your statement---this calls the Git command line utility. We can download our Github pages repository using the `git clone` command. Go to your GitHub repo online and click on `clone or download` and copy the link that pops up. Then, in your command line, type:

```sh
git clone [**insert copied link here**]
```

For our purposes (and for the success of the rest of this tutorial!), please start by forking the `reilab` repo. Go this page (https://github.com/epkh/reilab) and click on the `Fork` icon in the top right corner of the page. This will make a copy of the `reilab` repo to your own GitHub account. Then go to your GitHub profile and look at your list of repos; you should see one there called `reilab`! Click on it. Then, as we described above, click on `clone or download` and copy the link that pops up. Then, in your command line, type:

```sh
git clone [**insert copied link here**]
```

## Setting up your Atom Text Editor

When editing code, you'll use a text editor and NOT a word processor. A text editor is a simple program that edits plaintext files. This is very different from a word processor (e.g., Microsoft Word, Apple Pages, LibreOffice Writer). Text editors work with text and text only; what you see in a text editor window is the entirety of the file. Text editors are used to write code, scripts, and programs. But you can also use them to typeset documents using markup languages like Markdown and LaTeX, often in conjunction with command line utilities like Pandoc.

You can use your text editor of choice, but for working with GitHub, I prefer to work with **Atom**. If you'd like to try it, you can [download it here](https://atom.io/). Atom was created by GitHub and thus handles version control and merge conflicts in a very user-friendly fashion. With the `Hydrogen` [package](https://atom.io/packages/hydrogen), Atom is able to have some of the functionality of a [Jupyter Notebook](http://jupyter.org/).

### Opening Atom from the Command Line

If your working directory is still in your Github repo, you can open your repo as a project directory in Atom from the command line as follows:

```sh
atom ./
```

`./` is how you explicitly say 'the current folder.' If you receive a 'command not found' error, you'll have to open Atom from your applications folder or Start menu, then...

#### On Mac OS X
From the `Atom` dropdown menu, select "Install Shell Commands."

#### On Windows
You'll have to add a directory to your PATH variable---basically, this is how Windows knows what commands to include in its command line. Search for "Edit the System Environment Variables" from the start menu and open it. Click "Environment Variables..." at the bottom. Edit "Path", add a new path using the "New" button, and use the path `%LOCALAPPDATA%\Atom\bin`. Click OK, restart Git Bash, and you should be able to run Atom from the command line as described above.

### Edit the Github README.md

You should see your Github pages repository open in the file tree on the left side of the Atom window. Open the `README.md` file, which is a markdown file. Markdown only requires a single octothorpe character (`# Heading Text`). Documentation of Github's variant on Markdown (called 'Github-flavored Markdown') is [here](https://help.github.com/articles/basic-writing-and-formatting-syntax/). Markdown is a useful way of creating documentation for your GitHub repos.

Text contained in a README.md file in your repo's root folder is displayed by default when visitors view your GitHub repo. You'll want to describe your project: what it is, what it does, how do do it, and how people who fork a copy are permitted to use it.

## Git's Stage-Commit-Push Workflow (How to push changes to your repo)

The following series of tasks are very, very common series when working with Github repos. We'll

1. Check the **status** of our repo,
2. Stage (or **add**) our changed files,
3. **Commit** our changes, and
4. **Push** our changes to Github.

Over time, this workflow should be part of your muscle memory.

### Check repo status

First, while in your repo working directory, start by checking the status of your local repo as follows:

```sh
git status
```

This will output a list of changes made since the last commit or, in this case, since the repository was initialized. You should see that we've modified our `README.md` file. In order to commit these changes to our remote repository, we need to stage them first.

### Stage your changes

Second, you can stage your changes by using:

```sh
git add <filename>
```

This puts the files into the Git 'staging area.' You can add multiple files to your staging area at once. You can stage individual files using the following syntax:

```sh
git add README.md
```

In many cases, you'll find that you want to stage all modified, added, or deleted files. This could quickly become very tedious if you were required to stage files one-by-one. Luckily, this is not the case! You can simply use:

```sh
git add .
```

Check the result by typing in `git status` again to see that the changes are ready to be committed. If you ever need to unstage anything, use the following:

```sh
git reset HEAD <filename>
```

**Note:** Files are not staged in their entirety. Rather, changes to the files are staged.

### Commit changes

Once we've staged our files, we're ready to commit our changes and update the remote repository. We start locally---that is, with the repository stored on our local disk. Remember that Git acts as an intermediary between us and our edits. When we change files on our local machines, Git keeps track of changes, but we need to commit those changes to the local repository so that Git knows we'd like to consider this a checkpoint.

It is considered good practice to add a comment to your commit that describes the changes you made to the files. This helps others working with your code---and you, two months from now---know what you did that was worthy of a commit. For example, for this exercise, our comment might be: 'updated the README.'

To commit our files, we use `git commit`. We add a `–m` flag to indicate that we'll be including a message with our commit. In terminal, still in your working directory and with our files staged, type the following command:

```sh
git commit –m "updated the README"
```

This commits our changes to the local repository. You will see a note that files in your master branch were changed and created.

In the future, if you want to stage all previously staged files and commit them in one fell swoop, you can use the `-a` option of the `git commit` command like so:

```sh
git commit -am "commit message"
# OR its syntactical equivalent:
git commit -a -m "commit message"
```

### Push changes to GitHub

The last step is to **push** our committed changes to the remote repository. We do this using `git push`. The syntax for this is `git push origin <branchname>`. This will push the file to the remote origin and match it to the name of the branch. We'll talk more about branches below; for now we can just type `git push` which defaults to the `master` branch on the remote origin. To push our files to GitHub, use the following:

```sh
git push
```

You will then have to authenticate by typing your GitHub username and password. This will push our master branch to GitHub and sync our files.

Navigate to your Github page and check out your repository. You should see your README.md modifications.

## Credential Management

While it's great that GitHub wants to keep you secure, if you're on your personal computer, you may not want to enter your credentials every time you push changes to your remote repository. Luckily, Git provides a number of built-in ways to store your credentials for later use. You can do some reading on these [here](https://git-scm.com/book/en/v2/Git-Tools-Credential-Storage) if you'd like, but here we will use the 'cache' method. This method stores credentials in memory, not on your hard disk, and they are purged after a given period of time. Other methods require that you store your credentials in plain-text files on your hard drive.

To prevent GitHub from asking for your credentials for 30 minutes after they are entered, type the following command from either Terminal or Git Bash:

```sh
git config --global credential.helper 'cache --timout=1800'
```

You can modify your timeout value, measured in seconds, to your liking.

## Working with Branches

Up to this point, we have been working with what's called the `master` branch. The `master` branch is the main branch of our repository, and should always be kept working and clean. Branches allow you to create separate lines of development, including commits, that do not affect the `master`. These can then be merged into the `master` when they're complete, or abandoned if something doesn't work out. Long story short: if you're doing something that could conceivably break your code, you should make a new branch.

Keep in mind that creating new branches will **not create new local file directories**. That is, if you make changes to a local file while a non-master branch is checked out, the changes are stored in the local Git repository while the original local file remains unchanged (as it is represented by the `master` branch in Git). (A handy thing about using Atom is that you can easily see which branch you're working on in your text editor window.)

### Create a branch based on the master branch

To create a branch based on the `master` branch, use the following syntax:

```sh
git checkout –b <new branch name> <existing branch name>
```

For example, we can use:

```sh
git checkout –b testchanges master
```

This will create a new branch called `testchanges` based on the `master` branch. Technically the `master` part at the end is unnecessary, but it is almost always better to be verbose.

### Show all local branches

Show all branches of the repository using the following command:

```sh
git branch
```

**Note:** An asterisk will appear next to the current working branch.

### Make changes to your README

In your text editor, add a another line of text to your README to demonstrate how branches work.

Now stage the changes, commit them to your `testchanges` branch, and push them to your remote repo. Branches can be committed to the local repository and synced to the remote repository (on the GitHub site) using the very same **push** process described above.

### Merge branches

Let's say that we're done implementing changes that we've been building on the `testchanges` branch and that you'd now like to fold them into the `master` branch. Git calls this a **merge**. To merge `testchanges` back into `master`, change to your `master` branch using checkout, and then use the merge command.

```sh
git checkout master
git merge testchanges
```

If you're working on a project alone, it's likely to be smooth sailing. In collaborative settings with multiple people working on the same lines of code, you may experience what are called **merge conflicts**. In short, conflicts will be flagged in your file when you open it in a text editor. You will have to go through your file and find conflicts, decide which change to accept, and then delete the surrounding conflict markers. It's worth reading up on resolving merge conflicts [here](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/).

### Delete a Branch

If you ever need to delete a branch---maybe you're done working in a branch and have merged changes---use the –d key of the branch command. For example, to delete test-changes, use:

```sh
git branch –d testchanges
```

## Fetching changes from Github

Often you will need to incorporate changes to the remote repository into the clone on your local drive. To do this, you will use the `git pull` or the `git fetch` command. `git pull` will retrieve new work done by other people and merge the local changes with changes made by others (this may cause merge conflicts). `git fetch` will retrieve new work, but will not automatically merge it. More information on this on the [Github help pages](https://help.github.com/articles/fetching-a-remote/).


## Additional Reading and Resources

[Hello World tutorial on GitHub](https://guides.github.com/activities/hello-world/)

[Mac Command Line Cheatsheet](https://github.com/0nn0/terminal-mac-cheatsheet)

[Github Glossary of terms](https://help.github.com/articles/github-glossary/)

[Cheatsheet of essential Git commands](https://education.github.com/git-cheat-sheet-education.pdf)

[Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#blockquotes)

[GitHub Flavored Markdown cheatsheet and info](https://help.github.com/categories/writing-on-github/)
