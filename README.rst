..
    Make sure to apply any changes to this file to README_RAW.rst as well!

We have made you a wrapper you can't refuse

We have a vibrant community of developers helping each other in our `Telegram group <https://telegram.me/pythontelegrambotgroup>`_. Join us!

*Stay tuned for library updates and new releases on our* `Telegram Channel <https://telegram.me/pythontelegrambotchannel>`_.

Introduction
============

This library provides a pure Python, asynchronous interface for the
`Telegram Bot API <https://core.telegram.org/bots/api>`_.
It's compatible with Python versions **3.7+**.

In addition to the pure API implementation, this library features a number of high-level classes to
make the development of bots easy and straightforward. These classes are contained in the
``telegram.ext`` submodule.

Note
----

Installing both ``python-telegram-bot`` and ``python-telegram-bot-raw`` in conjunction will result in undesired side-effects, so only install *one* of both.

Telegram API support
====================

All types and methods of the Telegram Bot API **6.1** are supported.

Installing
==========

You can install or upgrade ``python-telegram-bot`` via

.. code:: shell

    $ pip install python-telegram-bot --upgrade

To install a pre-release, use the ``--pre`` `flag <https://pip.pypa.io/en/stable/cli/pip_install/#cmdoption-pre>`_ in addition.

You can also install ``python-telegram-bot`` from source, though this is usually not necessary.

.. code:: shell

    $ git clone https://github.com/python-telegram-bot/python-telegram-bot
    $ cd python-telegram-bot
    $ python setup.py install

Dependencies & Their Versions
-----------------------------

``python-telegram-bot`` tries to use as few 3rd party dependencies as possible.
However, for some features using a 3rd party library is more sane than implementing the functionality again.
The dependencies are:

* `httpx ~= 0.23.0 <https://www.python-httpx.org>`_ for ``telegram.request.HTTPXRequest``, the default networking backend
* `tornado~=6.1 <https://www.tornadoweb.org/en/stable/>`_ for ``telegram.ext.Updater.start_webhook``
* `cachetools~=5.2.0 <https://cachetools.readthedocs.io/en/latest/>`_ for ``telegram.ext.CallbackDataCache``
* `APScheduler~=3.9.1 <https://apscheduler.readthedocs.io/en/3.x/>`_ for ``telegram.ext.JobQueue``

``python-telegram-bot`` is most useful when used along with additional libraries.
To minimize dependency conflicts, we try to be liberal in terms of version requirements on the dependencies.
On the other hand, we have to ensure stability of ``python-telegram-bot``, which is why we do apply version bounds.
If you encounter dependency conflicts due to these bounds, feel free to reach out.

Optional Dependencies
---------------------

PTB can be installed with optional dependencies:

* ``pip install python-telegram-bot[passport]`` installs the `cryptography>=3.0 <https://cryptography.io/en/stable>`_ library. Use this, if you want to use Telegram Passport related functionality.
* ``pip install python-telegram-bot[socks]`` installs ``httpx[socks]``. Use this, if you want to work behind a Socks5 server.

Quick Start
===========

Our Wiki contains an `Introduction to the API <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Introduction-to-the-API>`_ explaining how the pure Bot API can be accessed via ``python-telegram-bot``.
Moreover, the `Tutorial: Your first Bot <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Extensions-%E2%80%93-Your-first-Bot>`_ gives an introduction on how chatbots can be easily programmed with the help of the ``telegram.ext`` module.

Resources
=========

- The `package documentation <https://docs.python-telegram-bot.org/>`_ is the technical reference for ``python-telegram-bot``.
  It contains descriptions of all available classes, modules, methods and arguments as well as the `changelog <https://docs.python-telegram-bot.org/changelog.html>`_.
- The `wiki <https://github.com/python-telegram-bot/python-telegram-bot/wiki/>`_ is home to number of more elaborate introductions of the different features of ``python-telegram-bot`` and other useful resources that go beyond the technical documentation.
- Our `examples section <https://docs.python-telegram-bot.org/examples.html>`_ contains several examples that showcase the different features of both the Bot API and ``python-telegram-bot``.
  Even if it is not your approach for learning, please take a look at ``echobot.py``. It is the de facto base for most of the bots out there.
  The code for these examples is released to the public domain, so you can start by grabbing the code and building on top of it.
- The `official Telegram Bot API documentation <https://core.telegram.org/bots/api>`_ is of course always worth a read.

Concurrency
===========

Since v20.0, ``python-telegram-bot`` is built on top of Pythons ``asyncio`` module.
Because ``asyncio`` is in general single-threaded, ``python-telegram-bot`` does currently not aim to be thread-safe.
Noteworthy parts of ``python-telegram-bots`` API that are likely to cause issues (e.g. race conditions) when used in a multi-threaded setting include:

* ``telegram.ext.Application/Updater.update_queue``
* ``telegram.ext.ConversationHandler.check/handle_update``
* ``telegram.ext.CallbackDataCache``
* ``telegram.ext.BasePersistence``
* all classes in the ``telegram.ext.filters`` module that allow to add/remove allowed users/chats at runtime
