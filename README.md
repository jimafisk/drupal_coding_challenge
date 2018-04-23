#City of Boston Drupal Coding Challenge

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
1) install homebrew: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2) install lando: `brew cask install lando`

If you're on Ubuntu:
1) Open [this link](https://github.com/lando/lando/releases/download/v3.0.0-beta.40/lando-v3.0.0-beta.40.deb){:target="_blank"} and run the installer.

If you're on Windows (requires Windows 10):
1) Open [this link](https://github.com/lando/lando/releases/download/v3.0.0-beta.40/lando-v3.0.0-beta.40.exe){:target="_blank"} and run the installer.
2) Enable Hyper V, by opening PowerShell as an administrator and running: `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

For more Lando installation help, see the docs: https://docs.devwithlando.io/installation/installing.html

## Data Structure
We have two (2) content types in the system already created for you:
1) Modules
2) Maintainers

## The Data Feed
We want to get
https://www.drupal.org/api-d7/node.json?type=project_module&limit=10 

https://www.drupal.org/project/drupal/maintainers.json
