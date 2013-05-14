rails_upgrade_article
=====================

I do not have the permissions to create a new svn repo for this project, so it will live here.

# So You Want to Upgrade Your Rails App...

Have you considered rewriting as an alternative?  Now might be the right time.  You really want to do this?  Okay.  I can't hold your hand every step of the way, but here is an outline of the process I used to upgrade a handful of rails 2 apps to the hippest version of rails 3 in early 2013.  At the time of this writing, rails 4 is nearing release.  If you are trying to upgrade all the way to rails 4, I cannot help you make that last leap.

I found that the upgrade process went smoothest when I divided it up into bite-sized chunks.  My method was to update to the latest revision within the current minor version, update to the oldest revision in the next minor version, and repeat.  I did the major 2-to-3 version update between an intermediate revision of the latest minor version of rails 2 and an intermediate revision of the oldest minor version of rails 3 because the resources available for the upgrade targeted rails 3.0.6.

## Version Map

* 2.3.12 (where we start)
* 3.0.6
* 3.0.10
* 3.1.0
* 3.1.3
* 3.2.0
* 3.2.13

The revision upgrades should be **much** easier than the version upgrades.

## 2.3.12 to 3.0.6 - The Big Jump

This is the most difficult step.  Make a new branch and take a deep breath.  The general strategy is to use rails new to generate a new rails 3 app in the same directory as the rails 2 app. Several files need to be backed up, and certain structural and syntactical differences need to be addressed through a merger process between the backup files and the new rails 3 files.  After this, additional incompatibilities need to be addressed throughout the app.  

### The rails_upgrade Plugin

There is an official rails plugin that automates much of the process of performing this major version upgrade.  Installation and usage is documented at https://github.com/rails/rails_upgrade.  Now would be a good time to watch Ryan Bates's awesome video on using this plugin: http://railscasts.com/episodes/225-upgrading-to-rails-3-part-1.  

After installing the plugin, running `rake rails:upgrade:check` will give you a list of issues detected by the plugin.  Save this output and the output of all rails_upgrade commands to a file for future reference.

### Backup

Creating the new rails 3 app will overwrite many files.  Running `rake rails:upgrade:backup` will backup most of the files you will need to keep.  It will also output a list of backed up files, which you should save for future reference.  You should consider if you have any additional files with modifications that you want to save.  Here are a few you may want to think about backing up:
* app/views/layouts/application.html.erb
* public/favicon.ico
* public/javascripts/application.js

It is helpful to give your additional backup files a '.rails2' extension, in keeping with the style of rails_upgrade.

### Generating New File Contents

rails_upgrade will automatically generate contents for a few key files. Run the following commands and save the output.
* `rake rails:upgrade:routes`
* `rake rails:upgrade:gems`
* `rake rails:upgrade:configuration`

#### Gotcha

rails_upgrade will pull the application module name from the name of the parent directory. If there is a period in this directory name, it will mess up and only use the portion of the directory name after the period. Do not trust the rails_upgrade plugin to get the application name right. This gotcha is the reason we will in the next section initialize the new rails 3 application from the parent directory rather than the root directory, as is suggested in the rails 3 upgrade railscast. 
This bug is fixed in my branch of rails_upgrade: https://github.com/HandyAndyShortStack/rails_upgrade
pull request: https://github.com/rails/rails_upgrade/pull/22
to install the plugin from this branch, use script/plugin install https://github.com/HandyAndyShortStack/rails_upgrade.git

### Installing Rails 3
