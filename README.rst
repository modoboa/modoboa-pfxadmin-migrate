modoboa-pfxadmin-migrate
========================

|landscape|

A script to migrate from PostfixAdmin to Modoboa. It has been tested
against versions 2.3.3 and upper.

.. note::

   This script is only suitable for a new Modoboa installation.

Installation
------------

Install this extension system-wide or inside a virtual environment by
running the following command::

  $ pip install modoboa-pfxadmin-migrate

Edit the ``settings.py`` file of your modoboa instance and add
``modoboa_pfxadmin_migrate`` inside the ``MODOBOA_APPS`` variable like this::

    MODOBOA_APPS = (
    
      # End of list
      'modoboa_pfxadmin_migrate',
    )

Then, add a new database connection named ``pfxadmin`` into the
``DATABASES`` variable corresponding to your PostfixAdmin setup::

  DATABASES = {
      "default" : {
          # default connection definition
      },
      "pfxadmin" : {
          "ENGINE" : "<engine>",
          "NAME" : "<database name>",
          "USER" : "<database user>",
          "PASSWORD" : "<user password>",
      }  
  }

This connection should correspond to the one defined in PostfixAdmin's
configuration file.

Run the script
--------------

You are now ready to start the migration so run the following commands::

  $ cd <modoboa_instance_dir>
  $ python manage.py migrate_from_postfixadmin -s <password scheme>

``<password scheme>`` must be replaced by the scheme used within
postfixadmin (``crypt`` most of the time).

Depending on how many domains/mailboxes your existing setup contains,
the migration can be long. Just wait for the script's ending.

The procedure is over, edit the ``settings.py`` file and:

* remove the ``pfxadmin`` database connection from the ``DATABASES``
  variable
* remove ``'modoboa_pfxadmin_migrate'`` from the
  ``MODOBOA_APPS`` variable

You should be able to connect to Modoboa using the same credentials
you were using to connect to PostfixAdmin.

.. |landscape| image:: https://landscape.io/github/modoboa/modoboa-pfxadmin-migrate/master/landscape.svg?style=flat
   :target: https://landscape.io/github/modoboa/modoboa-pfxadmin-migrate/master
   :alt: Code Health
