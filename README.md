RHSat-ansible-role-configuration-import
=========

Facilitate the runtime configuration of Red Hat Satellite, given an git repository of an export produced by the matching role.

Limitations
-----------

While "import everything" is a nice tagline, this role does not accomplish it. There are various "install time" settings which are better configured with an install time playbook (it possibly using the same underlying foreman-ansible-modules), suitably wrapped with restart scripts and OS level configurations.

This does not manage actual content. The actual content of *content views* can not be "synced" with this tooling.

Renamed/Deleted elements:

No consideration is placed on the possibility of elements being deleted, or renamed. The import process into a system for unmanged artiofacts is unexplored.

Content Views:

We consider here a Content View to be a set of configurations, including Content View Filters, which in turn includes Content View Filter Rules. When a Content View *Version* is created, the configuration is applied against the state of the local repositories, which is a function of the content sync process. From this, it is impossible to sync the exact set of artifacts into a Life Cycle Environment view, short of using the hammer-cli tooling and moving around the actual content.

Furthermore, foreman-ansible-modules has an open issue that makes managment of CVF Rules impossible. During the development of this role, a strategy for importing "all" versions regardless, using the same buggy configuration, was developed with a view that upstream bugs would eventually be fixed, but this style turned out to be very slow. Accordingly, Content View Filters (and rules) are not being imported at all, nor does this role currently handle promotion of CVs through Lifecycles.

Workaround: It is suggested that to keep Lifecycle Environments in sync, the cv promotion playbook, from the associated -management project, be suitably modfied and used to run against several Satellite systems at "the same time" when "the last sync" finished, keeping their operational tasks in lockstep. At least until the underlying modules are buggy, one must manually keep in sync Content View Filter Rules.

This role should be safe to run to keep "all" other configurations in sync.

Requirements
------------

Requires an export git repository as prepared by RHSat-ansible-role-configuration-export.

The foreman-ansible-modules

Helpful would be the RHSat-management playbook/inventory project.


Role Variables
--------------

import_git_url: 
import_git_branch:
	Git URL and branch name of source content.

satellite_api_username:
satellite_api_password:
	Credentials to access the Satellite API.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:


	---
	- hosts: satellite[0]
	  gather_facts: no
	  connection: local

	  tasks:
	    - name: Run Import Role
	      include_role:
		name: ansible-role-satellite-configuration-import
	      run_once: true
	      vars:
		curl_validate_certs: false

License
-------

BSD

Author Information
------------------
Jeff Warnica <jwarnica@redhat.com>
Ritesh Chitalia <rchitali@redhat.com>

