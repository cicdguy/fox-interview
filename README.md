Introduction:
=============

This is a homework assignment for an interview candidate to
complete as part of initial screening. This is a full vagrant
workspace that will execute the ansible provisioner.  To setup
you environment to run this first execute in this directory:

```shell
./setup_env
```

Then execute:

```shell
vagrant up
```

If you prefer another config management tool such as puppet
or chef, that is up to the interviewee to setup the provisioner
portion in the Vagrantfile and either provide documentation on
environment setup or automate that process as well.

Key Objectives:
===============

* Install lighttpd
* Configure lighttpd via a jinja2 template
* S3 artifact deployment into virtual host document root
  `/srv/bogusapp/`
* Full automation (`vagrant up` to working site with no
  manual intervention)
* Idempotency

Artifact deployment:
====================

The following access and secret keys have read only access
to the `bogus-app-homework` bucket in the `us-west-2` region:

```
export AWS_ACCESS_KEY_ID=XXXXXXXXXXXXXXXXX
export AWS_SECRET_ACCESS_KEY=YYYYYYYYYYYYYYYYYYYY
```

The artifact to deploy is `homework.tar.gz`. Note that this artifact needs to be unpacked.

Bonus
======

* Secure the S3 access and secret key
* Present some output at the end of the vagrant run with
  local host setup to test the named virtual host
* Be mindful of how roles or any config files are organized
