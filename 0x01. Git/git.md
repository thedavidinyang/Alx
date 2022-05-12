Setting your Git username for every repository on your computer
Open Terminal.

Set a Git username:

$ git config --global user.name "Mona Lisa"
Confirm that you have set the Git username correctly:

$ git config --global user.name
> Mona Lisa
Setting your Git username for a single repository
Open Terminal.

Change the current working directory to the local repository where you want to configure the name that is associated with your Git commits.

Set a Git username:

$ git config user.name "Mona Lisa"
Confirm that you have set the Git username correctly:

$ git config user.name
> Mona Lisa



Setting your commit email address in Git
You can use the git config command to change the email address you associate with your Git commits. The new email address you set will be visible in any future commits you push to GitHub.com from the command line. Any commits you made prior to changing your commit email address are still associated with your previous email address.

Setting your email address for every repository on your computer
Open Terminal.
Set an email address in Git. You can use your GitHub-provided no-reply email address or any email address.
$ git config --global user.email "email@example.com"
Confirm that you have set the email address correctly in Git:
$ git config --global user.email
email@example.com
Add the email address to your account on GitHub, so that your commits are attributed to you and appear in your contributions graph. For more information, see "Adding an email address to your GitHub account."
Setting your email address for a single repository
GitHub uses the email address set in your local Git configuration to associate commits pushed from the command line with your account on GitHub.com.

You can change the email address associated with commits you make in a single repository. This will override your global Git configuration settings in this one repository, but will not affect any other repositories.

Open Terminal.
Change the current working directory to the local repository where you want to configure the email address that you associate with your Git commits.
Set an email address in Git. You can use your GitHub-provided no-reply email address or any email address.
$ git config user.email "email@example.com"
Confirm that you have set the email address correctly in Git:
$ git config user.email
email@example.com
Add the email address to your account on GitHub, so that your commits are attributed to you and appear in your contributions graph. For more information, see "Adding an email address to your GitHub account."


