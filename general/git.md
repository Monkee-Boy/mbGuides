# Git Standards

> **Fleeting Tip**: Check out [github.com/fleeting/dotfiles](https://github.com/jamesfleeting/dotfiles) for some awesome git .files including a great default .gitconfig and .gitignore.

## Commit Often
The most important thing to remember when working on a project is to commit often. Don't spend hours or even days coding and then make a commit. This makes it much harder to look back over commits, revert if needed and diff commits are basically useless.

A good rule of thumb is commit after you do anything. If you update jQuery in the project then make a commit to mark that update. You don't need to commit after every line change so use your judgement. If you are making changes to calendar and the contact form then be sure and commit your calendar changes before moving on to your contact form changes.

Always remember to attach a commit message to every single commit and be as descriptive as possible in what was done in that commit. This helps a lot with diff, reverting and overall review of the code and commits.

```
git commit -a -m "Updated jQuery to v2.0."
```

Git allows you to add multiple commit messages. You want to keep the first one short and to the point. The second can be more of a description if it is needed.

```
git commit -a -m "Refactoring calendar plugin." -m "Removed duplicated functions in controller, added more descriptive comments, fixed SQL query on edit, and added caching."
```

If using Github and a commit fixes an issue then tag that commit message with the issue number as that will attach the commit to the issue for better tracking of code changes and the progress of the code base. I advise doing this the same for our Zendesk tickets and Beanstalk, just for reference.

```
git commit -a -m "fixes inability to log in [Fixes #123]"
```

## Use Branches for Development

Do not do development on the `master` branch. This branch should always be considered stable and in most cases what is currently live. It is always best to branch off and keep dev code in the new branch and only merge to master after it has been tested and ready to be pushed to production.

One method of branching is to use a different branch for every major change. If you are rewriting the calendar plugin in mbCMS then a branch of `v2-calendar` might be best. You would most likely also have a `version2` branch which will contain all v2 changes. This allows you to continue development on the calendar rewrite while still pushing and merging changes into the v2 branch. This way if you make a fix on `version2` and need to commit then you won't push the incomplete calendar changes.

Of course the method of branching you use will depend on the project and the versioning used. However, avoiding using `master` for development is still important.

**This is still valid when working solo on a project!**

For more information: <a href="http://progit.org/book/ch3-2.html" title="Pro Git - Basic Branching and Merging">http://progit.org/book/ch3-2.html</a>

## Make Use of Tags
Git lets you tag your code with a version. Make use of this not only in Github related projects but also on client projects in beanstalk. Tag the project when it enters production and goes live. Then if you have a handful of changes to make that result in several commits, when those commits are ready to be pushed tag it with a new version. This will help in knowing which changes were made to the live website and when they were pushed into production.

Rule of thumb is to tag a version every time you push to production.

For more information: <a href="http://gitref.org/branching/#tag" title="Git Reference - Tag">http://gitref.org/branching/#tag</a>

# Git Resources

Below are several awesome git resources that are worth bookmarking.

### Books, Articles, and Guides

* <a href="http://rogerdudler.github.com/git-guide/" title="git - the simple guide">http://rogerdudler.github.com/git-guide/</a>
* <a href="http://book.git-scm.com/" title="git community book">http://book.git-scm.com/</a>
* <a href="http://integralist.co.uk/post/3551693739/how-to-use-git-and-github" title="How to use Git and GitHub">http://integralist.co.uk/post/3551693739/how-to-use-git-and-github</a>
* <a href="http://gitref.org/" title="Git Reference">http://gitref.org/</a>
* <a href="http://progit.org/" title="Pro Git">http://progit.org/</a>
* <a href="http://gitready.com/" title="git ready">http://gitready.com/</a>
* <a href="http://help.github.com/git-cheat-sheets/" title="Git Cheat Sheets">http://help.github.com/git-cheat-sheets/</a>
* <a href="http://sandofsky.com/blog/git-workflow.html" title="Understanding the Git Workflow">http://sandofsky.com/blog/git-workflow.html</a>
* <a href="http://www.ndpsoftware.com/git-cheatsheet.html" title="Git Cheatsheet">http://www.ndpsoftware.com/git-cheatsheet.html</a>

### GUI Apps

* <a href="http://www.git-tower.com/" title="Tower Git App">http://www.git-tower.com/</a>
* <a href="http://www.sourcetreeapp.com/" title="SourceTree Git App">http://www.sourcetreeapp.com/</a>
* <a href="http://mac.github.com/" title="GitHub for Mac">http://mac.github.com/</a>
* <a href="http://gitx.frim.nl/" title="GitX">http://gitx.frim.nl/</a>
* <a href="http://gitboxapp.com/" title="GitBox App">http://gitboxapp.com/</a>
