# schiphol.management.manage_ctrl_exec_envs

Role to manage the execution environment on Ansible Controller. It will ensure
that execution environments defined in the hub_ee_images variable exist in
Automation Controller (and all other EE's are removed)

## Requirements

Collection: ansible.controller, version '<4.6.0'

## Role Variables

- ***controller_host***: FQDN Hostname of the controller host (or VIP-name) that
  needs configuring
- ***controller_username***: Username of the admin user on the controller
- controller_password: Password of the admin user on the controller
- aap_validate_certs: Boolean determining SSL certificate validation
- hub_ee_registries: List of remote registries for execution images
    - ***registry***: Label to link execution environment images to registries
    - ***name***: Name of the registry within Private Automation Hub
    - ***host***: Source container registry
    - ***proto***: Protocol to access registry (e.g. https)
    - username: Source registry username
    - password: Source registry password (always store encrypted)
- hub_ee_images: List of execution environment images
    - ***name***: Name of the image within Private Automation Hub
    - ***image***: Name of the image
    - namespace: Namespace of the execution environment image
    - registry: Label to link the image to a remote registry
    - description: Description of the image
    - tags: List of tags to include for this image
- hub_ee_sync_wait: Boolean whether or not to wait for synchronization to
  complete.

## Example Playbook

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

```
    - hosts: servers
      roles:
        - role: schiphol.management.manage_hub_exec_envs
          hub_host: automationcontroller.example.com
          hub_admin_user: admin
          hub_ee_registries:
            - registry: rh-registry
              name: "Red Hat Registry"
              host: registry.redhat.io
              proto: https
              username: "registry_user"
              password: "registry_token"
          hub_ee_images:
            - name: Default execution environment - RHEL-9
              image: ee-supported-rhel9
              namespace: ansible-automation-platform-24
              registry: rh-registry
              description: Red Hat Ansible Automation Platform Supported
              Execution Environment on RHEL-9
```

## License

GPL-3.0-only
