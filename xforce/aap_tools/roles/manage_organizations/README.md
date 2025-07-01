# schiphol.management.manage_global

===================================

## Introduction

This Ansible Collection contains roles to manage the basic configuration of the automation controller

## Requirements

ansible >= 2.14

## Role Variables

[=] controller_host       : FQDN of Automation Controller LB VIP
[=] controller_username   : User with admin rights
[=] controller_password   : Password for user with admin rights
[=] azdo_pat: ""          : Azure DevOPS Personal Access Token
[=] azdo_username         : Azure DevOPS Personal Access Token corresponding user
[=] organizations         : List of dictionaries describing the organizations to configure on Automation Controller
  [=] org_id              : 4-letter identifier of the Organization (Schiphol team)
  [=] name                : Name of the organization
  [-] description         : Description for this organization
  [-] instance_groups     : List of Execution Node instance groups for this organization (default: 'shared')
  [-] organization_admin  : List of users who are Org. Admins (only allowed on DEV)
  [-] credential_admin    : List of users who are Credential Admins (1 or 2 per Org)
  [=] teams               : List of dictionaries describing the Teams within the Organization
    [=] name              : Name of the team
    [-] description       : Description for this team
    [-] authorization_type: Authorization Type {user, approver, admin}

## Dependencies

ansible.controller <4.6
infra.ah_configuration

## Example Playbook

- name: Call the manage_global role for configuring the automation controller globally
  ansible.builtin.include_role:
    name: schiphol.management.manage_organizations
  vars:
    controller_host: "localhost"
    controller_username: "admin"
    controller_password: "password"
    azdo_pat: "<pat token>"
    azdo_username: "admin"

## License

BSD

## Author Information

Schipholgroup
