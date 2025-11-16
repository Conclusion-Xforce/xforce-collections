# xforce.aap_mgmt.manage_ctrl_exec_envs

Role to manage the execution environment on Ansible Automation Controller. It will ensure
that execution environments defined in the aap_container_registries variable exist in
Automation Controller. Execution environments not listed in aap_container_registries, or
having a namespace listed in aap_container_namespaces will be removed from Automation Controller

## Requirements

Collection:
- ansible.controller, version '>4.6.0'
- ansible.platform, version '>2.5.0' 

## Role Variables

- ***platform_host***: FQDN Hostname of the Platform Gateway host (or VIP-name)
- ***aap_admin_user***: Username of an admin user on the Private Automation Hub
- ***aap_admin_password***: Password of the admin user on the Private Automation Hub
- aap_validate_certs: Boolean determining SSL certificate validation
- aap_container_images: List of execution environment images
    - ***name***: Name of the image within Private Automation Hub
    - ***image***: Name of the image
    - namespace: Namespace of the execution environment image
    - registry: Label to link the image to a remote registry
    - description: Description of the image
    - type: Type of image: execution, builder, decision
    - tags: List of tags to include for this image
    - skip_tags: List of tags to exclude for this image
- aap_container_namespaces: List of namespaces that can exist on Controller
- aap_reserved_images: List of image **names** that should not be deleted from Controller

## Example Playbook

Assuming a roles section is used in the playbook, this role could be called as:

```
- hosts: servers
  roles:
    - role: xforce.aap_mgmt.manage_ctrl_exec_envs
      vars:
        platform_host: automationcontroller.example.com
        aap_admin_user: admin
        aap_container_images:
          - namespace: ansible-automation-platform-25
            image: ee-supported-rhel9
            label: rh-registry
            name: Default execution environment - RHEL-9
            description: Red Hat Ansible Automation Platform Supported Execution Environment on RHEL-9
```

## License

GPL-3.0-only
