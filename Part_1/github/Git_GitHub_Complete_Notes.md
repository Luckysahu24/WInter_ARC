# Git + GitHub Learning Notes

## Creating a Git Repository

--\> git init , Git creates a hidden: .git/

## Check Repository Status

--\> git status

## Staging

Tell Git which files you want in the next commit:

--\> git add file_name or git add . ( for all files)

## Commit

A commit is essentially a saved checkpoint.

--\> git commit -m "Add initial Message"

## Git's Three Important Areas

``` text
┌─────────────────────┐
│ Working Directory   │
│                     │
│ Your actual files   │
└──────────┬──────────┘
           │
        git add
           ↓
┌─────────────────────┐
│ Staging Area        │
│                     │
│ Files for next      │
│ commit              │
└──────────┬──────────┘
           │
       git commit
           ↓
┌─────────────────────┐
│ Git Repository      │
│                     │
│ Saved history       │
└─────────────────────┘
```

## View History

--\> git log

Or the compact version:

--\> git log --oneline

## .gitignore

.gitignore --\> Ignore the files and directory form being pushed into
the Repository

------------------------------------------------------------------------

# Branches

## What is a branch?

A branch is an independent line of development inside a Git repository.

main is your main/stable branch.

``` text
main
 │
 ●───●───●
         ↑
       latest
```

Instead of directly changing main, you create:

``` text
main
 │
 ●───●───●
         \
          ●───●───●
               ↑
          feature-login
```

## Checking Your Current Branch

``` bash
git branch
```

## Creating a Branch

``` bash
git branch feature-login
```

This creates the branch but does not switch to it.

## Switching to a Branch

Old/common command:

``` bash
git checkout feature-login
```

Modern command

Switching to a Branch:

``` bash
git switch feature-login
```

## Create + Switch in One Command

Create + Switch in One Command:

``` bash
git switch -c feature-login
```

``` text
main
 │
 ●───●
      \
       ●───●
            ↑
      feature-login
```

------------------------------------------------------------------------

# Merge

you have

main:

``` text
A ─── B ─── C
```

and

feature-login:

``` text
A ─── B ─── C ─── D ─── E
```

you want to bring your feature into main

## Important Rule

If you want to merge feature-login into main

you first switch to main : then

merge --\>

``` bash
git switch main
git merge feature-login
```

``` text
             feature-login
                  │
             D ─── E
                  │
                  ↓
main ─── A ─── B ─── C
                  │
                merge
                  ↓
             main contains
             feature-login
```

------------------------------------------------------------------------

# What does GITHUB Look LIKE ?

## GitHub Repository

``` text
main
 │
 ├── commits
 │
 └── stable code

feature-login
 │
 ├── commits
 │
 └── login development
```

## Pull Request

Pull Request : commonly called PR means : i've made changes in my branch
please review them and consider merging them into another branch

For example:

``` text
feature-login
      │
      │ Pull Request
      ↓
     main
```

A teammate can review your code.

They might:

-   comment
-   request changes
-   approve
-   merge

------------------------------------------------------------------------

# Merge Conflicts

A merge conflict happens when Git cannot automatically decide which
changes should be kept.

## What Does a Conflict Look Like?

Git may modify the file like this:

``` text
<<<<<<< HEAD
print("Hello NITK")
=======
print("Hello Laxminarayan")
>>>>>>> feature-login
```

\<\<\<\<\<\<\< The version from your current branch

======= Separator

> > > > > > > Incoming branch's version

## How Do You Resolve It?

You mannualy decide what final code should be

------------------------------------------------------------------------

# Collaboration Workflow

``` text
                 GitHub
                    │
                 main
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
   Laxminarayan    Jeny        Mahek
   feature-A      feature-B    feature-C
```

1.  clone main
2.  create your own branch make changes
3.  push in your branch
4.  create Pull request
5.  Once approved it wil be merged by the admin then in main git pull to
    get the local update

------------------------------------------------------------------------

# GITHUB --\> typicall Workflow

``` text
Create project
     ↓
python -m venv .venv
     ↓
Write Python code
     ↓
git init
     ↓
git add .
     ↓
git commit
     ↓
Create GitHub repository
     ↓
git remote add origin ...
     ↓
git push
```

## after that normal workflow

``` text
Modify code
    ↓
git status
    ↓
git add .
    ↓
git commit -m "message"
    ↓
git push
```

## git remote

git remote --\> Connects your local repository to GitHub

``` bash
git git remote add origin <repository-url>
```

Check :

``` bash
git remote -v
```

## Push

Push --\> local commits will be pushed with this commnads

``` bash
git push -u origin main
```

## Clone

Clone :Suppose a project already exists on GitHub and you want to
download

``` bash
git clone <repository-url>
```

## Pull

Pull : Suppose your teammate changed the GitHub repository.You want
those changes:

``` bash
git pull
```

``` text
GitHub
   ↓
git pull
   ↓
Your computer
```

## Push vs Pull

push = local → GitHub

pull = GitHub → local

------------------------------------------------------------------------

# The Complete Mental Model

``` text
                    GITHUB
                       ▲
                       │
                     push
                       │
              ┌────────┴────────┐
              │   Git Repository │
              │    (local)       │
              └────────▲────────┘
                       │
                    commit
                       │
              ┌────────┴────────┐
              │  Staging Area    │
              └────────▲────────┘
                       │
                     add
                       │
              ┌────────┴────────┐
              │ Working Directory│
              │                  │
              │ main.py          │
              │ requirements.txt │
              │ .gitignore       │
              └──────────────────┘
                       │
                       │
                     .venv
              ┌──────────────────┐
              │ Isolated Python  │
              │ Environment      │
              │                  │
              │ pandas           │
              │ numpy            │
              │ sklearn          │
              └──────────────────┘
```

------------------------------------------------------------------------

# Complete Collaboration Flow

``` text
                               GitHub
                    │
                    │ clone
                    ↓
              Local repository
                    │
                    ↓
                  main
                    │
                  pull
                    │
                    ↓
          Create feature branch
                    │
                    ↓
             Write your code
                    │
                    ↓
                git add
                    │
                    ↓
              git commit
                    │
                    ↓
                git push
                    │
                    ↓
              GitHub branch
                    │
                    ↓
             Pull Request
                    │
              ┌─────┴─────┐
              │           │
           Review       Conflict?
              │           │
              │      Resolve locally
              │           │
              └─────┬─────┘
                    ↓
                  Merge
                    ↓
                   main
                    │
                    ↓
              git pull
```

------------------------------------------------------------------------

# Delete the branch

Git normally won't delete the branch if it contains commits that haven't
been merged somewhere Git considers safely integrated.

``` bash
git branch -d feature-login
```

It does not necessarily delete the branch from GitHub.

To delete the remote GitHub branch:

``` bash
git push origin --delete feature-login
```

------------------------------------------------------------------------

# git diff

git diff: what exaclty did i change in my files?

``` bash
git diff
```

git diff --staged: what exaclty am i about to commit ?

``` bash
git diff --staged
```

------------------------------------------------------------------------

# git restore

git restore: Usefull when you make a mistake

``` bash
git restore filename.py
```

--\>can discard unstaged changes to that file.

``` bash
git restore --staged filename.py
```

--\> which removes a file from the stagging areas without deleting your
working copy.

------------------------------------------------------------------------

# Undoing commits

``` bash
git commit --amend
```

and

``` bash
git revert <commit>
```

------------------------------------------------------------------------

# Remote branches

Inspect remote branches

``` bash
git branch -r
```

Local:

``` text
main
feature-login
```

``` bash
git branch -a
```

Remote:

``` text
origin/main
origin/feature-login
```

------------------------------------------------------------------------

# Upstream / Tracking Relationship

in Git

``` bash
git push -u origin main
```

-u establishes an upstream/ tracking relationship

This means:

``` text
local main
     ↓
tracks
     ↓
origin/main
```

After this, you can generally use:

``` bash
git push
```

and:

``` bash
git pull
```

without specifying the remote and branch every time.

------------------------------------------------------------------------

# git commit --amend

Suppose you made a commit:

``` bash
git add .
git commit -m "Add login"
```

Then you realize:

"Oops, I forgot to include `login.css`."

You could create another commit:

``` bash
git add login.css
git commit -m "Add login CSS"
```

But if the CSS was supposed to be part of the previous commit, you can
use:

``` bash
git add login.css
git commit --amend
```

You can also change the commit message:

``` bash
git commit --amend -m "Add complete login feature"
```

Mental model:

``` text
Before:

A ─── B
      ↑
   Add login


After amend:

A ─── B'
      ↑
   Add complete
   login feature
```

Important:

`--amend` is safest when the commit has not already been pushed/shared.

If you've already pushed that commit to a shared branch, amending it
changes Git history and can create problems for teammates.

------------------------------------------------------------------------

# git fetch

You already know:

``` bash
git pull
```

Now learn:

``` bash
git fetch
```

Suppose GitHub has:

``` text
origin/main

A ─── B ─── C
```

but your local main is:

``` text
A ─── B
```

You run:

``` bash
git fetch
```

Git downloads information about the remote changes.

Conceptually:

``` text
GitHub
   │
   │ fetch
   ↓
Local Git knows about C
```

But your current files are not automatically changed by `git fetch`.

------------------------------------------------------------------------

# fetch vs pull

Think:

``` bash
git fetch
```

means:

"Tell me what changed on the remote."

While:

``` bash
git pull
```

roughly means:

"Get the remote changes and integrate them into my current branch."

A simplified mental model:

``` text
git pull
   =
git fetch
   +
integration
```

The exact integration behavior can involve merge or rebase depending on
configuration/options, so don't treat `pull` as literally always
"fetch + merge."

------------------------------------------------------------------------

# Why Would I Use fetch?

Imagine you're working on a project and don't want your local files
changed yet.

You can do:

``` bash
git fetch
```

Then inspect what's happening.

For example:

``` bash
git log main..origin/main
```

You can see commits that exist remotely but aren't in your local main.

Then decide what to do.

------------------------------------------------------------------------

# Remote Branches

You already have:

``` bash
git branch -r
```

This shows remote-tracking branches.

Example:

``` text
origin/main
origin/feature-login
origin/feature-payment
```

And:

``` bash
git branch -a
```

shows both local and remote-tracking branches.

For example:

``` text
* main
  feature-login

  remotes/origin/main
  remotes/origin/feature-login
```

A useful distinction:

``` text
main
↓
local branch


origin/main
↓
local reference to the remote-tracking state
```

Don't think of `origin/main` as another working directory on your
computer. It's Git's local record of the remote branch's state.

------------------------------------------------------------------------

# Pull Request Comments

Suppose you create:

``` text
feature-login
      ↓
     PR
      ↓
main
```

Your teammate reviews your code.

They might leave a comment:

"Can you validate the password length here?"

You modify the code:

``` bash
git add .
git commit -m "Add password validation"
git push
```

The existing PR automatically gets updated with your new pushed commits.

You don't normally create another PR for every change.

------------------------------------------------------------------------

# Request Changes

A reviewer can select:

Request changes

This means:

"I reviewed this PR, but I want modifications before it is merged."

You then make the requested changes and push them to the same branch.

``` text
PR
 ↓
Request changes
 ↓
Modify code
 ↓
commit
 ↓
push
 ↓
PR updated
 ↓
review again
```

------------------------------------------------------------------------

# Approve

A reviewer can approve your PR.

Conceptually:

``` text
Developer
    ↓
Pull Request
    ↓
Code Review
    ↓
Approve
    ↓
Merge
```

Approval itself does not necessarily mean the PR is merged.

Depending on the repository's rules, someone with appropriate
permissions may still need to merge it.

------------------------------------------------------------------------

# Merge the Pull Request

Once the requirements are satisfied:

``` text
feature-login
      ↓
     PR
      ↓
    review
      ↓
   approved
      ↓
    MERGE
      ↓
     main
```

Now the feature becomes part of the target branch.

------------------------------------------------------------------------

# Close a Pull Request

A PR can also be closed without merging.

For example:

``` text
feature-login
      ↓
     PR
      ↓
   decision
    ↙    ↘
 merge   close
```

Closing means:

"This PR will not be merged."

The branch itself may still exist.

Closing a PR and deleting a branch are separate actions.

------------------------------------------------------------------------

# Branch Protection

This is a very important professional concept.

Imagine a team repository:

``` text
main
```

contains production/stable code.

You don't want someone accidentally doing:

``` bash
git push origin main
```

and breaking the project.

GitHub can therefore have branch protection rules.

For example, the team can require:

``` text
main
 │
 ├── Pull Request required
 ├── Review required
 ├── Tests must pass
 └── Direct push restricted
```

Then developers are expected to do:

``` text
feature branch
      ↓
push
      ↓
Pull Request
      ↓
review
      ↓
tests
      ↓
merge
      ↓
main
```

rather than directly modifying `main`.

------------------------------------------------------------------------

# Why Restrict Direct Pushes to main?

Because main is often treated as a stable/integrated branch.

Without protection:

``` text
Developer A ────────┐
Developer B ────────┼──→ main
Developer C ────────┘
```

Someone could accidentally push broken code.

With a PR-based workflow:

``` text
Developer A → feature-A ──┐
                           │
Developer B → feature-B ──┼→ PR → Review → main
                           │
Developer C → feature-C ──┘
```

This gives the team a place to:

-   review code
-   discuss changes
-   run automated tests/checks
-   catch mistakes before integration

------------------------------------------------------------------------

# Complete Git Knowledge Map

``` text
                         GIT
                          │
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
     BASICS            BRANCHING        GITHUB
        │                 │                 │
   git init           branch            remote
   status             switch            clone
   add                merge             push
   commit             conflict          pull
   log                resolve           fetch
   diff                                 tracking
   restore
   amend
   revert
   .gitignore
        │                 │                 │
        └─────────────────┼─────────────────┘
                          ↓
                    COLLABORATION
                          │
                    Pull Request
                          │
              ┌───────────┼───────────┐
              ↓           ↓           ↓
           comment     review      approval
              │           │           │
              └───────────┼───────────┘
                          ↓
                        merge
                          │
                          ↓
                     main branch
                          │
                    branch protection
```

------------------------------------------------------------------------

# Notes / Questions Left

The remaining questions and concepts can be added below this section as
they come up.
