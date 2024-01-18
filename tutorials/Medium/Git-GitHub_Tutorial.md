# Tutorials From KillrKoda

## Topics

------

1. Install _git_ on Ubuntu
   * Check if it is installed:
     * ``dpkg -l | grep git``
     * ``apt list git -a``
     * ``apt-cache pkgnames git``
     * ``git``
   * Install _git_:
     * ``apt install -y git``
   * Check if it is installed:
     * ``git --version``

2. Configure _git_
   * Some required tags:
     * ``--system`` &rarr; table relevant for the whole machine
     * ``--global`` &rarr; for the current user
     * ``--local``  &rarr; (default) for the current repository
**Note: Create new dir and use ``git init``**

   * Make some entries to the config:
     * ``git config --local user.name "baba yega"``
     * ``git config --local user.email babayega@myemail.com``
**Note: ``--global`` configs will be overwritten by ``--local``**

   * List all the configuration:
     * ``git config --list``
     * ``git config --list --global`` &rarr; list global confs only.
     * ``git config user.name``

   * Config the repo:
     * ``cd .git/ && ll`` &rarr; take a look of git tree
     * ``cd .git/ and tree`` will have following tree structure;

   * Nice to Have Configurations:
     * ``git config -- global color.status auto``
     * ``git config --global color.branch auto``
     * ``git config --global color.interactive auto``
     * ``git config --global color.diff auto``
     * ``git config --global alias.adog "log --all --decorate --oneline --graph"``
     * ``git add . && git commit -m <commit_message>``
     * ``git adog``

3. Commiting the first files
   * Initialize the Repository
     * ``mkdir test-repo``
     * ``cd test-repo``
     * ``ls -al``
     * ``git init``
     * ``git status``
     * ``ls -al``
     * ``touch newfile && echo hello > newfile``
        * ``git status``  &rarr; untracked file
   * Adding to the Staging Area
        * ``git add newfile``
        * ``git status``
   * First Commit
        * ``git commit newfile -m "my first commit"``

4. Remove File from _commit_
   * Sometimes we decide to not continue some work. We have some "brutal" ways of cleaning the repository, but let's see first, how to do it nicely.

   * Create a file directory multiple files add to stage
     * ``git rm --cached file-01``
     * ``git status``
     * If we have more files, we need to remove them recursively.
     * ``git rm --cached -r .``
     * ``git status`` &rarr; * -f has unstaged
     * ``git checkout testfile-01``

5. Visual _commit_
6. Revert Changes
7. Check the Differences
8. Detailed Information About Previous _commits_
9. Conflicts
10. Stash
11. .gitignore
12. _git_ Tags
13. Merge
14. Cheat the history ???

## GitHub Tutorial

1. Connect Local Git Repository to Remote
   * [Connect with SSH](https://www.atlassian.com/git/tutorials/git-ssh)
   * Connect with Https
