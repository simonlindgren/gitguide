# gitguide

**Basics**

> [Introduction and setup](#introduction-and-setup)

> [Initialising a repository](#initialising-a-repository)

> [Committing](#comitting)

**Workflow**

> [Pushing](#pushing)

> [Forking](#forking)

> [Branching](#branching)

> [Pull requests](#pull-requests)

## Introduction and setup
Git is a version control system. It is installed and maintained on your local system. It manages a record of versions of ongoing projects (coding, writing, etc.).

GitHub is a cloud-based hosting service for sharing Git version control projects outside of your local computer. This also enables others to comment and contribute to your projects.
Git/GitHub tutorial

Check if you have Git installed by doing this:

```
$ git --version
```

If you don't have it installed,or if you want a more recent version, current installers are available from the Git project.

Set up your user info:

```
$ git config --global user.name "Your name here"
$ git config --global user.email "your_email@example.com"
```

You can also set up your editor of choice:

```
$ git config --global core.editor "atom --wait"
```

Enable ssh connection to GitHub. First, check if you have ssh keys on your computer:

```
$ cd ~/.ssh/id_rsa
$ cd ~/.ssh/id_rsa.pub
```

If you don't have them, create them.

```
ssh-keygen -t rsa -C "your_email@example.com"
```

Copy the contents of your public key into the clipboard:

On mac, use pbcopy:
```
$ pbcopy < ~/.ssh/id_rsa.pub
```

Another option is to `cat` the contents and copy them manually.
```
$ cat ~/.ssh/id_rsa.pub
```


If you don't have a GitHub account, go create one. Otherwise, log in to your existing account and do this:

- Go to your github account *Settings*
- Click “SSH and GPG Keys” on the left
- Click “New SSH Key” on the right
- Add a title (like “My laptop”) and paste the public key into the big text box
- Add the key

Back in Terminal, test the key:

```
$ ssh -T git@github.com
```

It has succeeded if it says something like:

```
Hi username! You've successfully authenticated, but Github does not provide shell access.
```

## Initialising a repository

When working on a project (writing, coding etc.), create a directory on your computer for that project. In that directory, enter `git init`.

This will create the hidden subdirectory .git which contains all information required for version control of your project. Your project is now a git project.
Add

When you have modified your project, and want to tag the changes in a file as ready (for now), do:

```
$ git add file.md   <-- adds single file
$ git add file.md file2.md   <-- several files
$ git add .   <-- add all files
```

You can check which files have been staged by `git status`.

Note that git add is used to add completely new files as well as to “add” modifications to files that already exist in the repository.

### Initialising a repository on github.com

If you have created a repository through the web interface at github.com, and later on want to work on it via command line, the process is the same as descibed under [Pushing](#pushing).

## Committing

Enter `git commit` to add the modifications to the repository. That will open up your editor of choice for you to enter a commit message (a note on what was changed). It is easier to do this without the editor, like this:

```
$ git commit -m "Fix such and such"
```

Commit messages are commonly written in the future tense.

If you want to commit all of the modifications you have made, without having to explicitly add each file, you can skip the separate add and commit commands and just type:

```
$ git commit -a -m "Fix such and such"
```

## Pushing

To be able to push the Git repository to GitHub, a home for it must be created at GitHub. 

- Go to GitHub and log in
- Click the new repository option in the top-right menu
- Give it a name and click to create

Then back in Terminal:

```
$ git remote add origin git@github.com:username/reponame.git  <-- use this ssh link, not https when cloning
git branch -M main
git push -u origin main
```

Now you can use `git push` to push your commits to GitHub.

## Forking

If you want to modify and/or contribute to someone else's project on GitHub, you can fork their repository.

- On the GitHub website, click "Fork" in the original repo. This will create a forked version in your own account.
- In your forked version of the repo, click the "Clone or download" button, and copy the git address (something like: `git@github.com:yourusername/therepo.git`).
- In Terminal (and in your desired project folder) enter git clone followed by your copied git address. This copies down both the contents and the commit history (i.e. the hidden git subdirectory).

If you just want to use this fork for adding your own modifications, and keeping them in this fork, you can continue from here with git commit and git push as described above.

If you want to take the project in a completely different direction, or for some other reason disconnect it from the orginal one and not receive updates from it, skip the whole forking thing and just [import a copy](https://docs.github.com/en/free-pro-team@latest/github/importing-your-projects-to-github/importing-a-repository-with-github-importer) of the repo.

## Branching

Branches are very useful for working on your own projects to try to fix or modify stuff without disturbing the master branch. If things work out, it can all be merged back into the master, and if not, the branch can be trashed.

- First, make sure that you are updated with `main`: 
    - `git branch`
    - `git checkout main`
    - `git pull origin main`

- Create a branch and name it: `git branch my_branch`.
- Checkout the branch: `git checkout my_branch`.
    - Double check: `git branch`
- Make your changes, then add and commit.
- To push the branch to GitHub: `git push origin my_branch`.
- If you are happy about the changes in the branch, merge them into the master: `git checkout master` and then `git merge my_branch`.

While working on a branch, you can always switch between working on the master, and on the branch by: `git checkout master` or git `checkout my_branch`.

When done with a branch, delete it: `git branch -d my_branch`. Delete it from GitHub too, if you pushed it: `git push origin --delete my_branch`.

## Pull requests
If you have forked a repo, and want to contribute back to the original project, branching is also part of the workflow:

- Create, checkout, and modify a branch of your forked project as above.
- Instead of merging, you need to request for the owner of the original repo to merge your changes. This is done by [making a pull request on GitHub](https://guides.github.com/activities/forking/#making-a-pull-request).


## Some other things

`git status`: You’ve made some changes to a project, but you’re not sure what. Type git status to see a list of files that have been changed, plus new files that haven’t been formally added.

`git diff`: Exactly what changes have you made? Type git diff. To see your changes to a particular file, type git diff filename.

change the last commit message: `$ git commit --amend -m "New commit message"`

`.gitignore`: The various files in your project directory that you are not tracking in git should be indicated in a .gitignore file. You don’t have to have a .gitignore file, but if you don’t, those files will show up every time you type git status.
