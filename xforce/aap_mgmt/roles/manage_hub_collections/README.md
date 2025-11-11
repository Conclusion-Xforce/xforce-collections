xforce.aap_tools.manage_hub_collections
=========

Role to manage the remote collection repositories on Ansible Private Automation Hub. It will create the
remote definitions of collection repositories as defined in the aap_collection_repos variable. It is up to
the calling playbook to ensure that e.g. proper tokens for the remote repositories are provided.

Requirements
------------

Collection: ansible.hub, version '>=1.0.0'

Role Variables
--------------

- ***platform_host***: FQDN Hostname of the Platform Gateway host (or VIP-name)
- ***automationhub_admin_user***: Username of an admin user on the Private Automation Hub
- ***automationhub_admin_password***: Password of the admin user on the Private Automation Hub
- aap_validate_certs: Boolean determining SSL certificate validation
- aap_proxy_url: Url of a http-proxy to be used to access remote sources
- aap_proxy_username: Username for authentication to the http-proxy
- aap_proxy_password: Password for authentication to the http-proxy

- aap_collection_repos: List of dictionaries holding remote sources for repositories
    - ***name***: Name of the collection repository in the hub
    - ***url***: Url to the remote source of the repository
    - auth_url: Separate authentication url
    - token: Authentication token for the remote source
    - requirements: List of collections to mirror to the hub - applicable on the Community repo (galaxy.ansible.com)
- aap_reposync_wait: Boolean determining waiting for collection repository syncing

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - role: xforce.aap_mgmt.configure_hub_collections
          hub_host: automationcontroller.example.com
          hub_admin_user: admin
          hub_remote_repos:
            - name: rh-certified
              url: https://console.redhat.com/api/automation-hub/content/published/
              auth_url: https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
              token: "{{ hub_redhat_token }}"

License
-------

GPL-3.0-only
