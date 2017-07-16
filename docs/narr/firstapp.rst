.. index::
   single: hello world program

.. _firstapp_chapter:

Создаем ваше первое :app:`Pyramid` приложение
==============================================

В этой главе, мы пробежим по созданию простого :app:`Pyramid`
приложения. По завершении мы создадим приложение, и рассмотрим как оно работает.
Подразумевается что вы уже установили :app:`Pyramid` .
Если нет, посмотрите раздел :ref:`installing_chapter` .

.. _helloworld_imperative:

Hello World
-----------

Это одно из самых простых приложений :app:`Pyramid` :

.. literalinclude:: helloworld.py
   :linenos:

Вставим этот код в скрипт Python с именем ``helloworld.py`` 
и выполним интерпретатором Python где :app:`Pyramid` установленный
софт, как HTTP server стартующий на TCP порту 8080.

Для UNIX:

.. code-block:: bash

   $ $VENV/bin/python helloworld.py

Для Windows:

.. code-block:: doscon

   c:\> %VENV%\Scripts\python helloworld.py

Эта команда ничего не возвращает и не выводит в консоль. Когда вы посетите порт
 8080 браузером по URL ``/hello/world``, сервер просто обслужит выведя текст
"Hello world!". Если ваше приложение запущено локально, используйте
`<http://localhost:8080/hello/world>`_ в браузере чтобы отобразить результат.

Каждый раз когда вы переходите по URL обслуживается приложением в браузере, в консоль
выводится строка логирования с именем хоста, датой, временем, типом запроса и путем
и доп. инф.  Этот вывод делает wsgiref сервер который вы используете для работы приложения.
Это лог "access log" из Apache совмещающий logging формат в консоли.

Нажмите ``Ctrl-C`` (или ``Ctrl-Break`` в Windows) чтобыостановить приложение.

Теперь мы имеем начальные представления о том как работает приложение,
давайте разберем по кусочкам.

Imports
~~~~~~~

Скрипт ``helloworld.py`` использует следующий набор операторов импорта:

.. literalinclude:: helloworld.py
   :lineno-match:
   :lines: 1-3

Скрипт импортирует :class:`~pyramid.config.Configurator` из модуля
:mod:`pyramid.config`.  Экземпляр класса
:class:`~pyramid.config.Configurator` в последствии используется для конфигурации
:app:`Pyramid` приложения.

Как и в других Python web фрэймворках, :app:`Pyramid` использует :term:`WSGI`
протокол для соединения приложения и web сервера вместе. Сервер
:mod:`wsgiref` используется в этом примере как WSGI сервер для удобства,
поскольку поставляется в стандартной библиотеке Python.

Этот скрипт также импортирует класс :class:`pyramid.response.Response` для
последующего использования. Экземпляр этого класса будет использован для создания
web-ответа.

Объявление вызываемого вида (View Callable Declarations)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

После операторов импорта, следует функция
``hello_world``.

.. literalinclude:: helloworld.py
   :lineno-match:
   :pyobject: hello_world

Функция принимает один аргумент (``request``) и он возвращает экземпляр
класса :class:`pyramid.response.Response`.  Единственный аргумент в конструкторе
класса (class' constructor) это строка вычисленная из parameters matched в URL. 
Это значение становится телом ответа.

Эту функцию называют :term:`view callable`.  View callable принимает один аргумент,
``request``.  Ожидается что это объект :term:`response`. 
View callable не обязан быть функцией; она может быть представлена
через другой тип объекта, класс или экземпляр, но для наших целей функция подходит лучше.

View callable всегда вызывается с объектом :term:`request`.  Объект request
прдставляет HTTP запрос посланный в приложение :app:`Pyramid` через активный :term:`WSGI` сервер.

View callable должен вернуть объект :term:`response` потому что объект response
обладает всей необходимой информацией для формирования актуального HTTP ответа;
Этот объект конвертируется в текст сервером :term:`WSGI` 
который вызывает Pyramid и этот объект возвращается в вызывающий браузер.
Возвращая ответ, каждый view callable creatсоздает экземпляр класса
:class:`~pyramid.response.Response`.  В функции ``hello_world``, строка передается
как тело для ответа.

.. index::
   single: imperative configuration
   single: Configurator
   single: helloworld (imperative)

.. _helloworld_imperative_appconfig:

Конфигурация приложения
~~~~~~~~~~~~~~~~~~~~~~~~~

В скрипте, следующий код представляет *конфигурацию* этого простого приложения.
Приложение конфигурировано с использованием прежде объявленных операторов импорта
и функции definitions, размещенных в операторе ``if``:

.. literalinclude:: helloworld.py
   :lineno-match:
   :lines: 9-15

Разберем это по частям.

Конструкция конфигуратора
~~~~~~~~~~~~~~~~~~~~~~~~~

.. literalinclude:: helloworld.py
   :lineno-match:
   :lines: 9-10

Строка ``if __name__ == '__main__':`` представляет идиому Python:
код внутри выражения if не вызывается если не вызывается, если скрипт 
содержащий этот код, запускается непосредственно из командной строки операционной системы.
Например, если файл ``helloworld.py`` содержит все тело скрипта, код в выражении ``if``
вызывается только если ``python helloworld.py`` выполнялся из командной строки.

Использование условия ``if`` необходимая или по-крайней мере лучшая практика
поскольку код Python в ``.py`` файлах может импортироваться опреатором Python ``import``
в другой ``.py`` файл который называют *modules*.  Используя идиому ``if __name__ ==
'__main__':`` , скрипт определяет что код в выражении ``if`` не должен выполняться
если этот модуль импортирован из другого; код в блоке ``if`` должен запускаться только
если скрипт был запущен непосредственно.

Строка ``with Configurator() as config:`` создает экземпляр класса
:class:`~pyramid.config.Configurator` используя :term:`context manager`.  
Итоговый объект ``config`` представляет API которое скрипт использует для конфигурирования
этой части :app:`Pyramid` приложения. Методы, вызванные конфигуратором приведут к регистрации
в :term:`application registry` ассоциированными с приложением.

.. _adding_configuration:

Добавление конфигурации
~~~~~~~~~~~~~~~~~~~~~~~

.. literalinclude:: helloworld.py
   :lineno-match:
   :lines: 11-12

Первая строка тут вызывает метод :meth:`pyramid.config.Configurator.add_route`
, который регистрирует :term:`route` в сопоставление пути URL который начинается на
``/hello/`` followed by a string.

Ворая строка регистрирует функцию ``hello_world`` как :term:`view
callable` и убеждается чтобы онбыл вызван когда роут ``hello`` совпадает.

.. index::
   single: make_wsgi_app
   single: WSGI application

Создание WSGI приложения
~~~~~~~~~~~~~~~~~~~~~~~~~

.. literalinclude:: helloworld.py
   :lineno-match:
   :lines: 13

После конфигурирования видов и завершения конфигурации, скрипт создает WSGI
*application* методом :meth:`pyramid.config.Configurator.make_wsgi_app`.
Вызов ``make_wsgi_app`` подразумевает что вся конфигурация завершена
(тоесть все методы для конфигуратора , которые настраивают виды
и другие настройки, были выполнены).  Метод ``make_wsgi_app``
возвращает объект приложения :term:`WSGI` который может быть использован
любым WSGI сервером для представления приложения в requestor. :term:`WSGI`
это протокол который позволяет серверу to talk to Python applications. 
Мы не касаемся :term:`WSGI` в этой книге, но вы можете узнать о нем из
документации `documentation <https://wsgi.readthedocs.io/en/latest/>`_.

Объект приложения :app:`Pyramid`, в частности, является экземпляром класса
представляющего :app:`Pyramid` :term:`router`.  Он имеет ссылку на
:term:`application registry` which resulted from method calls to the
configurator used to configure it.  Роутер :term:`router` consults the registry to
obey the policy choices made by a single application.  These policy choices
were informed by method calls to the :term:`Configurator` made earlier; in our
case, the only policy choices made were implied by calls to its ``add_view``
and ``add_route`` methods.

Обслуживание WSGI приложений
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. literalinclude:: helloworld.py
   :lineno-match:
   :lines: 14-15

Наконец, действительно подаем запрос на обслуживание запуском WSGI
сервера.  Для чего используем :mod:`wsgiref` ``make_server`` для создания сервера.
Мы передаем в качестве первого аргумента ``'0.0.0.0'``, что означает
"прослушивать все TCP интерфейсы".  По умолчанию, HTTP сервер слушает только
интерфейс ``127.0.0.1`` , что проблематично если вы запускаете сервер на удаленной
системе и хотите получить к нему доступ web браузером через локальную систему.
Мы также указываем номер TCP порта для прослушивания, передавая 8080, 
в качестве второго аргумента. 
Последний аргумент это объект ``app`` (:term:`router`), который является приложением
которое мы хотим обслуживать.  
Наконец мы вызываем метод сервера ``serve_forever``, который запускает главный цикл 
который будет ожидать запросы из внешнего мира.

Когда эта строка вызывается, тогда сервер начинает прослушивание TCP порта 8080.
Сервер будет обрабатывать запросы все время, пока мы не остановим его
убивая процесс который его запускает (обычно нажатием ``Ctrl-C`` или
``Ctrl-Break`` в котором мы его запускали).

Заключение
~~~~~~~~~~

Our hello world application is one of the simplest possible :app:`Pyramid`
applications, configured "imperatively".  We can see that it's configured
imperatively because the full power of Python is available to us as we perform
configuration tasks.

References
----------

For more information about the API of a :term:`Configurator` object, see
:class:`~pyramid.config.Configurator` .

For more information about :term:`view configuration`, see
:ref:`view_config_chapter`.
