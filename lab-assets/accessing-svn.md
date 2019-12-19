# Accessing SVN

_SBEL stores many of its internal files for papers, presentations, and such in an svn repository. Subversion, or svn, is a version control system similar in many ways to git. The main difference between the two is that svn allows users to checkout portions of the repository file tree._

#### Getting Access to the Repo
* You must have a CAE login. If you do not have a CAE login, ask Dan to email the CAE helpdesk to have them set up an account for you.
* Once you have a login, Dan should add you to the sbel group. At this point, you should have access to read and write the repo.

#### Checking Out a Local Copy
The repo is located [here](https://subversion.cae.wisc.edu/svn/sbel/). The repo is 56GB as of December 2019, so you should not clone the entire thing, but rather only the files that you need.
* In a browser, log in with your CAE login
* Traverse the file tree until you find the file or directory that you need.
* From the command line, checkout the *each* directory that you need:\
`svn checkout https://subversion.cae.wisc.edu/svn/sbel/path/to/directory`

#### Typical Uses
* Check the status of files: Check the status of the repo periodically, especially right before a commit. `svn status`
* Update files: As other people commit changes to the central remote repo, you should update your local copy. This updates your local copy of the files *in the subdirectory from which you run the update*. Do this frequently, especially when working on files that are being used by multiple people and before you commit. `svn update`
* Add a new file: To begin tracking a new file run `svn add newfile.txt`
* Modify an existing tracked file: Files that are already tracked are automatically watched for modifications and will be recorded when you commit.
* Commit changes: This varies from git. In svn terminology, a commit is essentially `git commit` and `git push` together. When you commit, all files *in the subtree from which you commit* that you have `svn add`-ed and all previously tracked files that you have modified are sent uploaded to the central remote repo so that others can see them. `svn commit -m "my commit message"`

#### Conflict Resolution
If you and someone else make changes to the same file at the same time, you may get a conflict when you commit or update. This occurs when svn is unable to automatically merge together your changes. When you encounter a conflict, `svn status` will mark the conflicting file with a 'C'. You will have to manually sort out how to rectify the two conflicting sets of changes.

You have two main options:
* Throw away your local changes entirely with `svn revert conflictfile.txt`
* Manually edit the file to choose which parts you want from each version. Conflicting sections will show both versions of that section, yours and theirs:
```
<<<<<<< .mine
your content
=======
their content
>>>>>>> .rREVNUM
```
Manually edit the file to choose one version or a combination of them and remove the markings left by svn. Do this for all such sections in the conlicting file. Once you are done, mark the file as resolved: `svn resolved conflictfile.txt`

Once all conflicts in your local repo copy have been resolved, commit the changes which fixed the conflict with `svn commit -m "my commit message about resolution"`

This process will likely leave some untracked files with suffixes after the names of conflicted files. Feel free to remove these untracked files after you have successfully resolved your conflicts and committed.

#### Troubleshooting
* `svn help` and `svn help <subcommand>` will give the help pages should for svn, should you need anything outside of the funcality listed here.