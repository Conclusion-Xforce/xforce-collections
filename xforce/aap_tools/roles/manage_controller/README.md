xforce.aap_tools.manage_controller
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
- cleanup_management_jobs: List of cleanup jobs with schedules
    - name: Name of the cleanup job
    - template: Job template for the cleanup job
    - rrule: Scheduling rrule
    - extra_data: Possible extra data for this job
- aap_global_credentials: List of global general-purpose credentials
    - name: Name of the credential
    - description: Description for the credential
    - organization: Name of the organization to which the credential belongs
    - credential_type: Credential type
    - inputs: Parameters for the credential like username, password etc

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
