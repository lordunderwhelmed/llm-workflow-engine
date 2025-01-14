.. _configuration_doc:

===============================================
Configuration
===============================================

*Configuration is optional, default values will be used if no configuration profile is
provided.*


-----------------------------------------------
Viewing the current configuration
-----------------------------------------------


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
From the command line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Run the program with the ``config`` argument:

.. code-block:: bash

   lwe config


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
From a running instance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

   /config

This will show all the current configuration settings, the most important ones for installation are:

* **Config dir:** Where configuration files are stored
* **Current profile:** (shown in the ``Profile configuration`` section)
* **Config file:** The configuration file current being used
* **Data dir:** The data storage directory

From a running instance, you can also view just a portion of the configuration by providing a
filter argument:

.. code-block:: bash

   /config model

...will show just the ``model`` portion of the configuration

A very handy filter is ``/config database``, which will show just the currently configured
database connection string.


-----------------------------------------------
Sample configuration
-----------------------------------------------

The default configuation settings can be seen in
`config.sample.yaml <https://github.com/llm-workflow-engine/llm-workflow-engine/blob/main/config.sample.yaml>`_
-- the file is well-commented with descriptions of the settings.

**DON'T just copy this file as your configuration!**

Instead, use it as a reference to tweak the configuration to your liking.

*NOTE:* Not all settings are available on all backends. See the example config for more information.

Command line arguments overrride custom configuration settings, which override default
configuration settings.

-------------------------------------------------
Editing the configuration for the current profile
-------------------------------------------------

1. Start the program: ``lwe``
2. Open the profile's configuration file in an editor: ``/config edit``
3. Edit file to taste and save
4. Restart the program

-----------------------------------------------
Configuring model properties
-----------------------------------------------

To change the properties of a particular LLM model, use the ``/model`` command:

.. code-block:: bash

   /model model_name gpt-3.5-turbo
   /model temperature 1.0

The ``/model`` command works within the models of the currently loaded :ref:`provider <Provider plugins>`.

*NOTE: The attributes that a particular model accepts are beyond the scope of this
document. While some attributes can be displayed via command completion in the
shell, you are advised to consult the API documentation for the specific provider
for a full list of available attributes and their values.*

-----------------------------------------------
Using browser backend
-----------------------------------------------

**This backend is deprecated, and may be removed in a future release.**

**NOTE:** Support will not be provided for using the ``BrowserBackend`` class of this backend directly.

The browser backend runs a headless browser, providing CLI access to https://chat.openai.com

In your profile configuration file, you'll want to make sure the backend is set to the following in order to use the browser backend:

.. code-block:: yaml

   backend: 'browser'

To tweak the configuration for the current profile, see :ref:`Configuration`

Install a browser in playwright (if you haven't already). The program will use firefox by default.

.. code-block:: bash

   playwright install firefox

Start up the program in `install` mode:

.. code-block:: bash

   lwe install

This opens up a browser window. Log in to ChatGPT in the browser window, walk through all the intro screens, then exit program.

.. code-block:: bash

   1> /exit

Restart the program without the `install` parameter to begin using it.

.. code-block:: bash

   lwe

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Using ChatGPT Plugins (alpha)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Officially approved ChatGPT plugins can be configured for use with the browser backend.

**NOTE:** This requires your OpenAI login account to have access to ChatGPT plugins.

To use plugins:

1. You must use a model that supports plugins: ``/model model_name gpt-4-plugins``
2. Browse the plugins: ``/chatgpt-plugins``, or a filter the full list by a phrase, ``/chatgpt-plugins youtube``
3. To enable the plugin by default, add the plugin ID to the ``browser.plugins`` list in your configuration file:

   .. code-block:: yaml

      browser:
        plugins:
          - plugin-d1d6eb04-3375-40aa-940a-c2fc57ce0f51

4. You can also dynamically enable/disable plugins, see the help for ``/chatgpt-plugin-enable`` and ``/chatgpt-plugin-disable``

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Using ChatGPT with browsing (alpha)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ChatGPT with browsing can be used with the browser backend.

**NOTE:** This requires your OpenAI login account to have access to ChatGPT with browsing.

To use ChatGPT with browsing, you must use a model that supports browsing: ``/model model_name gpt-4-browsing``
