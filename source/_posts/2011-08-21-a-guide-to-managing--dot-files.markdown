---
layout: post
title: "A Guide to Managing .(dot) Files"
date: 2011-08-21 12:24
comments: true
categories: [git, unix, dotfiles]
---

Home directory on a terminal/shell/bash for developers is close to what a backstage is for rockstars. That's where we put most of our self curated scripts which could do the magic for us at the moment we want. They make us highly productive. We wish that it's setup right at every place, so we could just start working - instead of re-tuning the environment variables again.

As a programmer often we work out of different machines, or login to remote machines for managing or debugging or even deploying our code. Thus its highly important to have the ability to sync where we need them.

###Store them in Source Control

There are several benefits to have them under source control. After all it is naturally beneficial to version them just like any code that we write. It would be easy to bring them back to live if your machine dies, or to resort to a last working copy.

Chose any source control that you are comfortable with. I have chosen git for various obvious benefits and its something I commonly use these days.

###Github or Dropbox or Remote Folder backup?

Once you decided to commit them to a source control system, the next obvious decision is to where to put the source control system. You definitely don't want them backup'ed only on local system, as you would need to sync them else where and also save yourself from machine crashes.

I would choose a public [Github](http://github.com) repository if my dot-files didn't have any private information. But quite often we share keys to remote machines, hashed passwords and other private information under our home directory. So I would choose a dropbox account or remote folder to sync them up based on your privacy requirements (i.e. what you have in your dot files). Dropbox normally syncs up your files at ~/Dropbox, thus you can easily use it.

{% gist 1160309 dot-files-1.sh %}

This creates the master repository under DropBox. Go check out dotfiles repository into some local directory.

{% gist 1160309 dot-files-2.sh %}

###Why not to make your home directory as a git repo!

Some people manage their home directory in a similar way, but keeping the entire home directory directly into the repository; and adding git ignore for the other folders under home directory. This has its minor advantage of being able to show you un-commited changes to your dot files, but with other drawbacks.

- requires manually adding git ignore for every new folder that you create on home
- if you want to ignore a folder only on several machines, not all.
- you don't want to sync all the dotfiles. you might want to just bring in what you want.

###How to
Copy over the dot files you want to save under the repository and commit them.

{% gist 1160309 dot-files-3.sh %}

I rather use small scripts to copy the dotfiles back to home directory or create symlinks in home directory that would point to the checked out repository. To copy or symlink is another personal choice. With symlinks you can change the files in home directory as seem them in git change-list. My personal favorite is to copy them across with file permissions and settings preserved.

{% gist 1160309 dot-files-4.sh %}

You now can check out the git repo and run those commands to sync your dot files. Configure Dropbox to sync the files on the machine, or just copy over that dot-files.git folder.

###Workflow

{% gist 1160309 dot-files-5.sh %}

On a new machine where there are existing dot files I normally run the update.sh script, so the existing dot files are copied over to repo. Then stash the changes (thus saving the current system config), and run deploy to move my dot files to the home directory. I can revert to old version from stash. Or I can diff the changes with stash and merge them to a machine specific branch.

That's it, never again lose your dot files.
