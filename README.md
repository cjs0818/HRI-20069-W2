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
Git supports two types of tags: lightweight and annotated.
A lightweight tag is very much like a branch that doesn’t change — it’s just a pointer to a specific
commit.
Annotated tags, however, are stored as full objects in the Git database.

  ##### Anotated Tags
  Creating an annotated tag in Git is simple. The easiest way is to specify -a when you run the tag command:
  
  ```
  $ git tag -a v1.4 -m "my version 1.4"
  $ git tag
  v0.1
  v1.3
  v1.4
  ```
The -m specifies a tagging message, which is stored with the tag. If you don’t specify a message for an annotated tag, Git launches your editor so you can type it in.

  ##### Lightweight Tags
  Another way to tag commits is with a lightweight tag. This is basically the commit checksum stored in a file — no other information is kept. To create a lightweight tag, don’t supply any of the -a, -s, or -m options, just provide a tag name:
  
  ```
  $ git tag v1.4-lw
  $ git tag
  v0.1
  v1.3
  v1.4
  v1.4-lw
  v1.5
  ```

  ##### Show Tags
  You can see the tag data along with the commit that was tagged by using the git show command:
  
  ```
  $ git show v1.4
  tag v1.4
  Tagger: Ben Straub <ben@straub.cc>
  Date:   Sat May 3 20:19:12 2014 -0700
  my version 1.4
  commit ca82a6dff817ec66f44342007202690a93763949
  Author: Scott Chacon <schacon@gee-mail.com>
  Date:   Mon Mar 17 21:52:11 2008 -0700
      changed the version number
  ```
  
  ##### Sharing Tags
  By default, the git push command doesn’t transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them. This process is just like sharing remote branches — you can run git push origin <tagname>.
  ```
  $ git push origin v1.5
  Counting objects: 14, done.
  Delta compression using up to 8 threads.
  Compressing objects: 100% (12/12), done.
  Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
  Total 14 (delta 3), reused 0 (delta 0)
  To git@github.com:schacon/simplegit.git
   * [new tag]         v1.5 -> v1.5
  ```
  If you have a lot of tags that you want to push up at once, you can also use the --tags option to the git push command. This will transfer all of your tags to the remote server that are not already there.
  ```
  $ git push origin --tags
  Counting objects: 1, done.
  Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
  Total 1 (delta 0), reused 0 (delta 0)
  To git@github.com:schacon/simplegit.git
   * [new tag]         v1.4 -> v1.4
   * [new tag]         v1.4-lw -> v1.4-lw
  ```
  ##### Checking out Tags

#### Git Aliases
  ```
  $ git config --global alias.co checkout
  $ git config --global alias.br branch
  $ git config --global alias.ci commit
  $ git config --global alias.st status
  ```


### Git Branching
 #### Creating a New Branch
  ```
  $ git branch testing
  ```
![pic-W2-003](./assets/images/two-branches.png)
  
How does Git know what branch you’re currently on? It keeps a special pointer called HEAD. In Git, this is a pointer to the local branch you’re currently on. In this case, you’re still on master. The git branch command only created a new branch — it didn’t switch to that branch.

![pic-W2-004](./assets/images/head-to-master.png)

### Git on the Server
 #### The Protocols
 ```
 $ git clone /path/to/git_project_in_local/project_name.git
 $ git clone http://github.com/your_ID/project_name.git
 $ git clone git@github.com:your_ID/project_name.git        # $ ssh-keygen, then ~/.ssh/id_rsa.pub needs to be copied to github (Settings)
 ```
![pic-W2-006](./assets/images/git_structure_01.png)

### Distributed Git
There several kinds of distributed workflows

 * Centralized Workflow
 * Integration-Manager Workflow
 * Dictator & Lieutenants Workflow
 * ...


 #### 1. Centralized Workflow
 In centralized systems, there is generally a single collaboration model — the centralized workflow. One central hub, or repository, can accept code, and everyone synchronizes their work to it. A number of developers are nodes — consumers of that hub — and synchronize to that one place.
![pic-W2-005](./assets/images/centralized_workflow.png  "Centralized Workflow")


 #### 2. Integration-Manager Workflow
 Because Git allows you to have multiple remote repositories, it’s possible to have a workflow where each developer has write access to their own public repository and read access to everyone else’s.
![pic-W2-006](./assets/images/integration-manager.png)

The process works as follows (see Integration- manager workflow.):
   1. The project maintainer pushes to their public repository.
   2. A contributor clones that repository and makes changes.
   3. The contributor pushes to their own public copy.
   4. The contributor sends the maintainer an email asking them to pull changes.
   5. The maintainer adds the contributor’s repository as a remote and merges locally. 
   6. The maintainer pushes merged changes to the main repository.

![pic-W2-006](./assets/images/Git_StorageDataFlow.png)


 #### 3. Dictator & Lieutenants Workflow
This is a variant of a multiple-repository workflow. It’s generally used by huge projects with hundreds of collaborators; one famous example is the Linux kernel. Various integration managers are in charge of certain parts of the repository; they’re called lieutenants. All the lieutenants have one integration manager known as the benevolent dictator. The benevolent dictator pushes from his directory to a reference repository from which all the collaborators need to pull. The process works like this:
1. Regular developers work on their topic branch and rebase their work on top of master. The master branch is that of the reference directory to which the dictator pushes.
2. Lieutenants merge the developers' topic branches into their master branch.
3. The dictator merges the lieutenants' master branches into the dictator’s master branch.
4. Finally, the dictator pushes that master branch to the reference repository so the other developers can rebase on it.

![pic-W2-007](./assets/images/benevolent-dictator.png)

### GitHub

### Git Tools
