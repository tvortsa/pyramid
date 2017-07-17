.. index::
   single: Agendaless Consulting
   single: Pylons
   single: Django
   single: Zope
   single: frameworks vs. libraries
   single: framework

:app:`Pyramid` Введение
===========================

:app:`Pyramid` это Python web приложение *framework*. Он разработан так чтобы упростить создание web приложений. Он open source.

.. sidebar:: Что такое Framework?

   *framework* предоставляет возможности, которые разработчики могут улучшить или расширить. Web application framework предоставляет множество общих потребностей при построении web приложений allowing developers to concentrate only on the parts that are specific to their application.

   Every framework makes choices about how a particular problem should be solved. When developers choose to use a framework, they cede control over the portions of their application that are provided by the framework. It is possible to write a complete web application without any framework, by using Python libraries. In practice, however, it is often more practical to use a framework, so long as your chosen framework fits the requirements of your application.

:app:`Pyramid` придерживается следующих дизацнерских и инженерных принципов:

Simplicity
   :app:`Pyramid` is designed to be easy to use. You can get started even if you don't understand it all. And when you're ready to do more, :app:`Pyramid` will be there for you.

Minimalism
   Out of the box, :app:`Pyramid` provides only the core tools needed for nearly all web applications: mapping URLs to code, security, and serving static assets (files like JavaScript and CSS). Additional tools provide templating, database integration and more. But with :app:`Pyramid` you can *"pay only for what you eat"*.

Documentation
   :app:`Pyramid` is committed to comprehensive and up-to-date documentation.

Speed
  :app:`Pyramid` is designed to be noticeably fast.

Reliability
  :app:`Pyramid` is developed conservatively and tested exhaustively. Our motto is: "If it ain't tested, it's broke".

Openness
  As with Python, the :app:`Pyramid` software is distributed under a `permissive open source license <http://repoze.org/license.html>`_.

.. _why_pyramid:

почему Pyramid?
---------------

In a world filled with web frameworks, why should you choose :app:`Pyramid`\ ?

Modern
~~~~~~

:app:`Pyramid` is fully compatible with Python 3. If you develop a :app:`Pyramid` application today, you can rest assured that you'll be able to use the most modern features of your favorite language. And in the years to come, you'll continue to bed working on a framework that is up-to-dateand forward-looking.

Tested
~~~~~~

Untested code is broken by design. The :app:`Pyramid` community has a strong testing culture and our framework reflects that. Every release of :app:`Pyramid` has 100% statement coverage (as measured by `coverage <http://coverage.readthedocs.io/en/latest/>`_) and 95% decision/condition coverage. (as measured by `instrumental <http://instrumental.readthedocs.io/en/latest/intro.html>`_) It is automatically tested using `Travis <https://travis-ci.org/Pylons/pyramid>`_ and `Jenkins <http://jenkins.pylonsproject.org/job/pyramid/>`_ on supported versions of Python after each commit to its GitHub repository. `Official Pyramid add-ons <https://trypyramid.com/resources-extending-pyramid.html>`_ are held to a similar testing standard.

We still find bugs in :app:`Pyramid`, but we've noticed we find a lot fewer of them while working on projects with a solid testing regime.

Documented
~~~~~~~~~~

The :app:`Pyramid` documentation is comprehensive. We strive to keep our narrative documentation both complete and friendly to newcomers. We also maintain the :ref:`Pyramid Community Cookbook <cookbook:pyramid-cookbook>` of  recipes demonstrating common scenarios you might face. Contributions in the form of improvements to our documentation are always appreciated. And we always welcome improvements to our `official tutorials <html_tutorials>`_ as well as new contributions to our `community maintained tutorials <tutorials:pyramid-tutorials>`_.

Supported
~~~~~~~~~

You can get help quickly with :app:`Pyramid`. It's our goal that no :app:`Pyramid` question go unanswered. Whether you ask a question on IRC, on the Pylons-discuss mailing list, or on StackOverflow, you're likely to get a reasonably prompt response.

:app:`Pyramid` is also a welcoming, friendly space for newcomers. We don't tolerate "support trolls" or those who enjoy berating fellow users in our support channels. We try to keep it well-lit and new-user-friendly.

.. seealso::

    See also our `#pyramid IRC channel <https://webchat.freenode.net/?channels=pyramid>`_, our `pylons-discuss mailing list <https://groups.google.com/forum/#!forum/pylons-discuss>`_, and :ref:`support-and-development`.

.. _what_makes_pyramid_unique:

Что делает Pyramid уникальным
-----------------------------

Существует множество инструментов для веб-разработки. Зачем бы кто-то захотел использовать :app:`Pyramid` ?  Что делает :app:`Pyramid` уникальным?

C :app:`Pyramid` вы можете создавать очень маленькие приложения не требующие больших знаний. Узнав немного больше, вы сможете писать и очень большие приложения тоже. :app:`Pyramid` позволит вам быстро стать продуктивным, и будет расти вместе с вами. Он не будет удерживать вас, когда ваше приложение будет небольшим, И он не будет мешать вам, когда ваше приложение станет большим. Остальные фрэймворки, похоже, попадают в две неперекрывающиеся категории: которые поддерживают "маленькие приложения" и те что разработаны под "большие приложения".

Мы не считаем, что вам нужно сделать этот выбор. Вы не можете точно знать, насколько большин станет ваше приложение. Вы, конечно, не должны переписывать небольшое приложение в другом фрэймворке, когда оно станет "слишком большим". Хорошо спроектированный фрэймворк должен быть одинаково хорош и для больших приложений и для малых. :app:`Pyramid` как раз такой фрэймворк.

:app:`Pyramid` provides a set of features that are unique among Python web frameworks. Others may provide some, but only :app:`Pyramid` provides them all, in one place, fully documented, and *à la carte* without needing to pay for the whole banquet.


Построение одно-файлового приложеия
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Вы можете написать на :app:`Pyramid` приложение существующее только в одном Python файле. Такое приложение легко понять, поскольку все находится в одном месте. Его легко развернуть, поскольку вам не нужно много знать о Python пакетах. :app:`Pyramid` позволяет делать практически все что подразумевают под *microframeworks* очень похожими способами.

.. literalinclude:: helloworld.py

.. seealso::

    See also :ref:`firstapp_chapter`.

Настройка приложений декораторами
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` позволяет сохранить конфигурацию прямо рядом с вашим кодом. Таким образом, вам не нужно переключать файлы, чтобы увидеть вашу конфигурацию. НАпример:

.. code-block:: python

   from pyramid.view import view_config
   from pyramid.response import Response

   @view_config(route_name='fred')
   def fred_view(request):
       return Response('fred')

Но, использование :app:`Pyramid` декораторов конфигурации не меняют ваш код. Он остается легко-расширяемым, тестируемым, и повторно используемым. Вы можете тестировать ваш код так как будто декораторов в нем нет. Вы можете сказать движку игнорировать некоторые декораторы. Вы даже можете использовать императивный стиль для написания вашей конфигурации, полностью пропустив декораторы.

.. seealso::

    See also :ref:`mapping_views_using_a_decorator_section`.

Генерауия URLов приложения
~~~~~~~~~~~~~~~~~~~~~~~~~~

Динамические web приложения генерируют URLы которые могут изменяться в зависимости от того что вы просматриваете. :app:`Pyramid` предоставляет гибкий, последовательный, простой в использовании инструмент генерации URLs. Используя который, вы можете менять вашу конфигурацию не боясь нарушить ссылки на веб-страницах.

.. seealso::

    See also :ref:`generating_route_urls`.

Статические активы
~~~~~~~~~~~~~~~~~~~

Web часто требуют JavaScript, CSS, images и проч. так называемых *статических активов*. :app:`Pyramid` предоставляет гибкий инструментарий для обслуживания этого типа файлов. Вы можете обслуживать их напрямую из :app:`Pyramid`, или хостить их на внешнем сервере или CDN (content delivery network). Either way, :app:`Pyramid` can help you to generate URLs so you can change where your files come from without changing any code.

.. seealso::

    See also :ref:`static_assets_section`.

Интерактивная разработка
~~~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` Может автоматически обнаруживать изменения, которые вы вносите в файлы шаблонов и кода, так что мваши изменения сразу доступны в браузере. Вы можете отлаживать используя простой старый вызов ``print()``, который будет отображаться на вашей консоли.

:app:`Pyramid` имеет тулбар отладки который позволяет вам видеть информацию о том, как ваше приложение работает прямо в браузере. See configuration, installed packages, SQL queries, logging statements and more.

Когда в приложении случается ошибка, интерактивный отладчик позволяет вам to poke around из браузера, чтобы узнать, что произошло.

Чтобы использовать тулбар отладки :app:`Pyramid` , соберите ваш проект с :app:`Pyramid` :term:`cookiecutter`.

.. seealso::

    See also :ref:`debug_toolbar`.

Мощная отладка
~~~~~~~~~~~~~~~~

Когда все плохо, :app:`Pyramid` дает вам мощные способы решения проблемы.

Вы можете настроить :app:`Pyramid` чтобы оно печатало полезную информацию в консоли. Настройка ``debug_notfound`` отображает информацию о URLах которые не соответствуют. Опция ``debug_authorization`` предоставляет полезные сообщения о том, почему вам не разрешено делать то, что вы только что пробовали.

:app:`Pyramid` also has command line tools to help you verify your configuration. You can use ``proutes`` and ``pviews`` to inspect how URLs are connected to your application code.

.. seealso::

    See also :ref:`debug_authorization_section`, :ref:`command_line_chapter`,
    and :doc:`../pscripts/index`

Extend your application
~~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` add-ons extend the core of the framework with useful abilities. There are add-ons available for your favorite template language, SQL and NoSQL databases, authentication services and more.

Поддерживаемые :app:`Pyramid` плагины придерживаются тех же требовательных стандартов, что и сам фрэймворк. Вы найдете их полностью протестированными и хорошо документированными.

.. seealso::

    See also https://trypyramid.com/resources-extending-pyramid.html

Написание ваших видов, *вашим* способом
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Фундаментальная задача для любого фрэймворка отображение URLs на код. В :app:`Pyramid`, этот код называется :term:`view callable`. View callables могут быть функциями, методами класса или даже экземплярами callable сласса. Вы можете выбрать подход, который наилучшим образом подходит для вашего случая использования. Независимо от вашего выбора, :app:`Pyramid` относится к ним одинаково. Вы можете передумать в любое время без каких-либо последствий. Нет никаких искусственных различий между различными подходами.

Вот view callable объявленный как функция:

.. code-block:: python
   :linenos:

   from pyramid.response import Response
   from pyramid.view import view_config

   @view_config(route_name='aview')
   def aview(request):
       return Response('one')

А вот несколько видов объявленные как методы класса:

.. code-block:: python
   :linenos:

   from pyramid.response import Response
   from pyramid.view import view_config

   class AView(object):
       def __init__(self, request):
           self.request = request

       @view_config(route_name='view_one')
       def view_one(self):
           return Response('one')

       @view_config(route_name='view_two')
       def view_two(self):
           return Response('two')

.. seealso::

    See also :ref:`view_config_placement`.

.. _intro_asset_specs:

Поиск *ваших* статических активов
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Во многих web frameworks, статические активы требуемые приложению, хранятся в глобальном общем месте, "папке *static* ". Другие используют lookup scheme, как упорядоченный набор шаблонных каталогов. Оба эти подхода имеют проблемы, когда дело доходит до настройки.

:app:`Pyramid` использует другой подход. Статические активы локализуются с использованием *asset specifications*, Строки, содержащие ссылки как на имя пакета Python, так и на имя файла или каталога, e.g. ``MyPackage:static/index.html``. Эти спецификации используются для шаблонов, JavaScript и CSS, файлов переводов, и любой другой статический ресурс, связанный с пакетом. Используя спецификации активов, :app:`Pyramid` Упрощает расширение вашего приложения с помощью других пакетов, не беспокоясь о конфликтах.

Что будет если другой :app:`Pyramid` пакет используемый вами предоставляет вам актив, необходимый для настройки? Возможно, этот шаблон страницы нуждается в улучшенном HTML, или вы хотите обновить некий CSS. С asset specifications вы можете переопределить активы из других пакетов с помощью простых оберток.

Пример: :ref:`asset_specifications` и :ref:`overriding_assets_section`.

Использование *ваших* шаблонов
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

В :app:`Pyramid`, задача по созданию ``Response`` лежит на :term:`renderer`. Любая система шаблонов—Mako, Chameleon, Jinja2—может быть отрендерена. Фактически, есть пакеты для каждой из этих систем. Но если вы предпочитаете использовать другую, существует структурированный API существует возможность создания рендерера с использованием вашей любимой системы шаблонов. Вы можете использовать систему шаблонов понятную *вам*, а не ту что требует framework.

What's more, :app:`Pyramid` does not make you use a single templating system exclusively.  You can use multiple templating systems, even in the same project.

Example: :ref:`templates_used_directly`.

Написание тестируемых видов
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Когда вы используете :term:`renderer` с вашим view callable, вы освобождаетесь от необходимости возвращать "webby" ``Response`` объект. Вместо этого ваши представления могут возвращать простой словарь Python. :app:`Pyramid` позаботится о рендеринге информации в этом словаре ``Response`` за вас. В результате ваши виды легче тестируются, поскольку вам не нужно парсить HTML для оценки результатов. :app:`Pyramid` делает его легким для написания модульных тестов для ваших представлений вместо того, чтобы требовать от вас использования функциональных тестов.

.. index::
   pair: renderer; явный вызов
   pair: view renderer; явный вызов

.. _example_render_to_response_call:

Например, типичный веб-framework может вернуть ``Response`` объект из ``render_to_response`` вызова:

.. code-block:: python
    :linenos:

    from pyramid.renderers import render_to_response

    def myview(request):
        return render_to_response('myapp:templates/mytemplate.pt', {'a':1},
                                  request=request)

А вы * можете * сделать это в :app:`Pyramid`, кроме того, вы можете вернуть словарь Python:

.. code-block:: python
    :linenos:

    from pyramid.view import view_config

    @view_config(renderer='myapp:templates/mytemplate.pt')
    def myview(request):
        return {'a':1}

Путем настройки вашего представления на использование рендера, вы сообщаете :app:`Pyramid` использовать ``{'a':1}`` Словарь и указанный шаблон ответа от вашего имени.

Строка передавалась как ``renderer=`` выше это :term:`asset specification`. Asset specifications широко используется в :app:`Pyramid`. Они обеспечивают более надежную настройку. См :ref:`intro_asset_specs` больше информации.

Пример: :ref:`renderers_chapter`.

Использование событий для координирования действий
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Создавая web приложения, часто бывает важно, чтобы ваш код выполнялся в определенной точке жизненного цикла запроса. В :app:`Pyramid`, вы можете выполнить это, используя *subscribers* и *events*.

Например, у вас может быть задание, которое нужно выполнять каждый раз, когда ваше приложение обрабатывает новый запрос. :app:`Pyramid` испускает ``NewRequest`` событие на этом этапе жизненного цикла обработки запросов. Вы можете зарегистрировать свой код в качестве подписчика на это событие, используя чисто декларативный стиль:

.. code-block:: python

    from pyramid.events import NewRequest
    from pyramid.events import subscriber

    @subscriber(NewRequest)
    def my_job(event):
        do_something(event.request)

Система событий :app:`Pyramid`\ может быть расширена. Если вам нужно, вы можете создавать собственные события и отправлять их с помощью системы событий :app:`Pyramid`\ . Тогда любой, кто работает с вашим приложением, может подписаться на ваши события и скоординировать свой код с вашими.

Пример: :ref:`events_chapter` и :ref:`event_types`.

Build international applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` ships with internationalization-related features in its core: localization, pluralization, and creating message catalogs from source files and templates.  :app:`Pyramid` allows for a plurality of message catalogs via the use of translation domains.  You can create a system that has its own translations without conflict with other translations in other domains.

Example: :ref:`i18n_chapter`.

Build efficient applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` provides an easy way to *cache* the results of slow or expensive views. You can indicate in view configuration that you want a view to be cached:

.. code-block:: python

    @view_config(http_cache=3600) # 60 minutes
    def myview(request):
        # ...

:app:`Pyramid` will automatically add the appropriate ``Cache-Control`` and ``Expires`` headers to the response it creates.

See the :meth:`~pyramid.config.Configurator.add_view` method's ``http_cache`` documentation for more information.

Build fast applications
~~~~~~~~~~~~~~~~~~~~~~~

The :app:`Pyramid` core is fast. It has been engineered from the ground up for speed. It only does as much work as absolutely necessary when you ask it to get a job done. If you need speed from your application, :app:`Pyramid` is the right choice for you.

Example: https://blog.curiasolutions.com/pages/the-great-web-framework-shootout.html

Хранение данных сессии
~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` имеет встроенную поддержку HTTP сессий, поэтому вы можете ассоциировать данные с конкретными пользователями между запросами. Многие другие фрэймворки также поддерживают сеансы. Но :app:`Pyramid` позволяет подключать произвольную систему сессий. Пока ваша система соответствует документированному интерфейсу, вы можете оставить ее вместо предоставленной системы.

В настоящее время существует пакет привязки для сторонней системы Redis для сеансов, которая выполняет именно это. But if you have a specialized need (perhaps you want to store your session data in MongoDB), you can.  You can even switch between implementations without changing your application code.

Пример: :ref:`sessions_chapter`.

Управлять проблемами изящно
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Никто не создает безошибочный код. :app:`Pyramid` предоставляет способ обработки исключений, с которыми сталкивается ваш код. Так :term:`exception view` это особый случай view который автоматически вызывается, когда возникает особый тип исключения, не обрабатываясь приложением.

Например, вы можете зарегистрировать exception view для :exc:`Exception` exception type, оторый поймает * все * исключения, и представит симпатичную страницу «ок, нам неловко».  Или вы можете зарегистрировать представление исключения только для определенных исключений для конкретных приложений. Вы можете сделать это, когда файл не найден или когда у пользователя нет разрешения на выполнение чего-либо. В первом случае вы можете показать красивую страницу «Не найдено»; В последнем случае вы можете указать форму входа в систему.

Пример: :ref:`exception_views`.

И многое, многое другое...
~~~~~~~~~~~~~~~~~~~~~~~~~~~

:app:`Pyramid` Был построен с рядом других сложных функций дизайна, которые делают его адаптируемым. Узнайте больше о них ниже.

.. toctree::
   :maxdepth: 2

   advanced-features





.. index::
   single: Pylons Project

What Is The Pylons Project?
---------------------------

:app:`Pyramid` is a member of the collection of software published under the Pylons Project.  Pylons software is written by a loose-knit community of contributors.  The `Pylons Project website <https://pylonsproject.org>`_ includes details about how :app:`Pyramid` relates to the Pylons Project.

.. index::
   single: pyramid and other frameworks
   single: Zope
   single: Pylons
   single: Django
   single: MVC

:app:`Pyramid` and Other Web Frameworks
---------------------------------------

The first release of :app:`Pyramid`\ 's predecessor (named :mod:`repoze.bfg`) was made in July of 2008.  At the end of 2010, we changed the name of :mod:`repoze.bfg` to :app:`Pyramid`.  It was merged into the Pylons project as :app:`Pyramid` in November of that year.

:app:`Pyramid` was inspired by :term:`Zope`, :term:`Pylons` (version 1.0), and :term:`Django`.  As a result, :app:`Pyramid` borrows several concepts and features from each, combining them into a unique web framework.

Similar to :term:`Zope`, :app:`Pyramid` applications may easily be extended. If you work within the constraints of the framework, you can produce applications that can be reused, modified, or extended without needing to modify the original application code. :app:`Pyramid` also inherits the concepts of :term:`traversal` and declarative security from Zope.

Similar to :term:`Pylons` version 1.0, :app:`Pyramid` is largely free of policy. It makes no assertions about which database or template system you should use. You are free to use whatever third-party components fit the needs of your specific application. :app:`Pyramid` also inherits its approach to :term:`URL dispatch` from Pylons.

Similar to :term:`Django`, :app:`Pyramid` values extensive documentation. In addition, the concept of a :term:`view` is used by :app:`Pyramid` much as it would be by Django.

Other Python web frameworks advertise themselves as members of a class of web frameworks named `model-view-controller <https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller>`_ frameworks. The authors of :app:`Pyramid` do not believe that the MVC pattern fits the web particularly well. However, if this abstraction works for you, :app:`Pyramid` also generally fits into this class.
