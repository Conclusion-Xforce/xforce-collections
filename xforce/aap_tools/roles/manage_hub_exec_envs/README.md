xforce.aap_tools.manage_hub_execenvs
=========

Role to manage the execution environment on Ansible Private Automation Hub.

Requirements
------------

Collection: infra.ah_configuration, version '>=2.0'

Role Variables
--------------

= automationhub_host: FQDN Hostname of the hub host (or VIP-name) that needs configuring
= automationhub_admin_user: Username of the admin user on the hub
- automationhub_admin_password: Password of the admin user on the hub
- hub_validate_certs: Boolean determining SSL certificate validation
- aap_ee_registries: List of remote registries for execution images
  - = label: Label to link execution environment images to registries
    = name: Name of the registry within Private Automation Hub
    = host: Source container registry
    = proto: Protocol to access registry (e.g. https)
    - username: Source registry username
    - password: Source registry password (always store encrypted)
- aap_ee_images: List of execution environment images
    - namespace: Namespace of the execution environment image
    = image: Name of the image
    - label: Label to link the image to a remote registry
    = name: Name of the image within Private Automation Hub
    - description: Description of the image
    - type: Type of container image [execution, builder, decision]
    - tags: List of tags to include for this image
- aap_ee_namespaces: List of namespaces to protect from deletion
- hub_ee_sync_wait: Boolean whether or not to wait for synchronization to complete.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - role: xforce.aap_mgmt.configure_hub_execenvs
          automationhub_host: automationcontroller.example.com
          automationhub_admin_user: admin
          aap_ee_registries:
            - label: rh-registry
              name: "Red Hat Registry"
              host: registry.redhat.io
              proto: https
              username: "registry_user"
              password: "registry_token"
          aap_ee_images:
            - namespace: ansible-automation-platform-25
              image: ee-supported-rhel9
              label: rh-registry
              name: Default execution environment - RHEL-9
              description: Red Hat Ansible Automation Platform Supported Execution Environment on RHEL-9

License
-------

GPL-3.0-only
