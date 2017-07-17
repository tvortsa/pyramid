Продвинутые фичи дизайна :app:`Pyramid`
=======================================

:app:`Pyramid` Была построена с нуля, чтобы избежать проблем, от которых пострадали другие фрэймворки.

Вам не нужны Singleton`ы
-------------------------

Вы когда-нибудь боролись с параметризацией в файле Django ``settings.py`` для нескольких инсталляций одного и того же Django приложения? Have you ever needed to monkey-patch a framework fixture to get it to behave properly for your use case? Вы когда-нибудь пытались развернуть свое приложение с помощью асинхронного сервера и не смогли?

Все эти проблемы являются симптомами :term:`mutable` :term:`global state`, также известного как :term:`import time` :term:`side effect`\ s и возникают из-за использования такой структуры данных как :term:`singleton`.

:app:`Pyramid` написан так, что вы не сталкиваетесь с такими проблемами. Можно даже запустить несколько копий *одного и того же* :app:`Pyramid` приложения настроенное по-разному в рамках одного процесса Python. Это делаетзапуск :app:`Pyramid` в средах с общим хостингом.

Упростите код вида с помощью предикатов
---------------------------------------

Сколько раз вы обнаруживали, что начинаете логику своего кода вида с чего-то подобного:

.. code-block:: python
    :linenos:

    if request.user.is_authenticated:
        # делаем одно
    else:
        # делаем другое

В отличие от многих других систем, :app:`Pyramid` позволяет связать несколько видов с одним маршрутом. Например, вы можете создать маршрут с паттерном ``/items`` и когда маршрут совпадает, Вы можете отправить запрос на один вид, если метод запроса - GET, другое представление, если метод запроса POST, и так далее.

:app:`Pyramid` использует систему :term:`view predicate`\ чтобы реализовать это. Согласование метода запроса - одна из основных вещей, которую вы можете сделать с помощью :term:`view predicate`. Вы также можете связывать представления с другими параметрами запроса, такими как элементы в строке запроса, заголовком Accept, является ли запрос AJAX (XHR) запросом или нет, и множеством другого.

В нашем примере выше вы можете сделать это вместо того:

.. code-block:: python
    :linenos:

    @view_config(route_name="items", effective_principals=pyramid.security.Authenticated)
    def auth_view(request):
        # делаем одно

    @view_config(route_name="items")
    def anon_view(request):
        # делаем другое

Этот подход позволяет вам разрабатывать более простой, понятный и более понятный код вида.

.. seealso::

   See also :ref:`view_configuration_parameters`.

Прекратите беспокоиться о транзакциях
-------------------------------------

:app:`Pyramid`\ 's :term:`cookiecutter`\ s render projects которая включает систему *transaction management*.  Когда вы используете эту систему, вы можете перестать беспокоиться о том, когда совершать изменения, :app:`Pyramid` обрабатывает его для вас. Система будет зафиксирована в конце запроса или прервана, если возникло исключение.

Почему это хорошо? Представьте ситуацию, когда вы вручную вносите изменения в свой уровень персистентности. Очень вероятно, что другой код фрэймворка будет запущен *после* того как ваши изменения закончены. Если в этом другом случае произошла ошибка, вы можете легко завершить работу с несогласованными данными, если вы не очень осторожны.

Использование управления транзакциями избавляет вас от необходимости думать об этом. Либо запрос завершается успешно, и все изменения совершаются, либо нет, и все изменения прерваны.

Менеджмент транзакциями в :app:`Pyramid`\ расширяем, Поэтому вы можете синхронизировать транзакции между несколькими базами данных или базами данных разных типов. Это также позволяет вам делать такие вещи, как условно отправлять электронную почту, если совершена транзакция, но в остальных случаях "молчать".

.. seealso::

   See also :ref:`bfg_sql_wiki_tutorial` (Обратите внимание на отсутствие команд фиксации в любом месте кода приложения).

Перестаньте волноваться по поводу конфигурации
----------------------------------------------

Когда система мала, разумно легко держать все в голове. Но по мере роста систем, конфигурация становится более сложной. Ваше приложение может вырасти, чтобы иметь сотни или даже тысячи инструкций конфигурации.

Система конфиграции :app:`Pyramid`\ отслеживает каждое из ваших стэйтов. Если вы случайно добавите два одинаковых, или :app:`Pyramid` не видит смысла в том что означало бы, что оба заявления активны одновременно, он будет громко протестовать во время запуска.

Система конфиграции :app:`Pyramid`\ не тупая. Если вы используете систему :meth:`~pyramid.config.Configurator.include` ,он может автоматически разрешать конфликты самостоятельно. Более локальные заявления предпочтительнее, чем менее локальные. Таким образом, вы можете разумно распределить большие системы на более мелкие.

.. seealso::

   See also :ref:`conflict_detection`.

Составление мощных приложений из простых частей
------------------------------------------------

Структура механизма :app:`Pyramid` :meth:`~pyramid.config.Configurator.include` , он позволяет создавать сложные приложения из нескольких простых пакетов Python. Все инструкции конфигурации, которые могут быть выполнены в вашем главном :app:`Pyramid` приложении также можно использовать в прилагаемых пакетах. Вы можете добавлять views, routes, и subscribers, и даже устанавливать политики авторизации и авторизации.

Если вам нужно, вы можете расширить или переопределить конфигурацию существующего приложения, включив его конфигурацию самостоятельно, а затем изменив ее.


Например, если вы хотите повторно использовать существующее приложение, которое уже имеет кучу маршрутов, просто используйте оператор ``include`` с ``route_prefix``. Все маршруты этого приложения будут доступны, с префиксом по вашему запросу:

.. code-block:: python
    :linenos:

    from pyramid.config import Configurator

    if __name__ == '__main__':
       config = Configurator()
       config.include('pyramid_jinja2')
       config.include('pyramid_exclog')
       config.include('some.other.package', route_prefix='/somethingelse')

.. seealso::

    See also :ref:`including_configuration` and :ref:`building_an_extensible_app`.

Аутентификация пользователей по-своему
-------------------------------------------

:app:`Pyramid` поставляется с предустановленной, протестированной схемой аутентификации и авторизации из коробки. Использование схемы - вопрос конфигурации. Поэтому, если вам нужно изменить подходы позже, вам нужно только обновить свою конфигурацию.

Кроме того, система, которая обрабатывает аутентификацию и авторизацию, является гибкой и подключаемой. Если вы хотите использовать другое надстройку безопасности или определить свой собственный, вы можете. И снова вам нужно только обновить конфигурацию своего приложения, чтобы внести изменения.

.. seealso::

   See also :ref:`enabling_authorization_policy`.

Построение дерева ресурсов
--------------------------

:app:`Pyramid` поддерживает :term:`traversal`, способ отображения URLs на конкретное :term:`resource tree`. Если ваше приложение, естественно, состоит из произвольной иерархии различных типов контента (как CMS или Document Management System), traversal для вас. Если у вас есть требование для высоко-гранулированной модели безопасности ("Jane может редактировать документы в папке *this* , но не *that* one"), может быть мощным подходом.

.. seealso::

   See also :ref:`hello_traversal_chapter` and :ref:`much_ado_about_traversal_chapter`.

Применяйте действия для каждого запроса с помощью Tweens
---------------------------------------------------------

:app:`Pyramid` имеет систему для применения произвольного действия к каждому запросу или ответу, называемому :term:`tween`. Система аналогична концепции WSGI :term:`middleware`, но может быть более полезным, поскольку :term:`tween`\ s запускается в контексте :app:`Pyramid` , и имеет доступ к шаблонам, объектам запросов и другим тонкостям.

Панели отладки :app:`Pyramid`  :term:`tween`, и ``pyramid_tm`` transaction manager.

.. seealso::

   See also :ref:`registering_tweens`.

Возвращайте что хотите из ваших Views
-------------------------------------

Мы показали ранее (in the :doc:`introduction`) как использование :term:`renderer` позволяет вам возвращать простые словари Python из вашего кода view. But some frameworks позволяют возвращать строки или кортежи из view callables. Когда фреймворки допускают это, код выглядит немного красивее, потому что импорта меньше и меньше кода. Сравните например:

.. code-block:: python
    :linenos:

    from pyramid.response import Response

    def aview(request):
        return Response("Hello world!")

To this:

.. code-block:: python
    :linenos:

    def aview(request):
        return "Hello world!"

Выглядит приятнее не так ли?

Из коробки, :app:`Pyramid` приведет к возникновению исключения, если вы попытаетесь запустить второй пример выше. В конце концов, представление должно возвращать ответ, а «явное - лучше, чем неявное».

Но если вы разработчик, которому нравится эстетика простоты, :app:`Pyramid` Обеспечивает способ поддержки такого рода вещей, the :term:`response adapter`\ :

.. code-block:: python
    :linenos:

    from pyramid.config import Configurator
    from pyramid.response import Response

    def string_response_adapter(s):
        response = Response(s)
        response.content_type = 'text/html'
        return response

Новый адаптер ответа зарегистрирован в конфигурации:

.. code-block:: python
    :linenos:

    if __name__ == '__main__':
        config = Configurator()
        config.add_response_adapter(string_response_adapter, str)

Теперь, можете возвращать строки из любого из ваших view callables, e.g.:

.. code-block:: python
    :linenos:

    def helloview(request):
        return "Hello world!"

    def goodbyeview(request):
        return "Goodbye world!"

Можете даже использовать :term:`response adapter` разрешить настраиваемые типы контента и коды возврата:

.. code-block:: python
    :linenos:

    from pyramid.config import Configurator

    def tuple_response_adapter(val):
        status_int, content_type, body = val
        response = Response(body)
        response.content_type = content_type
        response.status_int = status_int
        return response

    def string_response_adapter(body):
        response = Response(body)
        response.content_type = 'text/html'
        response.status_int = 200
        return response

    if __name__ == '__main__':
        config = Configurator()
        config.add_response_adapter(string_response_adapter, str)
        config.add_response_adapter(tuple_response_adapter, tuple)

С этим, оба эти представления будут работать должным образом:

.. code-block:: python
    :linenos:

    def aview(request):
        return "Hello world!"

    def anotherview(request):
        return (403, 'text/plain', "Forbidden")

.. seealso::

   See also :ref:`using_iresponse`.

Использование глобального объекта ответа (Global Response Objects)
------------------------------------------------------------------

Views должен возвращать ответы. Но построение их в виде кода - это обычное дело. И, возможно, зарегистрировать :term:`response adapter` как показано выше, это слишком много работы. :app:`Pyramid` предоставляет также global response.  Вы можете использовать его напрямую если хотите:

.. code-block:: python
    :linenos:

    def aview(request):
        response = request.response
        response.body = 'Hello world!'
        response.content_type = 'text/plain'
        return response

.. seealso::

   See also :ref:`request_response_attr`.

Расширение конфигурации
-----------------------

Возможно синтаксис конфигуратора :app:`Pyramid` кажется вам слегка многословным. Или, возможно, вы хотели бы добавить функцию в конфигурацию, не попросив основных разработчиков изменить сам :app:`Pyramid` ?

You can extend :app:`Pyramid`\ 's :term:`configurator` with your own directives. For example, let's say you find yourself calling :meth:`pyramid.config.Configurator.add_view` repetitively. Usually you can get rid of the boring with existing shortcuts, but let's say that this is a case where there is no such shortcut:

.. code-block:: python
    :linenos:

    from pyramid.config import Configurator

    config = Configurator()
    config.add_route('xhr_route', '/xhr/{id}')
    config.add_view('my.package.GET_view', route_name='xhr_route',
                    xhr=True,  permission='view', request_method='GET')
    config.add_view('my.package.POST_view', route_name='xhr_route',
                    xhr=True, permission='view', request_method='POST')
    config.add_view('my.package.HEAD_view', route_name='xhr_route',
                    xhr=True, permission='view', request_method='HEAD')

Pretty tedious right? You can add a directive to the :app:`Pyramid` :term:`configurator` to automate some of the tedium away:

.. code-block:: python
    :linenos:

    from pyramid.config import Configurator

    def add_protected_xhr_views(config, module):
        module = config.maybe_dotted(module)
        for method in ('GET', 'POST', 'HEAD'):
            view = getattr(module, 'xhr_%s_view' % method, None)
            if view is not None:
                config.add_view(view, route_name='xhr_route', xhr=True,
                                permission='view', request_method=method)

    config = Configurator()
    config.add_directive('add_protected_xhr_views', add_protected_xhr_views)

Once that's done, you can call the directive you've just added as a method of the :term:`configurator` object:

.. code-block:: python
    :linenos:

    config.add_route('xhr_route', '/xhr/{id}')
    config.add_protected_xhr_views('my.package')

Much better!

You can share your configuration code with others, too. Add your code to a Python package. Put the call to :meth:`~pyramid.config.Configurator.add_directive` in a function. When other programmers install your package, they'll be able to use your configuration by passing your function to a call to :meth:`~pyramid.config.Configurator.include`.

.. seealso::

    See also :ref:`add_directive`.

Интроспекция вашего приложения
------------------------------

If you're building a large, pluggable system, it's useful to be able to get a list of what has been plugged in *at application runtime*. For example, you might want to show users a set of tabs at the top of the screen based on a list of the views they registered.

:app:`Pyramid` provides an :term:`introspector` for just this purpose.

Here's an example of using :app:`Pyramid`\ 's :term:`introspector` from within a view:

.. code-block:: python
    :linenos:

    from pyramid.view import view_config
    from pyramid.response import Response

    @view_config(route_name='bar')
    def show_current_route_pattern(request):
        introspector = request.registry.introspector
        route_name = request.matched_route.name
        route_intr = introspector.get('routes', route_name)
        return Response(str(route_intr['pattern']))

.. seealso::

    See also :ref:`using_introspection`.
