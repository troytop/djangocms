Django CMS Sample
=================

A simple Django CMS site based on the [installation tutorial](http://docs.django-cms.org/en/latest/how_to/install.html#).

Running locally
---------------

The `project.db` SQLite database will be used if no `VCAP_SERVICES` environment
variable is set with PostgreSQL database connection information. A superuser
for the site is already configured (username:`admin` password:`admin`) .

Pushing to Cloud Foundry
------------------------

The demo will work in Cloud Foundry using the local (but non-persistent) SQLite
database without any further configuration:

    $ cd djangocms
    $ cf push ...

To deploy something more useful and robust, create a PostgreSQL backing
service, then uncomment the `services` block in `manifest.yml`. Make sure the
service name matches the service you have created. The `cf push` command should
automatically bind the app to the service instance.

Setup
-----

Before you can use the site, you must run the database migration. Using the `cf
run-task` command is the easiest way to do this:

  $ cf run-task djangocms "python manage.py migrate" --name migrate

To create the initial superuser for the site, use `cf ssh` to run the
`createsuperuer` script.

  $ cf ssh djangocms
  bash-4.3$ /tmp/lifecycle/shell # loads app python env
  bash-4.3$ django manage.py createsuperuser
  ...

When the first admin user has been created, you can start [using Django
CMS](http://docs.django-cms.org/en/latest/how_to/index.html#).


