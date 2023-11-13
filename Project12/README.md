# ANSIBLE PROJECT
# Ansible Dynamic Assignments (Include) and Community Roles
Ansible is an actively developing software project, therefore you are recommended highly to always visit [Ansible Documentation](https://docs.ansible.com/) for the latest updates on modules and their usage.

We can perform configurations using **playbooks**, **roles** and **imports** from the previous Ansible Projects. 

In this project we will introduce `dynamic-assignments` by using **include** module.

### Difference between static and dynamic assignments?
- `static-assignments` uses _import_ Ansible module while `dynamic-assignments` uses the _include_ module.

Hence

    import = Static
    include = Dynamic
### Import Module
- When you use the import module, all the statements in the playbooks are processed before they are read.
- Also means when you execute `site.yml` playbook, Ansible will process all the playbooks referenced during the time it is parsing the statements.
- During actual execution, if any statement changes, such statements will not be considered. Hence, it is static.

### Include Module
- When the include module is used, all the statements in the playbook are processed during playbook execution.
- This means that any changes to the statements encountered during execution will be taken into account.

**NB:** In most cases, it is recommended to use `static-assignments` for playbooks, because it is more **reliable**. 

With `dynamic-assignments`, it is hard to debug playbook problems due to its dynamic nature. However, you can use `dynamic-assignments` for environment specific variables as we will be introducing in this project.

### Introducing Dynamic Assignment Into Our structure
In your `https://github.com/<your-name>/ansible-config-mgt` GitHub repository start a new branch and call it `dynamic-assignments`.
In My case here,  `https://github.com/travdevops/ansible-config-mgt`
