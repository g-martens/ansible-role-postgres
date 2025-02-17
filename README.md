Role Name
=========

This playbook is created to install an Postgres database on an Redhat 9 Based machine,
You can also create users and databases

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

# Postgres Vars
pg_version: "17"
postgres_host: "10.0.0.x"
pg_hba: "/var/lib/pgsql/17/data/pg_hba.conf"
pg_conf: "/var/lib/pgsql/17/data/postgresql.conf"
postgres_port: "5432"
postgres_sslmode: "Disable"
postgres_root_password: "passwrd"

#db user
postgres_user: "awx-user"
postgres_user_password: "password"
postgres_database_name: "awx"
allow_subnet: "0.0.0.0/0"


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - name: Deploy Postgress
      hosts: all
      become: true

      vars:
        pg_version: "17"
        postgres_user: "awx-user"
        postgres_user_password: "do7iZNapRTVJXrrnFw"
        postgres_database_name: "awx"
        postgres_root_password: password
        postgres_host: "10.0.0.x"
        pg_hba: "/var/lib/pgsql/{{ pg_version }}/data/pg_hba.conf"
        pg_conf: "/var/lib/pgsql/{{ pg_version }}/data/postgresql.conf"

        allow_subnet: "0.0.0.0/0"
        

    tasks:

      - name: Postgress
        ansible.builtin.include_role:
          name: postgres
        tags:
          - prepare
          - install
          - createdb
          - createusr
          - hardening

License
-------
Guido Martes

Author Information
------------------

for questions, Contact guido-_@live.nl
