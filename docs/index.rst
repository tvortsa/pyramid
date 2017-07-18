.. _index:

=========================
 Pyramid Web Framework
=========================

:app:`Pyramid` это небольшой, быстрый, приземленный веб-фрэймворк для Python. 
Он разработан как часть проекта `Pylons Project <https://pylonsproject.org>`_.
Лицензирован под `BSD-like лицензией <http://repoze.org/license.html>`_.

Вот простейшее приложение :app:`Pyramid` :

.. literalinclude:: narr/helloworld.py

После установки :app:`Pyramid` запустите это приложение, посетите браузером
`<http://localhost:8080/hello/world>`_ , и увидите текст
``Hello, world!`` Прочтите :ref:`firstapp_chapter` чтобы узнать как работает это приложение.


.. _getting_started:

Приступаем
===============

Если вы новичок в Pyramid, у нас есть несколько ресурсов для ускоренного ознакомления.

.. toctree::
   :hidden:

   quick_tour
   quick_tutorial/index

* :doc:`quick_tour` дает обзор основных функций Pyramid,
  и раскрывает немного больше.

* :doc:`quick_tutorial/index` похож на Quick Tour, но в формате уроков,
   с несколько более глубоким рассмотрением каждой темы и рабочим кодом.

* Нравится обучение на примерах? Посетите официальный :ref:`html_tutorials` и
   community-contributed :ref:`Pyramid Tutorials
  <tutorials:pyramid-tutorials>` and :ref:`Pyramid Community Cookbook
  <cookbook:pyramid-cookbook>`.

* Получить помощь по настройке Pyramid, можно тут :ref:`installing_chapter`.

* Need help?  See :ref:`Support and Development <support-and-development>`.


.. _html_tutorials:

Уроки
=========

Официальные уроки рассказывают как использовать :app:`Pyramid` для построения
различных типов приложений, и как их развертывать :app:`Pyramid` на разных платформах.

.. toctree::
   :maxdepth: 1

   tutorials/wiki2/index
   tutorials/wiki/index
   tutorials/modwsgi/index


.. _support-and-development:

Поддержка и разработка
=======================

Сайт `Pyramid  <https://trypyramid.com/resources.html>`_ основная точка входа в :app:`Pyramid` ресурсы по поддержке
development information.

To report bugs, use the `issue tracker
<https://github.com/Pylons/pyramid/issues>`_.

If you've got questions that aren't answered by this documentation, contact the
`Pylons-discuss maillist
<https://groups.google.com/forum/#!forum/pylons-discuss>`_ or join the
`#pyramid IRC channel
<https://webchat.freenode.net/?channels=pyramid>`_.

Browse and check out tagged and trunk versions of :app:`Pyramid` via the
`Pyramid GitHub repository <https://github.com/Pylons/pyramid/>`_. To check out
the trunk via ``git``, use either command:

.. code-block:: text

  # If you have SSH keys configured on GitHub:
  git clone git@github.com:Pylons/pyramid.git
  
  # Otherwise, HTTPS will work, using your GitHub login:
  git clone https://github.com/Pylons/pyramid.git

To find out how to become a contributor to :app:`Pyramid`, please see `How to Contribute Source Code and Documentation <https://pylonsproject.org/community-how-to-contribute.html>`_.


.. _html_narrative_documentation:

Narrative Документация
=======================

Narrative документация в форме главы, объясняющая, как использовать :app:`Pyramid`.

.. toctree::
   :maxdepth: 2

   narr/introduction
   narr/install
   narr/firstapp
   narr/configuration
   narr/project
   narr/startup
   narr/router
   narr/urldispatch
   narr/views
   narr/renderers
   narr/templates
   narr/viewconfig
   narr/assets
   narr/webob
   narr/sessions
   narr/events
   narr/environment
   narr/logging
   narr/paste
   narr/commandline
   narr/i18n
   narr/vhosting
   narr/testing
   narr/resources
   narr/hellotraversal
   narr/muchadoabouttraversal
   narr/traversal
   narr/security
   narr/hybrid
   narr/subrequest
   narr/hooks
   narr/introspector
   narr/extending
   narr/advconfig
   narr/extconfig
   narr/cookiecutters
   narr/scaffolding
   narr/upgrading
   narr/threadlocals
   narr/zca


API документация
=================

Всесторонний справочный материал для каждого публичного API exposed by
:app:`Pyramid`:

.. toctree::
   :maxdepth: 1
   :glob:

   api/index
   api/*


``p*`` Scripts Documentation
============================

``p*`` scripts included with :app:`Pyramid`.

.. toctree::
   :maxdepth: 1
   :glob:

   pscripts/index
   pscripts/*


Change History
==============

.. toctree::
   :maxdepth: 1

   whatsnew-1.9
   whatsnew-1.8
   whatsnew-1.7
   whatsnew-1.6
   whatsnew-1.5
   whatsnew-1.4
   whatsnew-1.3
   whatsnew-1.2
   whatsnew-1.1
   whatsnew-1.0
   changes


Design Documents
================

.. toctree::
   :maxdepth: 1

   designdefense


Copyright, Trademarks, and Attributions
=======================================

.. toctree::
   :maxdepth: 1

   copyright


Typographical Conventions and Style Guide
=========================================

.. toctree::
   :maxdepth: 1

   typographical-conventions


Index and Glossary
==================

* :ref:`glossary`
* :ref:`genindex`
* :ref:`search`


.. toctree::
   :hidden:

   glossary

