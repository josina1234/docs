Releasing Debian Packages
#########################

.. note::

   This section is targeted at the maintainers of our repositories and is not relevant for anyone else.

.. _new-release-for-package:

Create a new Release for an Existing Package
============================================

The basic steps are

#. generate a changelog
#. bump the package version
#. create and push a new tag for that version

After that the `buildbot <https://buildbot.hippocampus-robotics.net>`__ will try to generate a new debian package and will update the `HippoCampus Repository <https://repositories.hippocampus-robotics.net/>`__.

There are convenience tools to perform the above mentioned steps, so the commands we need to exectute are the following:

.. code-block:: console

   $ cd <REPOSITORY>

.. code-block:: console

   $ catkin_generate_changelog \
   && git add CHANGELOG.rst \
   && git commit -m 'updated changelog' \
   && catkin_prepare_release

That's it!

Create a Release for a new Package
==================================

This requires some additional steps as it involves updating the buildbot to make sure it builds the release.

#. Add the new package to the list of repositories in the `master.cfg <https://github.com/HippoCampusRobotics/buildbot/blob/main/basedir/master.cfg>`__ in the `buildbot <https://github.com/HippoCampusRobotics/buildbot>`__ repository.

   .. note::

      Currently only repositories directly representing a ros package are supported.
      Support for multiple packages per repository could be enabled by updating the buildbot config to handle these cases.

#. Restart the buildbot instace on the buildbot server

   .. code-block:: console

      $ buildbot restart basedir

   .. note::

      If there are currently builds beeing processed, the buildbot master will not exit before they are completed.
      In this case, we will get the message

      .. code-block:: console

         $ buildbot restart basedir
         never sawy process go away

      We can either wait until it has completed (probably preferable) or if we do not care about the running builds, kill the ``twistd`` process.

#. Add the key for the package to our `rosdep file <https://github.com/HippoCampusRobotics/hippo_infrastructure/blob/main/rosdep-jazzy.yaml>`__ in our `infrastructure repository <https://github.com/HippoCampusRobotics/hippo_infrastructure>`__ (otherwise ``rosdep`` will not be able to resolve dependencies on the new repository).

#. Now execute the same steps as for :ref:`existing packages <new-release-for-package>`. The only difference is to append ``--all`` to the ``catkin_generate_changelog`` command so it becomes

   .. code-block:: console

      $ catkin_generate_changelog --all
   
   
