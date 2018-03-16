# HRI-20069: Introduction to S/W developmental tools & perception technologies 

Linux Laptop required!!!

## Week 2: Git (Version Control)

### Install git & sign up for github.com
In Ubuntu 16.04, git is already included, but for the other OS please refer to https://git-scm.com

  * References:
    * https://git-scm.com/book/en/v2
    * https://opentutorials.org/course/2708

### First-Time Git Setup
  * Configure the git
    ** Your Identity
    ```
    $ git config --global user.email "you@example.com”  
    $ git config --global user.name "Your Name"
    ```   
    ** Your Editor
    ```
    $ git config --global push.default simple
    $ git config --global core.editor vi           # Using vi editor for git
    ``` 
    ** Checking Your Settings
    ```
    $ git config -l
    user.name=John Doe
    user.email=johndoe@example.com
    color.status=auto
    color.branch=auto
    color.interactive=auto
    color.diff=auto
    ...
    ```

### Git Basics
Git has three main states that your files can reside in: committed, modified, and staged:

    * Committed means that the data is safely stored in your local database.

    * Modified means that you have changed the file but have not committed it to your database yet.

    * Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

This leads us to the three main sections of a Git project: the Git directory, the working tree, and the staging area.

![pic-W2-001](./assets/images/areas.png)

You typically obtain a Git repository in one of two ways:
  1. Initializing a repository in an existing directory, or
  2. Cloning an existing Git repository from elsewhere.
In either case, you end up with a Git repository on your local machine, ready for work.

#### Initializing a Repository in an Existing Directory

  * First, make a folder (a git repository)
  ```
    $ mkdir hri-20069-git
  ```

  * Initialize the repository,
  ```
    $ cd hri-20069-git
    $ git init
  ```

  * Let's make several files as
  ``` 
    $ echo "test1: v01" > test1.txt
    $ echo "test2: v01" > test2.txt
  ```
  
  * Add all files to git stage
  ```
    $ git add .
  ```
  
  * Commit the staged files
  ```
    $ git commit -m 'v01'
  ```

#### Cloning an Existing Repository
You clone a repository with git clone <url>. For example, if you want to clone the Git for this class called HRI-20069 , you can do so like this:
 
  ```
    $ git clone https://github.com/cjs0818/HRI-20069
  ```
If you want to clone the repository into a directory named something other than HRI-20069, you can specify that as the next command-line option:

  ```
    $ git clone https://github.com/cjs0818/HRI-20069 myHRI
  ```

#### Recording Changes to the Repository
As you edit files, Git sees them as modified, because you’ve changed them since your last commit. As you work, you selectively stage these modified files and then commit all those staged changes, and the cycle repeats.

![pic-W2-002](./assets/images/lifecycle.png)

#### Checking the Status of Your Files
  ```
    $ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    nothing to commit, working directory clean
  ```

#### Working with Remotes
  ##### Showing Your Remotes
To see which remote servers you have configured, you can run the git remote command. It lists the shortnames of each remote handle you’ve specified. If you’ve cloned your repository, you should at least see origin — that is the default name Git gives to the server you cloned from:

  ```
  $ git clone https://github.com/schacon/ticgit
  Cloning into 'ticgit'...
  remote: Reusing existing pack: 1857, done.
  remote: Total 1857 (delta 0), reused 0 (delta 0)
  Receiving objects: 100% (1857/1857), 374.35 KiB | 268.00 KiB/s, done.
  Resolving deltas: 100% (772/772), done.
  Checking connectivity... done.
  $ cd ticgit
  $ git remote
  origin
  ```
  
You can also specify -v, which shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote:

  ```
  $ git remote -v
  origin  https://github.com/schacon/ticgit (fetch)
  origin  https://github.com/schacon/ticgit (push)
  ```

If you have more than one remote, the command lists them all. For example, a repository with multiple remotes for working with several collaborators might look something like this.

  ```
 $ cd grit
 $ git remote -v
  bakkdoor  https://github.com/bakkdoor/grit (fetch)
  bakkdoor  https://github.com/bakkdoor/grit (push)
  cho45     https://github.com/cho45/grit (fetch)
  cho45     https://github.com/cho45/grit (push)
  defunkt   https://github.com/defunkt/grit (fetch)
  defunkt   https://github.com/defunkt/grit (push)
  koke      git://github.com/koke/grit.git (fetch)
  koke      git://github.com/koke/grit.git (push)
  origin    git@github.com:mojombo/grit.git (fetch)
  origin    git@github.com:mojombo/grit.git (push)
  ```

This means we can pull contributions from any of these users pretty easily. We may additionally have permission to push to one or more of these, though we can’t tell that here.

  #### Adding Remote Repositories
We’ve mentioned and given some demonstrations of how the git clone command implicitly adds the origin remote for you. Here’s how to add a new remote explicitly. To add a new remote Git repository as a shortname you can reference easily, run git remote add <shortname> <url>:
 
  ```
  $ git remote
  origin
  $ git remote add pb https://github.com/paulboone/ticgit
  $ git remote -v
  origin  https://github.com/schacon/ticgit (fetch)
  origin  https://github.com/schacon/ticgit (push)
  pb  https://github.com/paulboone/ticgit (fetch)
  pb  https://github.com/paulboone/ticgit (push)
  ```

Now you can use the string pb on the command line in lieu of the whole URL. For example, if you want to fetch all the information that Paul has but that you don’t yet have in your repository, you can run git fetch pb:
 
  ```
  $ git fetch pb
  remote: Counting objects: 43, done.
  remote: Compressing objects: 100% (36/36), done.
  remote: Total 43 (delta 10), reused 31 (delta 5)
  Unpacking objects: 100% (43/43), done.
  From https://github.com/paulboone/ticgit
   * [new branch]      master     -> pb/master
   * [new branch]      ticgit     -> pb/ticgit
  ```

Paul’s master branch is now accessible locally as pb/master — you can merge it into one of your branches, or you can check out a local branch at that point if you want to inspect it. 

#### Fetching and Pulling from Your Remotes
As you just saw, to get data from your remote projects, you can run:

  ```
  $ git fetch <remote>
  ```
  cf.) 'git pull' means fetch and merge.

#### Pushing to Your Remotes
When you have your project at a point that you want to share, you have to push it upstream. The command for this is simple: git push <remote> <branch>. If you want to push your master branch to your origin server (again, cloning generally sets up both of those names for you automatically), then you can run this to push any commits you’ve done back up to the server:
 
  ```
  $ git push origin master
  ```

This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime. If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You’ll have to fetch their work first and incorporate it into yours before you’ll be allowed to push.

#### Inspecting a Remote
If you want to see more information about a particular remote, you can use the git remote show <remote> command. If you run this command with a particular shortname, such as origin, you get something like this:

  ```
  $ git remote show origin
  * remote origin
    Fetch URL: https://github.com/schacon/ticgit
    Push  URL: https://github.com/schacon/ticgit
    HEAD branch: master
    Remote branches:
      master                               tracked
      dev-branch                           tracked
    Local branch configured for 'git pull':
      master merges with remote master
    Local ref configured for 'git push':
      master pushes to master (up to date)
  ```

#### Renaming and Removing Remotes
You can run git remote rename to change a remote’s shortname. For instance, if you want to rename pb to paul, you can do so with git remote rename:

  ```
  $ git remote rename pb paul
  $ git remote
  origin
  paul
  ```

It’s worth mentioning that this changes all your remote-tracking branch names, too. What used to be referenced at pb/master is now at paul/master.
If you want to remove a remote for some reason — you’ve moved the server or are no longer using a particular mirror, or perhaps a contributor isn’t contributing anymore — you can either use git remote remove or git remote rm:

  ```
  $ git remote remove paul
  $ git remote
  origin
  ```

Once you delete the reference to a remote this way, all remote-tracking branches and configuration settings associated with that remote are also deleted.

#### Tagging

#### Git Aliases



### Git Branching

### Git on the Server

### Distributed Git

### GitHub

### Git Tools

### Version control for Dockerfile using git
  * ros-kinetic-core
  * ros-kinetic-base
  * ...
  * ros-kinetic-desktop-full
