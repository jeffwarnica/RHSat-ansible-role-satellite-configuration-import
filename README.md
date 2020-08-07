Role Name
=========

Facilitate configuration of Red Hat Satellite, given an git repository of an eport

Requirements
------------

Codewise, nothing special. Requires an export git repository as prepared by RHSat-ansible-role-configuration-export.

Role Variables
--------------

import_git_url: 
import_git_branch:
	Git URL and branch name of source content.

satellite_api_username:
satellite_api_password:
	Credentials to access the Satellite API.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
