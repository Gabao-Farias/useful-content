There was a situation that I needed to bring a commit that would be intersting to have in another repo wich was pretty similar to the current one. And for these kind of problems, the best thing to do is a patch, wich saves the changes from a specific hash or more and save them into a .patch file and later you can use this file to add these changes in another repo. So let's see how it works!

## First things first

`git format-patch -0 <sha>`

This is the command and the parameters are:
* `-0`: how many commits you want to add in patch (it start counting from HEAD if no sha was specified);
* `<sha>`: here you insert a specific commit that you want to add instead of HEAD.

## Hands on
  * Use the command as you wish, in my case, I just wanted to retrieve the changes from the last pull request made on another repo, and push it into master of my current branch. So I moved to master branch from the old repo and there used:

`git format-patch -1`

  <div align="center">
    <img src="afew3" />
  </div>

  * A patch file will be generated showing all changes made on last commit.

  * After that you can copy and paste this file into the target repo.

  * Now on the target repo you must run `git apply <FILE_NAME.patch>`.

    * If there are conflits, or you receive a message saying: `"git: patch does not apply"` , you can use `git --reject --whitespace=fix apply <FILE_NAME.patch>`.
      * `--reject` is used to continue over merge rejection and to create .rej files showing wich diffs couldn't be applied, and with these files you can handle the merge manually.

      * `--whitespace=fix` is used to warn about whitespaces instead of blocking the applying operation.

  * With all the files solved and changed, we can proceed commiting those changes and pushing to desired repository!
