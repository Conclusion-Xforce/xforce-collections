# xforce.aap_tools.manage_hub_collections

Role to manage the remote collection repositories on Ansible Private Automation Hub. It will create the
remote definitions of collection repositories as defined in the aap_collection_repos variable. It is up to
the calling playbook to ensure that e.g. proper tokens for the remote repositories are provided.

## Requirements

Collection: ansible.hub, version '>=1.0.0'

## Role Variables

- ***platform_host***: FQDN Hostname of the Platform Gateway host (or VIP-name)
- ***aap_admin_user***: Username of an admin user on the Private Automation Hub
- ***aap_admin_password***: Password of the admin user on the Private Automation Hub
- aap_validate_certs: Boolean determining SSL certificate validation
- aap_proxy_url: Url of a http-proxy to be used to access remote sources
- aap_proxy_username: Username for authentication to the http-proxy
- aap_proxy_password: Password for authentication to the http-proxy

- aap_collection_repos: List of dictionaries holding remote sources for repositories
    - ***name***: Name of the collection repository in the hub
    - ***url***: Url to the remote source of the repository
    - auth_url: Separate authentication url
    - password: Password to authenticate to the remote repository
    - token: Authentication token for the remote source
    - requirements: List of collections to mirror to the hub - applicable on the Community repo (galaxy.ansible.com)
    - download_concurrency: Number of concurrent collections to download (default: 10)
    - max_retries: Retries to use when running sync (default: 0)
    - rate_limit: Limits total download rate in requests per second
    - request_timeout: Specify the timeout Ansible should use in requests to the Hub
    - signed_only: Whether to only download signed collections (default: false)
    - sync_dependencies: Whether to download dependencies when syncing collections (default: true)
    - description: Description for the collection repository
    - interval: The interval to request an update from the Hub
    - private: Make the repository private (default: false)
    - retain_repo_versions
- aap_reposync_wait: Boolean determining waiting for collection repository syncing

## Example Playbook

Assuming a roles section is used in the playbook, this role could be called as:

```
- hosts: localhost
  roles:
    - role: xforce.aap_mgmt.manage_hub_collections
      vars:
        platform_host: automationcontroller.example.com
        aap_admin_user: admin
        aap_collection_repos:
          - name: rh-certified
            url: https://console.redhat.com/api/automation-hub/content/published/
            auth_url: https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
            token: "{{ my_redhat_token }}"
```

## License

GPL-3.0-only
