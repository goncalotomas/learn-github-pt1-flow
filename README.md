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

The second command is adding all changes for files inside the `src` directory, while the third command is adding all files with the `.java` extension.

If you run `git status` again after adding the changes you want to push, you'd see something like this:

```bash
user@computer$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  modified:   src/Main.java
	modified:   src/MyAwesomeProgram.java
```

> Can I push now...?

No.  
You see, git has strict rules about how your updates are sent to the server/repository. Updates, or code pushes, are sent out in batches. Each batch of updates needs to have a descriptive message of what the changes are to make it easier for other people working in the project to understand what is happening. The only thing missing here is to choose an adequate message for the changes and creating a "batch of changes" that is referred to as a _commit_. This can be done with the `git commit` command:

```bash
git commit -m "fix NullPointerException error"
[master 8ca1aff] fix NullPointerException error
 2 files changed, 3 insertions(+), 3 deletions(-)
```

> Finally! So everyone has to do a "git pull" now?

Not yet! Your changes are still only on your computer!  
Git is lazy: you can create multiple "batches of changes" (start remembering these as _commits_ from now on) and you need to _push_ in order to send ALL of your locally stored _commits_ to the repository.

So now your final step is to actually run `git push origin master`. You'll learn why you need `origin` and `master` in following sections.

**NOTE:** It is very easy to underestimate Git and say it is too complicated, but the reason why you should be learning git is for all of the cool features you have yet to see. I just want you to know that it is normal to think this is too much work to keep code on a repository, but you'll learn why everyone serious uses it when things _don't_ go as planned :)

## Branches
If you made it this far you're already capable of having a project with 1-2 people and you should be able to work smoothly.  
However, as soon as the group you're working in grows, you increase the chance of having _conflicts_ when you pull or push code. _Conflicts_ happen when more than one people changes the same bit of code (git is able to check line by line if it has been changed). In the previous example, if someone added changes to `src/Main.java` while you were changing the same part of code locally, you'd get an error when you tried to push code saying you needed to perform a `git pull` to get all the latest changes. When you _pull_ your code, you'd see all these merge conflict messages that are not going to be addressed in this tutorial, but you should understand that before working on a piece of code you should check if someone has sent changes to the server.

> OK, so how do I avoid conflicts?

Well, a good way is to make sure that no one works a section of code if there is already someone else assigned to it. This will ensure you will not have merge conflicts, but git provides easier workflows that don't involve this assumption: branches.

### Creating a new branch to implement a feature or to fix a bug

You can see a branch as a version of the code. Every repository needs a pre-defined main branch, which in GitHub is called `master` by default. When people `clone` your repository they will download the `master` branch, and since it is the main branch some extra attention is needed when _pushing_ changes to the branch.

Let's imagine that `Main.java` contains code for a social network server, and that in the `master` branch so far the server does not support friendships between users. You are assigned the responsibility of adding that feature and you are told by the project manager that nobody can commit to `master`. How should you proceed?

The logic behind branches is more or less the same about _commits_, in the sense that you should create a "version of the project" (branch) where you are going to work specifically in adding the friendship feature, and then we will see how to get that _committed_ into the `master` branch of the repository.

Creating a branch is super easy:
```bash
user@computer$ git checkout -b add-friendships
Switched to a new branch 'add-friendships'
```

The command is `git checkout` and it needs one argument passed in via the `-b` flag that is the branch name. The name should make it trivial to understand what type of changes are going to be in this "version of the project".

Now you'd make all the changes you needed to add the friendship feature to your social network server, and you could follow the `git add` and `git commit` instructions above, but _pushing_ is slightly different. If you already added and committed your changes, you need to execute the following command:

```bash
user@computer$ git push origin add-friendships
[... some text omitted here ...]
 * [new branch]      add-friendships     -> upstream/add-friendships
```

The only thing that changes from the previous `git push` command is that instead of pushing to the main branch (the `master` branch), you're pushing to a new branch that did not exist yet, explaining the last line that mentions the creation of a new branch on the server.

### Making the changes from one branch end up in the master branch
If you're keeping up thus far you're not going to be disappointed!

Now that you've sent your changes to the repository in a separate branch, you can use the GitHub web interface and go to the "Pull requests" tab:

![Click the Pull requests tab](http://i.imgur.com/otgvYbw.png)

Then click the "New pull request" button:

![Click the green button](http://i.imgur.com/1CNGpYG.png)

And finally leave the base branch as `master` select your branch (`add-friendships` in the example) for the compare field and click the "Create pull request" button:

![Click the button after selecting the compare field](http://i.imgur.com/7B4fRCq.png)

This will open a new item in the Pull requests tab listing all of the commits that were done in that branch as well as some additional information about Git's checks for conflicts (that should not happen if you always create new branches for adding new features or fixing bugs):

![Click the merge pull request button](http://i.imgur.com/V34IHNa.png)

You can click the "Merge pull request" button if the green check mark is shown, symbolizing that there are no conflicts with the `master` branch. Once the process is done, the changes you made in the `add-friendships` branch are added to the `master` branch. The advantage of using pull requests instead of committing directly to master besides the lower chance of errors is that the workflow scales to big teams, and you'd be surprised about all the features that the GitHub web interface offers. For instance, once you open a pull request you may assign someone else (normally the repository owner or someone else who knows about what you worked on) to review your changes and only merge them into `master` if everything is OK. That way, possible errors that you might have unknowingly introduced can be catched by someone else and you won't be responsible for "breaking everything".

## Some cool things about contributing
If you're working on a pull request for a public repository and you get it accepted, it will show on your GitHub contribution score in your profile. Not only does it count how many contributions you made (number of commits sent, number of issues created/closed, etc.), it also publicly shows where you've contributed. So if you keep all of your code on GitHub, you're writing your CV as you code :)

Here's my contribution score:
![1024 is a cool number](http://i.imgur.com/AFJzy1G.png)

It may seem like much for someone just starting, but I've seen people with more than 10K... :)

## Now what?
Like I've said previously, the goal of this challenge is to give you the chance of contributing to this repository and fixing spelling errors. Can you create a pull request fixing a single spelling mistake and tag me as a reviewer?
