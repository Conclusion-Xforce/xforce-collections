xforce.aap_tools.configure_hub_collections
=========

Role to perform the collection repositories on Ansible Private AutomationHub configuration.

Requirements
------------

Collection: ansible.hub, version '>=1.0.0'

Role Variables
--------------

= hub_host: FQDN Hostname of the hub host (or VIP-name) that needs configuring
= hub_admin_user: Username of the admin user on the hub
- hub_admin_password: Password of the admin user on the hub
- hub_validate_certs: Boolean determining SSL certificate validation
- hub_remote_repos: List dictionaries holding remote sources for repositories
    - = name: Name of the collection repository in the hub
      = url: Url to the remote source of the repository
      - auth_url: Separate authentication url
      - token: Authentication token for the remote source
      - requirements: List of collections to mirror to the hub - applicable on the Community repo (galaxy.ansible.com)
- hub_proxy_url: Url of a http-proxy to be used to access remote sources
- hub_proxy_username: Username for authentication to the http-proxy
- hub_proxy_password: Password for authentication to the http-proxy
- hub_redhat_token: API Access token for Red Hat supported collection download, to be created at console.redhat.com


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - role: xforce.aap_tools.configure_hub_collections
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
