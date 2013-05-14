rails_upgrade_article
=====================

I do not have the permissions to create a new svn repo for this project, so it will live here.

# So You Want to Upgrade Your Rails App...

Have you considered rewriting as an alternative?  Now might be the right time.  You really want to do this?  Okay.  I can't hold your hand every step of the way, but here is an outline of the process I used to upgrade a handful of rails 2 apps to the hippest version of rails 3 in early 2013.  At the time of this writing, rails 4 is nearing release.  If you are trying to upgrade all the way to rails 4, I cannot help you make that last leap.

I found that the upgrade process went smoothest when I divided it up into bite-sized chunks.  My method was to update to the latest revision within the current minor version, update to the oldest revision in the next minor version, and repeat. I did the major 2-to-3 version update between an intermediate revision of the latest minor version of rails 2 and an intermediate revision of the oldest minor version of rails 3 because the resources available for the upgrade targeted rails 3.0.6.

## Version Map

* 2.3.12 (where we start)
* 3.0.6
* 3.0.10
* 3.1.0
* 3.1.3
* 3.2.0
* 3.2.13

The revision upgrades should be **much** easier than the version upgrades.

