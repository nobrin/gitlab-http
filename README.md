GitLab-http 2012-01-16
======================

Overview
--------
### Wrapper for accessing GitLab-gitolite over HTTP with GitLab accounts.

This short script **glgl(say 'guruguru')-http-auth** provides a slightly convinient access way to GitLab (i.e. `git clone http://gitlab.foo.com/git/my-project.git` with GitLab accounts).  [GitLab](http://gitlabhq.com/) is a web interface which has github-like interface.  Gitolite is so convinient for SSH, and is capable for Smart HTTP.  In case of Smart HTTP, gitolite needs apache authentication mechanism, which does not satisfy convinient use for GitLab.

This glgl-http-auth bridges GitLab and gitolite with HTTP authentication and access. This is so simple script.
With this script, you can access the repository of your GitLab with your GitLab account.


License
-------
AS IS.


Requirements
------------
GitLab-http is written in WSGI application.  Requires web server and mod_wsgi.

- Python 2.5+
- apache 2.2.x
- GitLab 2.0
- gitolite
- mod_wsgi


Installation
------------
1. setup apache, GitLab, gitolite
2. place glgl-http-auth into proper path (ex. with SuexecUserGroup, the script must be placed into under the DocumentRoot for restriction of apache.)

        # cd /var/www
        # mkdir gitlab-http
        # cd gitlab-http
        # cp /path/to/glgl-http-auth .
        # chmod +x glgl-http-auth

   after that, modify the head of glgl-http-auth for your environment.
3. edit apache configuration


Configuration
-------------
An example for apache is example.conf.
Modify ScriptAlias and WSGIAuthUserScript.


Usage
-----
If the script has been installed correctly, you can access the repository below.

    % git clone http://gitlab.foo.com/git/my-project.git


Implementation
--------------
This script provides authentication with GitLab web interface and wraps gl-auth-command of gitolite.

1. For hooking the authentication process of apache, this used mod_wsgi.
2. The handler for WSGIAuthUserScript attempts sign-in on GitLab.
3. If success, glgl-http-auth translate GitLab's email to identifier in gitolite using GitLab **production.sqlite3** DB directly.
4. After that, the script passes identifier in gitolite to `gl-auth-command`.


---
Thanks for getting interested in this script.  I am pleased if helpful.  
Nobuo OKAZAKI

URL: [http://github.com/nobrin/gitlab-http](http://github.com/nobrin/gitlab-http)

