xforce.aap_tools.configure_controller
=========

Role to perform global Ansible Automation Controller configuration.

Requirements
------------

Collection: ansible.controller, version '<4.6.0'

Role Variables
--------------

= controller_host: FQDN Hostname of the controller host (or VIP-name) that needs configuring
= controller_admin_user: Username of the admin user on the controller
- controller_admin_password: Password of the admin user on the controller
- controller_validate_certs: Boolean determining SSL certificate validation
- controller_config_settings: List dictionaries holding the settings to set on the controller
    - name: Name of the setting (consult the controller api for the exact name)
      value: Value of the setting
- controller_instance_groups: Dictionary of instance groups and their instances on the controller


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - role: xforce.aap_tools.configure_controller
          controller_host: automationcontroller.example.com
          controller_admin_user: admin
          controller_config_settings:
            - name: "REMOTE_HOST_HEADERS"
              value:
                - "REMOTE_ADDR"
                - "REMOTE_HOST"
                - "HTTP_X_FORWARDED_FOR"

License
-------

GPL-3.0-only
