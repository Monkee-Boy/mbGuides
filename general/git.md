# Git ![Current Status](https://img.shields.io/badge/status-Approved-green.svg)

* Remember that you are never the only developer on a project. You might be coding solo to start with but at any point another developer could jump in.
* **This is the agreed upon style and it should be strictly enforced.**

> **Monkee Tip**: Check out [fleeting/dotfiles](https://github.com/jamesfleeting/dotfiles) for some awesome git .files including a great default .gitconfig and .gitignore. /selfpromotion

## Commits

The most important thing to remember when working on a project is to commit often. Don't spend hours or even days coding and then make a commit. This makes it much harder to look back over commits, revert if needed and diff commits are basically useless.

A good rule of thumb is commit after you do anything. If you update jQuery in the project then make a commit to mark that update. You don't need to commit after every line change so use your best judgement. If you are making changes to calendar and the contact form then try to commit your calendar changes before moving on to your contact form changes.

Always remember to attach a commit message to every single commit and be as descriptive as possible in what was done in that commit. This helps a lot with diff, reverting, and overall code reviews.

The first message should always be short and to the point. Think of this as a summary of your commit.

```
git commit -a -m "Updated jQuery to v2.0."
```

When you need to elaborate on your summary you can attach a second message to be an extended description and can go into as much detail as you need.

```
git commit -a -m "Refactoring calendar plugin." -m "Removed duplicated functions in controller, added more descriptive comments, fixed SQL query on edit, and added caching."
```

All commits that relate to an open ticket or issue should include the ticket number in the message. This allows us to reference a ticket when reviewing commits and keep better track of what led to the code change. The number would be a Zendesk ticket, a GitHub issue, or issue from BitBucket.

```
git commit -a -m "Changing default location on Google Map to 30.2500, 97.7500. #1234"
```

For details on creating commits checkout the [git docs](http://git-scm.com/docs/git-commit).

---

## Branches

You should **never** make any code changes directly on the `master` branch. This branch should always be considered stable and matches production. How you handle branches during development will depend on the project.

If you are working on a fairly simple project then you might just have a `dev` branch along with `master`. All your development will take place on `dev` and only merged into `master` when properly QA tested.

However, if you are working on a more complex or larger project then it might make more sense to use feature branches. Say you are working on adding event locations to the calendar plugin in mbCMS, you might have a branch of `calendar-adding-locations`. You would develop and QA here. Then when ready that would get merged into `dev` for a proper QA and review with another developer. After final approval that would then be merged into `master` and pushed to production.

However you do branches the most important thing to remember is **never develop directly on ``master``**.

For details on creating and using branches checkout the [git docs](http://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging).

---

## Tags

You will be using tags on every project.

* Every time a branch is deployed to an environment it should be tagged with a datetime stamp.
  * When `master` is deployed to production it would be tagged as `master-201502201109`.
  * When `dev`  is deployed to development it would be tagged as `dev-201502201109`.

When using mBoy Deployments this is handled for you automatically. See **General - Deployments** for more details.

If you are not using a deployment process, you must manually create these tags and push. These tags allow each developer to know if there are commits that haven't been deployed.

For details on creating, pushing, or checking out tags checkout the [git docs](http://git-scm.com/book/en/v2/Git-Basics-Tagging).

---

## End of Life

When a project is being redesigned or moving away from Monkee-Boy, we should mark the last active state of the code as `End of Life`. This is primarily helpful during a redesign as a way to archive the old site when taking the new site live. This allows us to checkout old versions at any time.

**Project Removal**
* Create a new branch from `master` with the name `EOL-YYYYMMDD` (`EOL-20150220`). Push this new branch to the remote.
* Open the repo on BitBucket and under settings change the main branch to the new EOL branch you pushed above.
* Delete any branches that were part of the old site; `master`, `staging`, `dev`, etc. These should be removed from your local and from the remote.

**Project Redesign**
* At the start of the redesign process you will create a `redesign` branch. This will allow you to continue to update the live site as needed with the `dev` and `master` branches until the redesign is complete.
* When the redesign is complete and ready to go live - create a new branch from `master` with the name `EOL-YYYYMMDD` (`EOL-20150220`). Push this new branch to the remote.
* Open the repo on BitBucket and under settings change the main branch to the new EOL branch you pushed above.
* Delete any branches that were part of the old site; `master`, `staging`, `dev`, etc. These should be removed from your local and from the remote.
* From your `redesign` branch, create a new branch for `dev`. Push the new branch and deploy as needed.
* From `dev`, create a new branch for `staging`. Push and deploy. *(optional, only if a staging environment is needed)*
* From `staging` (or `dev` if there is no `staging`), create a new branch for `master`. Push the new branch and deploy as needed.
* Open the repo on BitBucket and under settings change the main branch back to `master`.

---

## Thanks

* [Tim Pope on proper commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
* [GitHub on great commit messages](https://github.com/blog/926-shiny-new-commit-styles)
