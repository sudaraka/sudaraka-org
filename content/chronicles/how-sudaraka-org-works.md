{
  "title": "How Sudaraka.Org Works",
  "description": "How Sudaraka.Org Works - details description of technologies used in my website",
  "keywords": "Sudaraka.Org,technology,methodology,dokuwiki,dropbox,git,gitorious,linode",
  "date": "2013-02-24"
}

Following is a detailed description of how I setup and maintain my web
site.<!--more-->

## Objectives

  * Off-line availability for quick reference.
  * Real-time synchronization of off-line and on-line content.
  * Simple method of writing content (i.e. in plain text)
  * Make the code available under FLOSS license.
  * Geek fun!

## Software & Services

### DokuWiki

[DokuWiki](https://www.dokuwiki.org/), a Wiki software that is written in
PHP is the core component of the entire system. Everything else depends on
DokuWiki's it's simplicity and the way it stores the data (Wiki articles).

Article content of the DokuWiki is stored in plain text files, therefor
making it as readable quick reference files even without a web server to
render the HTML.

Plus, since DokuWiki doesn't require a database or any other support
software, even a low end computer running a light weight web server (i.e.
Nginx, Lighttpd) can host a local web site for off-line view.

Since this web site doesn't use all the features that are bundled with the
DokuWiki, I have striped out unused features and using it only as an engine
to convert and render HTML for the content that is in Wiki syntax.

### Dropbox

Although [Dropbox](https://www.dropbox.com/) is a closed source proprietary
service and has not so perfect track record when it comes to security, for
this setup it is an adequate solution. And since it does what it do best
(synchronizing files between multiple devices) I choose to overlook it's
closeness.

Dropbox act as centralized repository for content and the code of the website
which synchronously share the between my work stations and the web server.

### Linode

VPS hosting service provider that provides a very flexible platform to build
up a server for our needs almost from scratch.

Sudaraka.Org is hosted on a [Debian](http://www.debian.org/) server on
[Linode](http://www.linode.com/), which gives me the option to install and
configure Dropbox daemon for Linux.

### Gitorious

In order to maintain the complacency with the license of DokuWiki (GNU GPL v2),
I have published by modification in a public [GIT repository](https://gitorious.org/sudaraka-org/dokuwiki-mods)
hosted at [Gitorious](https://gitorious.org/).

Theme used is this website is also available on a separate [GIT repository](https://gitorious.org/sudaraka-org/dokuwiki-theme)
under GNU AGPL v3.

## Implementation

![](/images/chronicles/how-sudaraka-org-works-01.png)

### Main Workstation

Website is configured to run on Apache, and everything under the web root
except for the cache and meta data is under version control using GIT.

Local GIT repository has the Gitorious repository configured as
remote/upstream.

Web root is also symlinked to a directory under ~/Dropbox which is make the
code, data and the local GIT repository to be automatically synchronized into
the Dropbox cloud storage.

### Mobile Workstation

I do go out once every couple of months or so, in such occasions I like to
have my web site with me as a quick reference even when I'm off-line.

I simply have Dropbox software installed on my netbook and entire website is
with all the recent modifications is there automatically. A simple text
editor (or even cat) can be use to view the articles, to get the full glory
of my website I run a web server on this machine also.

Since Dropbox also brings the local GIT repository with it, I can also make
any modifications to the code here and push them to Gitorious.

### Web Server

Dropbox daemon is installed on the server and is started on the boot which
automatically bring modifications I do on the workstations on to the server.

## Benefits

  * Fulfills all the objectives mentioned above.
  * Provides in-house and off-site backup for both code and data.
