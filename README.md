Ansible role used by RDO to deploy the RDO dasboard

Code of the dashboard is on https://github.com/rdo-infra/rdo-dashboards

# Usage

The role can be used like this:

```
$ cat deploy_dashboards.yml
- hosts: web
  roles:
  - role: rdo_dasboards
    website_domain: dashboard.example.org
```

Since the role use the role httpd from http://github.com/OSAS/ansible-role-httpd,
several options can be used to enable https with letsencrypt and others. See the 
documentation of the httpd role for more information

# Code and data refresh

The data is updated every 15 minutes, using a cron job running as a non privileged
user. The code itself is updated every 20 minutes using a cron job, and the whole 
application run under a user that has no specific privilege.

# Authentication between script and frontend

To ensure that no one can push bogus information, a variable `token_auth` must be declared.
However, this is not critical to protect, and a random variable could simply be used
for every deployment and things would be fine. 
