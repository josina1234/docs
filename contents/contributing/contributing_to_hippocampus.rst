Contributing to HippoCampus
###########################

Creating new Packages
---------------------

.. note::

   This requires write permissions for the HippoCampus project.
   Hence, the instructions are only applicable for maintainers/owners of HippoCampus

As a good starting point copy the following files from ``hippo_common``.

* :file:`.pre-commit-config.yaml`
* :file:`.clang-format`
* :file:`.gitignore`
* :file:`pyproject.toml`

This is easily done if the ``hippo_common`` package exists in your workspace and your current working directory is inside your newly created package.

.. code-block:: console

   $ cp ../hippo_common{.gitignore,.clang-format,.pre-commit-config.yaml, pyproject.toml} ./


Working on Existing Packages
----------------------------


The following instructions are given exemplary for the ``hippo_common`` package and are applicable for other repositories/packages as well.

Forking the Repository
======================

.. note::

   This step requires you to have a GitHub account.

Go to repository's GitHub website: `https://github.com/hippoCampusRobotics/hippo_common <https://github.com/hippoCampusRobotics/hippo_common>`__ and hit the :guilabel:`Fork` button and select your account's personal repositories as location to create the fork.

Clone the Repository into the Workspace
=======================================

Clone your own fork of the repository into your workspace and replace ``<YOUR_USERNAME>`` with your actual GitHub username. 

.. code-block:: console

   $ git clone git@github.com:<YOUR_USERNAME>/hippo_common

Install the ``pre-commit`` Hooks
================================

Make sure you are inside the repository.

.. code-block:: console

   $ pre-commit install

.. note::

   If you do not have ``pre-commit`` installed, you can do so with

   .. code-block:: console

      $ sudo apt install pre-commit

These hooks ensure that proper formatting rules defined in the repository's :file:`.clang-format` and :file:`pyproject.toml` are applied.
Typically we have ``ruff`` configured as Python formatter and ``clang-format`` as Cpp formatter.
The hooks are run automatically for each commit and will abort the commit if the checks fail.
The proper formatting is applied as unstaged change to the respective files.
To 'accept' these changes, you have to stage them via ``git add <FILE>``.
After that you can retry the commit.

.. note::

   The hook only checks the formatting for the changes made since the last commit.
   If you want to check all files for proper formatting you can do so by running

   .. code-block:: console

      $ pre-commit run --all-files
      trim trailing whitespace.................................................Passed
      ruff.....................................................................Passed
      ruff-format..............................................................Passed
      clang-format.............................................................Passed

.. hint::

   If you have a good reason to skip the checks and really have to create a commit without passing the checks, you can skip the pre-commit hooks by adding ``--no-verify`` as option for the ``git commit`` command.

   .. code-block:: console

      $ git commit --no-verify -m 'There is hopefully a proper reason to skip the pre-commit hooks in this commit!'
   
   
   

Create a Pull Request
=====================

After you have done all the changes you wanted and pushed your commits to your own fork, you can create a Pull Request on `github.com <github.com>`__ to 
