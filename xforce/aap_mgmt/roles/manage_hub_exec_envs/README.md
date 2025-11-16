# xforce.aap_mgmt.manage_hub_execenvs

Role to manage the execution and decision environment on Ansible Private Automation Hub. It will
create the remote registry definitions for the container images as defined in the aap_container_registries
variable, and it will create the container image definitions as defined in the aap_container_images
variable. It is up to the calling playbook to ensure that e.g. proper tokens for the remote repositories
are provided.

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
