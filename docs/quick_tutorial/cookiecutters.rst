.. _qtut_cookiecutters:

=================================================
Прелюдия: Быстрый старт проекта с Cookiecutters
=================================================

Чтобы упростить процесс запуска проекта, Pylons Project предоставляет :term:`cookiecutter`\ который генерирует простые :app:`Pyramid` проекты по шаблонам проектов. Эти cookiecutters устанавливают :app:`Pyramid` и его зависимости. Мы по-прежнему будем охватывать многие темы разработки веб-приложений, используя :app:`Pyramid`, но хорошо знать его возможности. Эта прелюдия демонстрирует как запустить проект :app:`Pyramid` web приложения используя ``cookiecutter``.


Цели
==========

- Использовать cookiecutter для создания нового проекта.

- Запустить приложение :app:`Pyramid` и посетить его web браузером.


Шаги
=====

#.  Установите cookiecutter в virtual environment.

    .. code-block:: bash

        $VENV/bin/pip install cookiecutter

#.  Используем cookiecutter ``pyramid-cookiecutter-starter`` для создания стартового проекта :app:`Pyramid` в текущей папке, entering values at the prompts as shown below for the following command.

    .. code-block:: bash

        $ $VENV/bin/cookiecutter gh:Pylons/pyramid-cookiecutter-starter --checkout master

    If prompted for the first item, accept the default ``yes`` by hitting return.

    .. code-block:: text

        Вы клонировали ~/.cookiecutters/pyramid-cookiecutter-starter прежде.
        Удалить и переклонировать это? [yes]: yes
        project_name [Pyramid Scaffold]: cc_starter
        repo_name [cc_starter]: cc_starter
        Select template_language:
        1 - jinja2
        2 - chameleon
        3 - mako
        Choose from 1, 2, 3 [1]: 1

#.  We then run through the following commands.

    .. code-block:: bash

        # Change directory into your newly created project.
        $ cd cc_starter
        # Create a new virtual environment...
        $ python3 -m venv env
        # ...where we upgrade packaging tools...
        $ env/bin/pip install --upgrade pip setuptools
        # ...and into which we install our project.
        $ env/bin/pip install -e .

#.  Запуск приложения с помощью :app:`Pyramid`'s ``pserve`` команды at the
    project's (generated) configuration file:

    .. code-block:: bash

        $ env/bin/pserve development.ini --reload

    На старте, ``pserve`` логирует некоторый вывод:

    .. code-block:: text

        Starting subprocess with file monitor
        Starting server in PID 73732.
        Serving on http://localhost:6543
        Serving on http://localhost:6543

#. Откройте http://localhost:6543/ в вашем браузере.

Анализ
=======

Rather than starting from scratch, a cookiecutter can make it easy to get a Python
project containing a working :app:`Pyramid` application. The Pylons Project provides `several cookiecutters <https://github.com/Pylons?q=pyramid-cookiecutter>`_.

``pserve`` is :app:`Pyramid`'s application runner, separating operational details from
your code. When you install :app:`Pyramid`, a small command program called ``pserve``
is written to your ``bin`` directory. This program is an executable Python
module. It is passed a configuration file (in this case, ``development.ini``).
