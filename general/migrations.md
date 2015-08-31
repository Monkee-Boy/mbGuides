# Migrations ![Current Status](https://img.shields.io/badge/status-DRAFT-green.svg)

> Monkee-Boy's step-by-step guide for migrating sites to the Habitat.

## Preparing the Repository

**All site files need to be stored in a Bitbucket repository.**

If a Bitbucket repository isn't present at the time of the migration, perform the following steps:

* Download all files from the live site's FTP except for the wp-config.php file and the wp-content/uploads folder.
* Add the standard `.gitignore` file to the site's root folder.
* Initialize the repository and push the downloaded files to the `master` branch.
* Create a `dev` branch off of the `master` branch.

If a Bitbucket repository is present, but the files are outdated, perform the following steps:

* Download all files from the live site's FTP except for the wp-config.php file and the wp-content/uploads folder.
* Add the standard `.gitignore` file to the site's root folder.
* Create a new branch off of the repository's `master` branch that will be used to store the existing repository files.
* Push the downloaded files to the `master` branch.
* Create a `dev` branch off of the `master` branch.

## Setting Up the Deployment Environment

**SSH**
* Open your Terminal application and SSH into deploy@habitat.monkee-boy.com.
* Change into the /var/www directory.
* Check the existing production site and see if it redirects to `www` when submitted. If so, enter the following ([siteURL] should be replaced with the actual site URL):
```
~/bin/domaininit [siteURL] www
```
* Omit the trailing `www` if the site does not redirect.

**SFTP**
* SFTP into habitat.monkee-boy.com.
* Enter into the directory for the site you're migrating and create a `dev` folder in same level as the `www` folder.
* Create a `shared` folder within both the `www` and `dev` directories.
* Add the live site's .htaccess file, wp-config.php file, and wp-content/uploads folder to both `shared` directories.
  * See the Databases section for how to configure the wp-config.php file before adding it to the `shared` directory.

## Setting Up the Database

* Go to habitat.monkee-boy.com/phpmyadmin.
* Click on the Databases tab and create two new databases for the development and production sites.
  * Development: `[site]_dev`
  * Production: `[site]_www`
* Create a user for the parent database [site].
  * Ensure that the wildcard `*` is added to the user.
  * Have the system automatically generate a password for the user.
  * **Copy and paste these credentials in the site's wp-config.php file. The dev database's name should be '[site]_dev' and the production database's name should be '[site]_www'.**
* Log into the live site's FTP and export the database as a compressed gzip file.
* Import the compressed gzip file into both the development and production databases in the Habitat.

## Deploying the Site

* Add the Capistrano generator to the site by following the [Monkee-Boy deployment process](general/deployments.md).
  * Set the site's domain to the current site's domain.
* Deploy the site.
* Edit your hostfile to make sure that the dev site shows up on your machine.
  * 198.58.101.143 dev.[siteURL]
* SSH into deploy@habitat.monkee-boy.com.
* CD into the project directory.
* Run `cd dev/public.html`
* Run `wp search-replace ‘[produrl]’ ‘[devurl]' --all-tables`
