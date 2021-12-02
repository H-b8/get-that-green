### SHOWING A PAST PROJECT ON A NEW ACCOUNT

1. Clone your repo down from your old account, if not on your machine already
2. On GitHub: In your new account, create a new repository
3. In terminal: `cd` into your old project repo
4. Change its remote origin to that of your new repository that was created on your new account using `git remote set-url origin [PASTE SSH/HTTP HERE URL]`
5. Run `git remote -v` to check that it's correct
6. Now do your usual add, commit, and push
7. Check your new repo on GitHub to make sure it was pushed up

You can stop here if you want! This will show the project on your new account, but all commits will show that they are written by your other account. And therefor, you will not receive green activity squares on your profile page.

If your name is attached to your other account, there's no doubt that you were the one who wrote this code. You can pin it to your profile for people to see. And if you wanted, you could update the "About" section (on the right of your repo) to inform viewers that this was initially written by you from a different account.

To retroactively receive green activity squares, follow the next set of directions.

### REWRITING HISTORY (GETTING RETROACTIVE GREEN SQUARES)

*After doing above steps*, go back in your terminal. You should still be in your project folder

1. Run `git log`. You should see a history of your commits with the **Author** key displaying `your name <your old email>`. Take note of your old email here, we'll be using it later. Hit 'q' to get out
2. Copy this block of code into a text editor and change variables for OLD_EMAIL, NEW_NAME, and NEW_EMAIL on the second through fourth line. DO NOT TOUCH ANYTHING ELSE. (**NOTE:** If your email for your new account is the same as an old enterprise account, this is okay. Just set the same email for each variable anyways)

```
git filter-branch -f --env-filter '
OLD_EMAIL="the old account email you saw in git log"
NEW_NAME="the name you want displayed for these rewritten commits"
NEW_EMAIL="your new account email"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$NEW_NAME"
    export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$NEW_NAME"
    export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

3. Once you've edited the code to include your own info, paste it into your terminal, (making sure you're still in the right folder). 
4. Hit enter!
5. Run `git log` again to see that the changes have been made. Hit 'q' to get out
6. Run the command `git merge origin/master --allow-unrelated-histories`
7. Now do your usual add, commit, and push again

Your profile will now reflect that you made *a bunch* of commits today. But should now also show activity for past dates!

**ADDITIONAL INFO:** https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
