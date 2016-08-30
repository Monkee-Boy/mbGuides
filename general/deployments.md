# Deployments ![Current Status](https://img.shields.io/badge/status-Approved-green.svg)

Monkee-Boy has tried to streamline our deployment process as much as possible. There are still things we can improve and will over time. We use Capistrano to manage our deployments between environments.

> **Monkee Tip**: If interested in an overview of what went into creating our deployment process checkout the blog post [How Monkee-Boy Does Deployments](http://iwasasuperhero.com/2015/04/how-monkee-boy-does-deployments/).

## The Setup

There are a few things you will need to get setup before you can start deployments.

### RVM & Ruby
* `curl -sSL https://get.rvm.io | bash -s stable --ruby`
* `rvm reload`

### Capistrano & Required Gems
* `gem install capistrano`
* `gem install hipchat`
* `gem install capistrano-gitslave`
* `gem install mboy-deploy --source PRIVATESOURCE`
  * See [private repo](https://bitbucket.org/monkeeboy/mboy-deploy-gem) for details.

## The Deployment

You have Capistrano and the required gems installed so you should be ready to deploy. If you are working on a new project then continue below for details on setting up the config files. If you are working on an existing project that already handles deployments, then deploying is really simple. Remember that deployments use the git repo so be sure to commit and push anything you need deployed.

* `cap production deploy`
  * This will deploy the `master` branch to the production environment (the live site). Do not ever deploy to production without first deploying to dev and doing a QA.
* `cap dev deploy`
  * This will deploy the `dev` branch to the development environment. You should always deploy here before production. This is where you will QA your work.
* `cap foo deploy`
  * In `./config/deploy` you can setup any number of environments to deploy to. You specify the path on the server and what git branch to use. Reference the dev and production files if needed. An example might be a staging environment that uses the `staging` branch for clients to QA/approve as a middle step between dev and production.
* `cap production build:bower`
  * You can setup custom Capistrano tasks to run with every deployment but you can also choose to only run tasks manually. It could be database migrations or maybe to sync a database between dev and production.
* `cap production deploy:rollback`
  * So, you deployed to production after doing a proper QA on dev but a bug showed up right after deploying to production. You can do a rollback which will rollback the site to the previous version just before you deployed.

## The Configuration

If working on a new project or one that hasn't been setup with our deployment process, you will need to generate the config files. You could do this manually but that's just not how developers work. We have a Yeoman Generator that asks you a few questions and generates the config files you need.

### The Generator

You will need to have npm and yeoman. Full details for setting up the generator can be found at [generator-mboy-deploy](https://www.npmjs.com/package/generator-mboy-deploy). After everything is installed you simply `cd` into the project root and run `yo mboy-deploy`. Some general basic questions will be project name, git url, and path on The Habitat. Depending on your project it will ask several more questions so you end up with a config that just works.

### The Manual Way

We highly recommend using the generator but it's always good to know what the generator is doing and how the config files work. Capistrano consists of at least three files. This will assume you started with one of the deploy templates or are viewing the files that the generator created.

`Capfile`

This file doesn't need any customizations in typical use. It requires the gems needed and loads any custom tasks.

`./config/deploy.rb`

This is where it all happens. You will notice that the file makes heavy use of the mBoy gem to load in defaults and customize the deployment messages. You can overwrite any of the defaults set in the gem as needed.

There are a few variables you are required to set before deploying.

* **:application** is the project name with no spaces or special characters.
* **:project_name** is the pretty project name that can have spaces; this is used for HipChat notifications.
* **:repo_url** should be the complete git url, typically from beanstalk.
* **:linked_files** should contain any files that are not in the repo but are still needed. This is typical config files like wp-config.php. Capistrano will create a symlink to these files inside `./shared`. These files must already exist inside shared or the deployment will fail.
* **:linked_dirs** should contain any directories that are not in the repo but are still needed. This Typically includes uploads, node_modules, bower_components, etc.

In `:deploy` you will find the build task. This task should be customized based on the project needs. Typically you would invoke `build:npm` and `build:bower` here. You could also do `jekyll build` or anything else needed for your build process.

At the bottom you will find `:build` which has some basic build tasks including `npm install` and `bower install` to update modules and components as needed. You can also add any other build tasks as needed.

`./config/deploy/production.rb`

Inside `./config/deploy` you will specify your environments. Typically this will be production and dev but you can have any number of environments.

There are only a few things that should be tweaked in these environment files.

* **:deploy_to** should be the server path where the deployment should take place. For production this would typically be `/var/www/projectdomain.com/_`. For dev this might be `/var/www/projectdomain.com/dev`.
* **:deploy_env** is the name of that environment. Typically will be production, dev, staging, etc.
* **:branch** is the name of the branch that should be deployed. Default is `master` so this only needs to be set in other environments besides production; see `./config/deploy/dev.rb` for example.

## The Process

So, what exactly happens when you run `cap production deploy`? First lets take a look at the directory structure on the server that deployments use.

```
./current
./public_html
./releases
    /RELEASETIMESTAMP
./repo
./shared
```

`./current` is a symlink to the latest release inside `./releases`. `./public_html` is a symlink to `./current` but this is not created by Capistrano and instead you will create it. `./releases` contains each stored release of the project. By default we store five releases at a time. This is where the project files actually live. `./repo` contains the bare bones git repo. `./shared` is where the linked files and directories live. Capistrano will create these directories and then it never touches them again.

Back to the deployment. Capistrano will first SSH into the server and cd `:deploy_to`. It then sets the shared assets; as in the linked files and directories. Then it creates a new release from the git repo in `./releases`. It then creates the symlinks from inside releases to the linked files and directories in `./shared`. Next it will run any of our build tasks such as `npm install`, `bower install`, or `jekyll build`. Then it will publish the new release by creating a symlink from `./current` to this new release inside `./releases`. Then it will finish by cleaning up any tmp directories and logging the revision to a log file.

When you do `cap production deploy:rollback` it follows much of this same flow with the exception of setting the current symlink to a previous release instead of the newest one.

To dive more into Capistrano don't forget the official documentation at [capistranorb.com](http://capistranorb.com/).
