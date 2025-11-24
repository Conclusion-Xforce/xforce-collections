# xforce.aap_mgmt.manage_hub_exec_envs

The role manage_hub_exec_envs is used to configure the execution environment repositories in Ansible Automation Platform. It contains three tasks: validate_input, configure, and sync.

The configure task configures the registries for execution environments by using the ah_ee_registry module. It loops through the aap_container_registries list and sets the name, URL, username, password, proxy_url, proxy_username, proxy_password, and state for each registry.

Next it adds the execution environments to the hub by using the ah_ee_repository module. It loops through the aap_container_images list and sets the name, description, include_tags, exclude_tags, upstream_name, registry, and state for each execution environment.

The sync task syncs the registries and execution environments on the hub by using the ah_ee_registry_sync and ah_ee_repository_sync modules. It loops through the aap_container_registries list and aap_container_images list to sync each registry and execution environment.

The validate_input task checks that a hub host is specified, a hub admin user is specified, and a hub admin password is specified.

Entrypoint for the role is either the main.yml or the standalone_sync.yml task file.

- main.yml is used when configuring execution environments

Usage:
```
tasks:
  - ansible.builtin.include_role:
      name: xforce.aap_mgmt.manage_hub_exec_envs
```
- standalone_sync.yml is used when only the syncing of repositories and images is requested

Usage:
```
tasks:
  - ansible.builtin.include_role:
      name: xforce.aap_mgmt.manage_hub_exec_envs
      tasks_from: standalone_sync.yml
```

# Requirements

Collection: ansible.hub, version '>=1.0'

# Role Variables

- ***platform_host***: FQDN Hostname of the Platform Gateway host (or VIP-name)
- ***aap_admin_user***: Username of an admin user on the Private Automation Hub
- ***aap_admin_password***: Password of the admin user on the Private Automation Hub
- aap_validate_certs: Boolean determining SSL certificate validation
- aap_proxy_url: Url of a http-proxy to be used to access remote sources
- aap_proxy_username: Username for authentication to the http-proxy
- aap_proxy_password: Password for authentication to the http-proxy

- aap_container_registries: List of remote registries for execution images
    - ***registry***: Label to link execution environment images to registries
    - ***name***: Name of the registry within Private Automation Hub
    - ***host***: Source container registry
    - ***proto***: Protocol to access registry (e.g. https)
    - username: Source registry username
    - password: Source registry password (always store encrypted)
- aap_container_images: List of execution environment images
    - ***name***: Name of the image within Private Automation Hub
    - ***image***: Name of the image
    - namespace: Namespace of the execution environment image
    - registry: Label to link the image to a remote registry
    - description: Description of the image
    - type: Type of image: execution, builder, decision
    - tags: List of tags to include for this image
    - skip_tags: List of tags to exclude for this image
- aap_container_namespaces: List of namespaces for **local** container images
- aap_ee_sync_wait: Boolean whether or not to wait for synchronization to complete.

## Example Playbook

Assuming a roles section is used in the playbook, this role could be called as:

```
- hosts: servers
  roles:
    - role: xforce.aap_mgmt.manage_hub_execenvs
      vars:
        platform_host: automationcontroller.example.com
        aap_admin_user: admin
        aap_container_registries:
          - label: rh-registry
            name: "Red Hat Registry"
            host: registry.redhat.io
            proto: https
            username: "registry_user"
            password: "registry_token"
        aap_container_images:
          - namespace: ansible-automation-platform-25
            image: ee-supported-rhel9
            label: rh-registry
            name: Default execution environment - RHEL-9
            description: Red Hat Ansible Automation Platform Supported Execution Environment on RHEL-9
```

## License

GPL-3.0-only
