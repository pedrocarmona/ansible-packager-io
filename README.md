Role Name
=========

This role aims to allow [packager.io](https://packager.io) users to easily install their packages in their servers. This packages are built with [heroku](https://heroku.com) buildpacks and user code.

### Why package your application?

When you package our web application it will run as a unix service. The most important reason to package your application is to have a complete freeze of your application context, dependencies and source code. This allows you to deploy exactly the same service across multiple hosts, with minimal effort. Apart from that, this service has its own user, and therefore you can set filesystem access acordingly. Also, you can use unix conventions to configure the service via the `/etc/` folder, and all the code will be placed in `/opt/`. Moreover, it has its own env variables.

Role Variables
---------------

The application name, which is also the name which will be used as the `unix service` after installation. (`packager_io_application_name`).

Typically, heroku buildpack applications include a `Procfile` wich declares the types of process that can be run by the service. For instance you could have a `web` process, and a `worker` process. If you include that in the compiled service, then you can configure the number of process instances (aka. heroku `dynos`) that are run for each kind of process. The role variable that declares the application processes and their instances is `packager_io_application_processes`.

Also, applications compiled with packager.io, are provided via an `apt` or `rpm` repository. In order to download your application you need to provide: `packager_io_key`,`packager_io_repo_owner`,`packager_io_repo_name`.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: pedrocarmona.packager-io, packager_io_application_name: "airflow", packager_io_application_processes: [ { type: "web", instances: 1 }, { type: "worker", instances: 2 } ], packager_io_key: "my_key", packager_io_repo_owner: "pedrocarmona", packager_io_repo_name: "airflow-pkg" }

License
-------

BSD

