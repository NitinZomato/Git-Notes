## Git Notes

> #### Frequently used commands for quick access

1. **Update the Existing Remote's URL**  
`git remote set-url <REMOTE-NAME> <NEW-URL>`  
**e.g** `git remote set-url origin https://github.com/Zomato/Android`

2. **Clone repository in a folder from remote**
* First of all create folder and go into that folder using `cd` command
* Then clone here using command `git clone <url>`

3. To find out what branches are available and what the current branch name is execute `git branch`  

4. **Create and Do Switching between Branches :**
* `git checkout -b <new branch-name>` [ The **`git checkout`** command accepts a **`-b`** argument that acts as a convenience method which will create the new branch and immediately switch to it.]

* `git checkout <existing branch-name>` [ Switching branches is a straightforward operation. Executing the following will point **`HEAD`** to the tip of **`＜branchname＞`**.]

* `git checkout -b ＜new-branch＞ ＜existing-branch＞` [ By default **`git checkout -b`** will base the **`new-branch`** off the current **`HEAD`**. An optional additional branch parameter can be passed to **`git checkout`**. In the above example, **`＜existing-branch＞`** is passed which then bases **`new-branch`** off of **`existing-branch`** instead of the current **`HEAD`**.]

* `git reflog` [Git tracks a history of checkout operations in the reflog]

5. **Git Stash Commands** - git stash temporarily shelves (or stashes) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on.
* **Create Stash**
  * `git stash` : changes saved with random name/stash created with random name.
  * `git stash -m "message for this stash"` : changes saved with a given name/message.
* **Show Stash**
  * `git stash list` : Get the list of all stash.
  * `git stash show` : shows the summary of the latest stash diffs.
  * `git stash show -p` : shows the summary of the latest stash full diffs.
  * `git stash show stash@{1}` : shows the summary of the specific stash diffs.
* **Apply Stash**
  * `git stash apply` : Apply latest/most recent changes to your work.
  * `git stash apply stash@{3}` : Apply specific stash changes to your work.
* **Delete Stash**
  * `git stash drop` : Delete the most recent stash.
  * `git stash drop stash@{1}` : Delete a specific stash.
  * `git stash clear` : Delete all stashes.
* **Apply and Delete Stash Simultaneously**  
  * `git stash pop` : Take the content from the latest stash and then apply those changes to our current working file, and remove that topmost stash. This command is very similar to stash apply but it deletes the stash from the stack after it is applied.
  * `git stash pop stash@{1}` : same as git stash pop but for specific stash id.   
* **Create Branch From Stash**
  * `git stash branch <branch_name>` : creates a new branch with the latest stash, and then deletes the latest stash (like stash pop).
  * `git stash branch <branch_name> stash@{1}` : creates a new branch with the specific stash, and then delete that specific stash.

6. `git merge` **Vs** `git rebase`  [[visual explanation](https://www.youtube.com/watch?v=BoXAv9M4boU)]
* `git merge` - It create new commit in `main branch` after combining commits of `new branch` and `main branch`.
* `git rebase` - Rebasing is the process of moving or combining a `sequence of commits` to a new base commit.
* `git rebase --abort` - Run this to completely undo the rebase. Git will return you to your branch's state as it was before git rebase was called.  
<img width="380" src="https://user-images.githubusercontent.com/122450528/219931120-79ce2aba-849f-412f-a1fb-f399e1a12bd1.png"> - <img width="380"  src="https://user-images.githubusercontent.com/122450528/219931369-f05c02b1-0547-4495-8fe4-a2c31eed22cf.png">



7. `git fetch` **Vs** `git pull`  [[simple video](https://www.youtube.com/watch?v=KmagW60Li-o)]
* `git pull` - Used to fetch and download content from a remote repository and immediately update the local repository to match that content  
* `git fetch` - just used to check that there are any changes available, if yes then download latest changes using `git merge`
* `git pull = git fetch + git merge`  
  <img width="350" src="https://user-images.githubusercontent.com/122450528/219922638-d3912aab-21c0-4643-b74f-1afb06257197.png">
  
8. `git log` - Used to view the history of committed changes within a Git repository.
9. `git push` - Used to upload local repository content to a remote repository.
10. `git remote -v` - It will list the URL of the remote repo.
11. `git log <branch_name> --oneline` - Only show commits of current branch.

12. **List all the committed files that are going to push to the remote repository**  
**P.S** The `git status` didn’t show the committed files.

- `git log` to display all the commit_id, the first one is the last commit_id, copy it
- `git show commit_id --name-only` to display all the files committed in the specified commit_id
- Undo the last commit with `git reset --soft HEAD~1`, move the mistakenly committed files back to the staging area

13. **How to Delete a Git Branch Both Locally and Remotely**
* **Steps to Delete Locally**
  * Git will not let you delete the branch you are currently on so you must make sure to **checkout** a branch that you are **NOT** deleting. For example: `git checkout development`
  * Delete a branch : `git branch -d <branch_name>`
  * The `-d` option will delete the branch only if it has already been pushed and merged with the remote branch. 
  * Use `-D` instead if you want to force the branch to be deleted, even if it hasn't been pushed or merged yet.
  * The branch is now deleted locally.
* **Steps to Delete Remotely**
  * Command to delete a branch remotely : `git push <remote> --delete <branch_name>` [remote = origin]

14. **Rename Git Branch Locally and Remotely**
* **STEP-1 : Rename the local branch**
  * First of all switch to the local branch which you want to rename : `git checkout <old_name>`
  * Rename the local branch using command : `git branch -m <new_name>`
  * OR without switching to target branch you can use : `git branch -m <old_branch_name> <new_branch_name>`
* **STEP-2 : Rename the Remote Branch**   
  * If you have renamed the local branch, and you’ve already pushed the <old_name> branch to the remote repository ,perform the next steps to rename the remote branch.
    * Push the <new_name> local branch and reset the upstream branch : `git push origin -u <new_name>`
    * Delete the <old_name> remote branch : `git push origin --delete <old_name>`
    * OR directly you can use : `git push origin :<old_branch_name> <new_branch_name>`
  * DONE ! That’s it. You have successfully renamed the local and remote Git branch.

15. **Checkout Git Tag**
* First of all fetch all tags using command : `git fetch`
* In order to checkout a Git tag, use the **git checkout** command and specify the _tagname_ as well as the _branch_ to be checked out.
  * `git checkout tags/<tag_name> -b <branch_name>`
  * e.g - `git checkout tags/v17.3.5 -b release/v17.3.5`
* you have successfully checked out the “v17.3.5” tag

16. Merging Abort : `git merge --abort`

➡️ [simplest and visual explanation of Git commands](https://www.atlassian.com/git/tutorials/setting-up-a-repository) 

##

> #### Project Setup [23 Jan, 2023]

* [HomeBrew Install](https://brew.sh/)
* Install git using brew - `brew install git`
* `clone git (url)`
* [OH M ZSH](https://ohmyz.sh/)
* [Set Environment Variables for ZSH](https://linuxhint.com/set-environment-variable-zsh/)

##

> #### Steps for setting up SSH key for your github account [To avoid authentication everytime while pushing to remote repo]
1. ssh-keygen -t ed25519 -C "mygithub@org.com"
2. No need to enter any passphrase, simply hit enter button.
3. Copy the SSH Key that is generated
4. `cat ./.ssh/id_ed25519.pub` you can use `cat` for printing your SSH Key which is stored in `pub` file.
5. After all these steps finally paste the SSH Key in your Github SSH Key and then everything done.

##

> #### Steps for pushing my branch changes to remote repo from Android Studio Terminal   
1. First of all create new branch from my developement branch in Android Studio.
2. `git remote set-url origin <repo-SSH link>`
3. `git status 🔴` [Track changes in modifies files, Unstaging area]
4. `git add .`   
5. `git status 🟢` [staging area]
6. `git restore --staged <file path>` [ **Note** : Only use when required to remove any file from staging area]
7. `git commit -m "message"` [After commit, modified files comes in staging area] 
8. `git status` [nothing to commit, working tree clean]
9. `git push origin <branch name>` [But before this setup SSH key for your github account]

##

> #### Steps for pushing my work by creating new branch
1. `git checkout -b <new branch name>`
2. `git status 🔴` [Track changes in modifies files, Unstaging area]
3. `git add .`  
4. `git status 🟢` 
5. `git commit -m "message"` [After commit, modified files comes in staging area] 
6. `git status` [nothing to commit, working tree clean]
7. `git push origin <new branch name that you have created earlier>` [But before this setup SSH key for your github account]

##

> #### Steps for resolving the conflicts arising in PR  
1. `git pull <origin> development` (Pull all changes from zomato development, use origin = git@github.com:Zomato/Android.git)
2. RESOLVE ALL CONFLICTS
3. `git merge --continue` (Use to commit all changes)
4. If some secrets found, then rollback those files, `e.g abc9.json`, and then again run command `git merge --continue`
5. `:wq` [write and quit]  

##

> #### Install 'Oh My ZSH' for Syntax-Highlighting and Auto-Suggestions  
1. Install [Oh My Zsh](https://ohmyz.sh/)
2. Install Oh My Zsh Via Curl `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
3. [Follow steps from here - Syntax-Highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)
4. [Follow steps from here - Auto-Suggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)
5. Use `nano ~/.zshrc` command to add both Plugin (i.e `zsh-syntax-highlighting`, `zsh-autosuggestions`) in file.
6. For Write Out press`Ctrl + O`
7. For exit press `Ctrl + X`

##

> #### Method-1 : How to Setup Charles in Android [Recommended]  
1. Open `Zeus` from `zomato debug app` and enable `Charles-proxy`
2. Enter `proxy hostname` : **Local IP Address** [ Get `local IP address` by clicking over `help` tab of charles]
3. Enter `Port` : **8888** 

> #### Method-2 : How to Setup Charles in Android   
1. Do manual setup in your phone, Go to Advanced settings of your wifi 
2. Set `proxy hostname` : **Local IP Address** [ Get `local IP address` by clicking over `help` tab of charles]
3. Set `Port` : **8888** 
4. Download `CA certificate` using chrome by visiting this link `chls.pro/ssl`, Or you can go to settings of your phone and download `CA Certificate`.

##

> #### Screenshot testing
1. Download [imagemagick](https://imagemagick.org/script/download.php) using commands to generate the report for changes happen in Screenshots.
2. Run command `brew install imagemagick`
3. Run command `brew install ghostscript`

##

> #### [How to Create and Delete Multiple Files and Directories at Once with a prefix name](https://trendoceans.com/create-multiple-files-and-directories/)
1. Open the Terminal.
2. First of all change the directory from/where you want to delete/create respectively, using command `cd <path_of_folder>` 
3. To **create** multiple files use command eg. `touch v2_image_text_snippet_type_{1..51}.json`
4. To **delete** multiple files use command eg.  
Note : (Type each line at a time and press enter)
``` 
for file in v2_image_text_snippet_type_*     
do
rm $file
done
```

##

> #### Don'ts ❌

* Resolve secret key error, files which has sensitive data, will be commited using  
`git commit -m "asfasg" --no-verify`
