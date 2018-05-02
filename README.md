# City of Boston Drupal Coding Challenge

## Welcome!
Thanks for your interest in being a software engineer on 
the City of Boston’s 
[Digital team](https://www.boston.gov/departments/digital-team)! 
And congratulations for making it this far in the hiring process.

The goal of this code challenge is to give us a chance to 
evaluate some aspects of your software engineering skill set, 
and for you to get a taste for how we’re building new web 
applications at the city.

This exercise shows off one kind of work we do on the Digital 
team, which is extending Drupal's base system by writing custom
module code. Specifically in this excercise you are going to be
migrating data from a third party JSON API into Drupal. If you 
like this code challenge, that’s a good sign that you’ll be 
happy building things here.

## Project Setup

### Download Lando
Our goal is to standardize the local environment setup as much
as possible to create a consistent experience for developers so 
you can focues on actually writing code for the challenge. We've
approached this task using a project called 
Lando (https://docs.devwithlando.io/) which will create the full 
software stack needed to run the application using Docker containers.
If you have an alternative means for local development, feel free to
use that instead, the intention of the Lando setup is simply to save
you time. To get started with Lando, you first need to install it: 

If you're on a Mac:
1) Install homebrew: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2) Install lando: `brew cask install lando`

If you're on Ubuntu:
1) Open [this link](https://github.com/lando/lando/releases/download/v3.0.0-beta.40/lando-v3.0.0-beta.40.deb) and run the installer.

If you're on Windows (requires Windows 10):
1) Open [this link](https://github.com/lando/lando/releases/download/v3.0.0-beta.40/lando-v3.0.0-beta.40.exe) and run the installer.
2) Enable Hyper V by opening PowerShell as an administrator and running: `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

For more Lando installation help, see the docs: https://docs.devwithlando.io/installation/installing.html

### Clone the project
We use Git to version control all our projects, so we're using it
on this coding challenge as well. Clone a copy of this repository 
to your local computer before getting started:
`git clone https://github.com/jimafisk/drupal_coding_challenge.git`

### Create the application
1) In your terminal (command line), make sure you're inside the base folder of the project: `cd drupal_coding_challenge`
2) Create the software stack using lando: `lando start`

### Login to the application
Visit the URL that lando creates for you and displays in the terminal. It will
be unique to your environment, but should look something like this:
http://localhost:32901. Then click "Log in" in the upper right and enter these
credentials:
- Username=admin
- Password=admin

Alternatively you can use `lando drush uli` but you'll need to adjust the baseurl
for this to work.

## Data Structure
We have two (2) content types in the system already created for you:
1) Modules
2) Maintainers

These represent the types of information we're going to be pulling from the API
on the Drupal project's website: https://www.drupal.org/drupalorg/docs/api

Note that the Module content type has an entityreference to the Maintainers
content type. Every module on Drupal.org has a person behind it that actually
maintains the code. We're using the entityreference field to establish this 
relationship between the two content types.

## The Data Feed
We can get module information by looking through Drupal's node feed:
https://www.drupal.org/api-d7/node.json

We can also apply filters to this feed to narrow our dataset. For 
example, we only want nodes for Contributed modules and maybe we only
want ten (10) items to display for now:
https://www.drupal.org/api-d7/node.json?type=project_module&limit=10 

**Hint:** If you wanted to top ten most popular Drupal modules you
could apply sort criteria and filters like so:
https://www.drupal.org/api-d7/node.json?type=project_module&sort=field_download_count&direction=DESC&limit=10

Similarly, we can retreive data about project maintainers from
Drupal's API:
https://www.drupal.org/project/drupal/maintainers.json

You can limit the Maintainers to a specific Module by referencing
the Node ID (nid) of the project. So for example Buddy List 
(https://www.drupal.org/project/buddylist) has a Node ID of
`3230` so you can see Buddy List maintainers like so:
https://www.drupal.org/project/3230/maintainers.json

**NOTE**: The query endpoints will return up to 100 resources, paged.
For example you could look through all users on Drupal.org page by 
page like so: https://www.drupal.org/api-d7/user.json?page=1, 
https://www.drupal.org/api-d7/user.json?page=2, etc.

You can narrow down the User feed to a specific user by filtering the
list by their ID like so: https://www.drupal.org/api-d7/user.json?uid=2747155

There are services out there that will format JSON into an easy-to-read 
format with a simple copy and paste: https://jsonformatter.curiousconcept.com/

## The Code
The code you're going to be writing is in a custom module called 
`top_ten_modules`. 

## Objective
We want to pull in the top 10 most popular Modules from Drupal.org as 
determined by the project's number of downloads (`field_download_count`). We
Also want to pull in the corresponding profile information from the maintainers
of these projects so we can display a quick thank you for their work on our site.
The actual thank you will be displayed in a View that has already been created 
for you. Your goal is to bring the relevant content into the system and establish
the relationship between the Modules and the Maintainers.
