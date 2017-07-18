Pyramid
=======

.. image:: https://travis-ci.org/Pylons/pyramid.png?branch=master
        :target: https://travis-ci.org/Pylons/pyramid
        :alt: master Travis CI Status

.. image:: https://readthedocs.org/projects/pyramid/badge/?version=master
        :target: https://docs.pylonsproject.org/projects/pyramid/en/master
        :alt: master Documentation Status

.. image:: https://img.shields.io/badge/irc-freenode-blue.svg
        :target: https://webchat.freenode.net/?channels=pyramid
        :alt: IRC Freenode

`Pyramid <https://trypyramid.com/>`_ это небольшой, быстрый, приземленный, open
source Python web framework. Он делает разработку web-приложений  и их развертку,
веселой предсказуемой и продуктивной.

.. code-block:: python

   from wsgiref.simple_server import make_server
   from pyramid.config import Configurator
   from pyramid.response import Response

   def hello_world(request):
       return Response('Hello %(name)s!' % request.matchdict)

   if __name__ == '__main__':
       with Configurator() as config:
           config.add_route('hello', '/hello/{name}')
           config.add_view(hello_world, route_name='hello')
           app = config.make_wsgi_app()
       server = make_server('0.0.0.0', 8080, app)
       server.serve_forever()

Pyramid это проект проекта `Pylons  <https://pylonsproject.org>`_.

Поддержка и документация
-------------------------

См `Pyramid Support и Development
<https://docs.pylonsproject.org/projects/pyramid/en/latest/#support-and-development>`_
for documentation, reporting bugs, and getting support.

Разработка и содействие
---------------------------

См `HACKING.txt <https://github.com/Pylons/pyramid/blob/master/HACKING.txt>`_ and
`contributing.md <https://github.com/Pylons/pyramid/blob/master/contributing.md>`_
гадлайны по юнит-тестам, доп. фичам, стилю кодинга, and updating
documentation when developing in or contributing to Pyramid.

Лицензия
--------

Pyramid is offered under the BSD-derived `Repoze Public License
<http://repoze.org/license.html>`_.

Authors
-------

Pyramid is made available by `Agendaless Consulting <https://agendaless.com>`_
and a team of `contributors
<https://github.com/Pylons/pyramid/graphs/contributors>`_.
