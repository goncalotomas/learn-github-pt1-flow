# Learn how GitHub works - Part 1, Workflows

This GitHub project does not contain any code, instead we only have poetry. This way you'll be able to focus only on the GitHub way of doing this and you won't have to learn any programming languages.  
Your goal to pass this challenge is to contribute to this repository by fixing spelling mistakes.

## How git works
Git is a distributed version control system, used for projects where many people are supposed to be handling the same codebase at once. To download and work on a local copy of the repository, you can run the following command on an UNIX shell (Windows has a similar git-shell executable):

```bash
git clone https://github.com/goncalotomas/learn-github-pt1-flow.git
```

This will _clone_ the code that is currently on the server and download it to a local folder that has the same name as the repository, in this case `learn-github-pt1-flow`. Navigate to the repository root folder by changing directory:

```bash
cd learn-github-pt1-flow
```

You are almost ready to start contributing to open source projects!

## Pushing and Pulling
Git has a concept of _pushing_ and _pulling_ code.  
Likewise to a _very exciting_ real life interaction with a door, when you _pull_ code you are bringing code to you (i.e. downloading code), and this may have several effects. When you type `git pull` in the terminal you are asking for the latest changes, and if everything proceeds as normal then you update your local copy of the code.  
As you've probably guessed by now, _pushing_ code is sending updates to the server where the code is hosted (GitHub), and this procedure is usually done every time a new feature is added to a program or a bug is fixed. Every time a person _pushes_ code, every one else should _pull_ in order to keep the local copies updated.

### How to push code
Git was designed for huge projects, and its flexibility can be sometimes hard to understand to newcomers. In order to push code changes to the repository, you need to say which files you want to push since git assumes that you might not want to send all of them!

First, git has a command that lets you see which files you changed by running `git status`. Here is an example result in a local repository with two changes made so far:

```bash
user@computer$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   src/Main.java
	modified:   src/MyAwesomeProgram.java
```

In order to tell git which changes you want to push, you have to use the `git add` command. You can add multiple files in a single command call, like follows:

```bash
git add src/Main.java src/MyAwesomeProgram.java
```

In most cases you will be able to use autocomplete features by pressing Tab (if you can't, maybe you should switch your operating systems or shell!)

> What if I want to add 100 files at once?

You can `git add` multiple files by referring to their parent directory, but git also supports working with wildcards. This means that the following 3 commands are equivalent for the previously shown project:

```bash
git add src/Main.java src/MyAwesomeProgram.java
git add src
git add *.java
```


### FAQ about git push and git pull

- What happens if I run `git pull` right after a `git clone`?
Unless the repository is **very** busy, nobody will have _pushed_ any changes in the time interval between your clone and pull operation, and basically the `git pull` will have no effect and it should report something similar to `everything up to date.`.
- What happens if I forget to push my code?
Nobody else will see your changes.
- How can I see if I pushed every

## Branches
