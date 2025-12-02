Project configuration and management
====================================

Django projects integrating the functionalities provided by ``django_rdkit`` should configure their settings to use the PostgreSQL database backend::

  DATABASES={
      'default': {
          'ENGINE': 'django.db.backends.postgresql',
          # [...],
      }
  }

This project supports both ``psycopg2`` and ``psycopg`` (psycopg3) as PostgreSQL drivers. Install your preferred driver separately::

  pip install psycopg2  # or psycopg2-binary
  # OR
  pip install "psycopg[binary]"  # psycopg3 with pre-built binary
  # OR
  pip install "psycopg[c]"  # psycopg3 with C speedups (requires build tools)

Two additional operations are then to be performed on the database in order to use the RDKit cartridge.

Firstly, it is necessary to have the cartidge installed in the configured database. This operation corresponds to executing the following SQL statement::

  CREATE EXTENSION IF NOT EXISTS rdkit;

One simple way to integrate this operation within a django project consists in installing the ``django_rdkit`` package as a django application::

  INSTALLED_APPS = (
      # [...]
      'django_rdkit',
  )

A migration will be this way automatically included in the database configuration, ensuring that that the RDKit extension is created (please note that creating an extension requires database superuser privileges).

Migration Operations
--------------------
.. module:: django_rdkit.operations

.. currentmodule:: django_rdkit.operations

.. class:: RDKitExtension( )

An ``Operation`` subclass that will install the RDKit cartridge (install ``django_rdkit`` as a django application to include a migration that wraps this operation).
