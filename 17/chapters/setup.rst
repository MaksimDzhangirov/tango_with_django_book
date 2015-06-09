.. _setup-label:

.. _django-basics:

Основы работы с Django 
========================
Давайте начнем работать с Django! В этой главе мы дадим краткий обзор основ работы с Django. Вы настроите новый проект и новое веб приложение. В конце этой главы Вы будете иметь простую работающую веб страницу, созданную с помощью Django!

Проверка Вашей конфигурации
-----------------------------
Давайте начнем, проверив, что Вы правильно установили Python и Django, и что они имеют подходящую версию для этого учебного пособия. Для этого запустите новую копию терминала и выполните следующую команду.

::
	
	$ python --version
	2.7.5

Она выведет на экран номер версии устанолвенного интерпретатора Python. Если версия, изображенная на экране отличается от ``2.7.5``, Вам необходимо вернуться к Разделу :ref:`installing-software` и проверить, что Вы выполнили все необходимые шаги по установке для Вашей операционной системы.

После проверки версии Python, проверьте Вашу версию установки Django, выполнив следующую команду.

::
	
	$ python -c "import django; print(django.get_version())"
	1.7

Команда опять выполнит код внутри строки, которая вводится за ключем ``-c``. После импорта Django, Вы должны увидеть в терминале ``1.7`` на следующей строке. Если Вы видите другой набор чисел или выводится ``ImportError`` интерпретатором Python, вернитесь в Раздел :ref:`installing-software` или обратитесь к `Документации Django по установке Django <https://docs.djangoproject.com/en/1.7/topics/install/>`_ за дальнейшей информацией. Если Вы обнаружили, что импользуете другую версию Django, то у Вас могут возникнуть проблемы в дальнейшем. Из-за этого стоит удостовериться, что у Вас установлена версия Django 1.7. 

Создание Вашего Django проекта
-------------------------------
Чтобы создать новый Django проект, перейдите в каталог, который Вы используете для создания ``кода`` (т. е., в каталог Вашего ``<рабочего пространства>``), и выполните следующую команду:

``$ django-admin.py startproject tango_with_django_project``

.. note:: В Windows может потребоваться задавать полный путь к скрипту django-admin.py, т. е. ``python c:\python27\scripts\django-admin.py startproject tango_with_django_project`` как предложено в ссылке `StackOverflow <http://stackoverflow.com/questions/8112630/cant-create-django-project-using-command-prompt>`_.

Эта команда вызовет скрипт ``django-admin.py``, который настроит новый Django проект под названием ``tango_with_django_project`` для Вас. Обычно мы добавляем слово ``_project`` в конец названий каталогов наших Django проектов, чтобы точно знать, что они содержат - однако названия Ваших проектов полностью зависят от Вас.

Теперь в вашем рабочем пространстве должен появиться каталог, название которого совпадает с названием Вышего нового проекта ``tango_with_django_project``. Внутри этого только что созданного каталога, вы должны увидеть:

* другой каталог с таким же названием как и Ваш проект, ``tango_with_django_project``; и
* скрипт на языке Python, который называется ``manage.py``.

В этом учебном пособии мы будем называть этот вложенный каталог, *каталогом для настройки проекта*. Внутри этого каталога, находятся четыре Python скрипта. Мы подробно рассмотрим эти скрипты позднее, но пока Вы должны увидеть:

* ``__init__.py``, пустой Python скрипт, наличие которого говорит интерпретатору Python, что этот каталог является Python пакетом;
* ``settings.py``, файл, где хранятся все Ваши настройки Django проекта;
* ``urls.py``, Python скрипт для хранения URL шаблонов Вашего проекта; и 
* ``wsgi.py``, Python скрипт, который поможет запустить Выш сервер для разработки приложения и развернуть Ваш проект на сервере, который будет использоваться для работы приложения.

.. note:: Каталог для настройки проекта создается для новых Django проектов, начиная с версии 1.4. Некоторым создание двух каталогов с одинаковыми именами может показаться странным, но это было сделано для того, чтобы отделить компоненты, связанные с проектом от входящих в него отдельных приложений.

В каталоге проекта, Вы должны увидеть файл, который называется ``manage.py``. Мы будем постоянно вызывать этот скрипт при разработке нашего проекта, поскольку он содержит ряд команд, которые Вы можете использовать, для развития Вашего Django проекта. Например, ``manage.py`` позволяет Вам запустить встроенный в Django сервер разработки для проверки, проделанной Вами работы, и выполнения команд, связанных с базой данных. Вы будете очень часто использовать этот скрипт во время цикла разработки приложения.

.. note:: Смотри Django документацию, чтобы узнать больше о `скриптах django-admin.py и manage.py <https://docs.djangoproject.com/en/1.7/ref/django-admin/#django-admin-py-and-manage-py>`_.

Теперь попытайтесь использовать скрипт ``manage.py``, выполнив следующую команду.

``$ python manage.py runserver``

Выполнение этой команды приведет к тому, что Django инициализирует свой "облегченный" сервер для разработки. Вы должны увидеть в окне Вашего терминала текст, подобный указанному ниже:

::
	
	$ python manage.py runserver

	System check identified no issues (0 silenced).

	You have unapplied migrations; your app may not work properly until they are applied.
	Run 'python manage.py migrate' to apply them.

	October 01, 2014 - 19:49:05
	Django version 1.7c2, using settings 'tango_with_django_project.settings'
	Starting development server at http://127.0.0.1:8000/
	Quit the server with CONTROL-C.
	
	
	
::

	$ python manage.py migrate
	
	Operations to perform:
	  Apply all migrations: admin, contenttypes, auth, sessions
	Running migrations:
	  Applying contenttypes.0001_initial... OK
	  Applying auth.0001_initial... OK
	  Applying admin.0001_initial... OK
	  Applying sessions.0001_initial... OK
	
	
#TODO(leifos): add description of migrate command: from django tutorial: The migrate command looks at the INSTALLED_APPS setting and creates any necessary database tables according to the database settings in your mysite/settings.py file and the database migrations shipped with the app (we’ll cover those later). You’ll see a message for each migration it applies. If you’re interested, run the command-line client for your database and type \dt (PostgreSQL), SHOW TABLES; (MySQL), or .schema (SQLite) to display the tables Django created.
	
	
	

Теперь откройте Ваш любимый веб-браузер и введите URL http://127.0.0.1:8000/ [#f1]_. Вы должны увидеть веб страницу подобную той, который показана на Рисунке :num:`fig-django-dev-server-firstrun`. 

.. _fig-django-dev-server-firstrun:

.. figure:: ../images/django-dev-server-firstrun.png
	:figclass: align-center
	
	Снимок экрана начальной страницы Django, которую Вы видите при запуске сервера для разработки первый раз.

Вы можете остановить сервер для разработки в любой момент, нажав ``CTRL + C`` в Вашем окне терминала. Если Вы хотите запустить сервер для разработки на другом порте или открыть доступ к нему пользователям на других машинах, Вы можете сделать это, введя необязательные вспомогательные параметры. Рассмотрим следующую команду:

``$ python manage.py runserver <ip_адрес_Вашей_машины>:5555``

Выполнение этой команды приведет к тому, что сервер для разработки будет отвечать на входящие запросы по TCP порту 5555. Также необходимо заменить <ip_адресс_Вашей_машины> на IP адрес Вашего компьютера. 

При выборе порта, вероятно Вы не сможете использовать TCP порт 80, поскольку он обычно зарезервирован для HTTP траффика. Также любой порт меньше 1024 считается `привилегированным <http://www.w3.org/Daemon/User/Installation/PrivilegedPorts.html>`_ Вашей операционной системой.

Хотя Вы не будете использовать облегченный сервер для разработки при развертывании Вашего приложения, иногда желательно иметь возможность продемонстрировать Ваше приложение на компьютере коллеги. Запуская сервер с IP адресом Вашей машины, позволит другим обратиться к нему как ``http://<your_machines_ip_address>:<port>/`` и просмотреть Ваше веб приложение. Конечно такая возможность будет зависеть от того как настроена Ваша локальная сеть. Существующие прокси серверы или файрволы должны быть настроены соответствующим образом, чтобы такой способ работал. Обратитесь к администратору локальной сети, которую Вы используте, если Вы не можете получить доступ к серверу для разработки удаленно.

.. note:: Скрипты ``django-admin.py`` и ``manage.py`` содержат множество полезных, экономящих время функцональных возможностей. ``django-admin.py`` позволяет создавать новые проекты и приложения наряду с другими командами. Внутри Вашего каталога с проектом, ``manage.py`` позволяет решать задачи администрирования только внутри Вашего проекта. Чтобы узнать возможности каждого скрипта, просто выполните его без каких-либо аргументов. В  `официальной документации по Django дается подробный список и пояснение к каждой возможной команде <https://docs.djangoproject.com/en/1.7/ref/django-admin/>`_, которую Вы можете вводить для этих скриптов.

Если Вы используете систему контроля версий, сейчас стоит осуществить коммит тех изменений, которые Вы сделали в вашем рабочем пространстве. Обратитесь к ссылке :ref:`Ускоренный курс по GIT <git-crash-course>`, если Вы забыли команды и последовательность шагов, которые необходимо осуществить для этого.

Создание Django приложения
-----------------------------
A Django project is a collection of *configurations* and *applications* that together make up a given web application or website. One of the intended outcomes of using this approach is to promote good software engineering practices. By developing a small series of applications, the idea is that you can theoretically drop an existing application into a different Django project and have it working with minimal effort. Why reinvent the wheel if it's already there? [#f2]_

A Django application exists to perform a particular task. You need to create specific applications that are responsible for providing your site with particular kinds of functionality. For example, we could imagine that a project might consist of several applications including a polling app, a registration app, and a specific content related app. In another project, we may wish to re-use the polling and registration apps and use them with to dispatch different content. There are many Django applications you can `download <https://code.djangoproject.com/wiki/DjangoResources#Djangoapplicationcomponents>`_ and use in your projects. Since we are getting started, we'll kick off by walking through how to create your own application.

To start, create a new application called *Rango*. From within your Django project directory (e.g. ``<workspace>/tango_with_django_project``), run the following command.

::
	
	$ python manage.py startapp rango

The ``startapp`` command creates a new directory within your project's root. Unsurprisingly, this directory is called ``rango`` - and contained within it are another five Python scripts:

- another ``__init__.py``, serving the exact same purpose as discussed previously;
- models.py, a place to store your application's data models - where you specify the entities and relationships between data;
- tests.py, where you can store a series of functions to test your application's code; and
- views.py, where you can store a series of functions that take a clients's requests and return responses.
- admin.py, where you can register your models so that you can benefit from some Django machinery which creates an admin interface for you (see #TODO(leifos):add link to admin chapter)


``views.py`` and ``models.py`` are the two files you will use for any given application, and form part of the main architectural design pattern employed by Django, i.e. the *Model-View-Template* pattern. You can check out `the official Django documentation <https://docs.djangoproject.com/en/1.7/intro/overview/>`_ to see how models, views and templates relate to each other in more detail.

Before you can get started with creating your own models and views, you must first tell your Django project about your new application's existence. To do this, you need to modify the ``settings.py`` file, contained within your project's configuration directory. Open the file and find the ``INSTALLED_APPS`` tuple. Add the ``rango`` application to the end of the tuple, which should then look like the following example.

.. code-block:: python

	INSTALLED_APPS = (
	    'django.contrib.admin',
	    'django.contrib.auth',
	    'django.contrib.contenttypes',
	    'django.contrib.sessions',
	    'django.contrib.messages',
	    'django.contrib.staticfiles',
	    'rango',
	)

Verify that Django picked up your new application by running the development server again. If you can start the server without errors, your application was picked up and you will be ready to proceed to the next step.

Создание Представления
---------------
With our Rango application created, let's now create a simple view. For our first view, let's just send some simple text back to the client - we won't concern ourselves about using models or templates just yet.

In your favourite IDE, open the file ``views.py``, located within your newly created ``rango`` application directory. Remove the comment ``# Create your views here.`` so that you now have a blank file.

Теперь добавьте следующий код.

.. code-block:: python

	from django.http import HttpResponse
	
	def index(request):
	    return HttpResponse("Rango says hey there world!")

Breaking down the three lines of code, we observe the following points about creating this simple view.

* We first import the `HttpResponse <https://docs.djangoproject.com/en/1.7/ref/request-response/#django.http.HttpResponse>`_ object from the ``django.http`` module.
* Each view exists within the ``views.py`` file as a series of individual functions. In this instance, we only created one view - called ``index``.
* Each view takes in at least one argument - a `HttpRequest <https://docs.djangoproject.com/en/1.7/ref/request-response/#django.http.HttpRequest>`_ object, which also lives in the ``django.http`` module.  Convention dictates that this is named ``request``, but you can rename this to whatever you want if you so desire.
* Each view must return a HttpResponse object. A simple HttpResponse object takes a string parameter representing the content of the page we wish to send to the client requesting the view.

With the view created, you're only part of the way to allowing a user to access it. For a user to see your view, you must map a `Uniform Resources Locator (URL) <http://en.wikipedia.org/wiki/Uniform_resource_locator>`_ to the view.

Mapping URLs
------------
Within the ``rango`` application directory, we now need to create a new file called ``urls.py``. The contents of the file will allow you to map URLs for your application (e.g. ``http://www.tangowithdjango.com/rango/``) to specific views. Check out the simple ``urls.py`` file below.

.. code-block:: python

	from django.conf.urls import patterns, url
	from rango import views

	urlpatterns = patterns('',
		url(r'^$', views.index, name='index'))

This code imports the relevant Django machinery that we use to create URL mappings. Importing the ``views`` module from ``rango`` also provides us with access to our simple view implemented previously, allowing us to reference the view in the URL mapping we will create.

To create our mappings, we use a `tuple <http://en.wikipedia.org/wiki/Tuple>`_. For Django to pick your mappings up, this tuple *must* be called ``urlpatterns``. The ``urlpatterns`` tuple contains a series of calls to the ``django.conf.urls.url()`` function, with each call handling a unique mapping. In the code example above, we only use ``url()`` once, so we have therefore defined only one URL mapping. The first parameter we provide to the ``django.conf.urls.url()`` function is the regular expression ``^$``, which matches to an empty string. Any URL supplied by the user that matches this pattern means that the view ``views.index()`` would be invoked by Django. The view would be passed a ``HttpRequest`` object as a parameter, containing information about the user's request to the server. We also make use of the optional parameter to the ``url()`` function, ``name``, using the string ``'index'`` as the associated value.

.. note:: You might be thinking that matching a blank URL is pretty pointless - what use would it serve? When the URL pattern matching takes place, only a portion of the original URL string is considered. This is because our Django project will first process the original URL string (i.e. ``http://www.tangowithdjango.com/rango/``). Once this has been processed, it is removed, with the remained being passed for pattern matching. In this instance, there would be nothing left - so an empty string would match!

.. note:: The ``name`` parameter is optional to the ``django.conf.urls.url()`` function. This is provided by Django to allow you to distinguish one mapping from another. It is entirely plausible that two separate URL mappings expressions could end calling the same view. ``name`` allows you to differentiate between them - something which is useful for *reverse URL matching.* Check out `the Official Django documentation on this topic <https://docs.djangoproject.com/en/1.7/topics/http/urls/#naming-url-patterns>`_ for more information.

You may have seen that within your project configuration directory a ``urls.py`` file already exists. Why make another? Technically, you can put *all* the URLs for your project's applications within this file. However, this is considered bad practice as it increases coupling on your individual applications. A separate ``urls.py`` file for each application allows you to set URLs for individual applications. With minimal coupling, you can then join them up to your project's master ``urls.py`` file later.

This means we need to configure the ``urls.py`` of our project ``tango_with_django_project`` and connect up our main project with our Rango application.

How do we do this? It's quite simple. Open the project's ``urls.py`` file which is located inside your project configuration directory. As a relative path from your workspace directory, this would be the file ``<workspace>/tango_with_django_project/tango_with_django_project/urls.py``. Измените кортеж ``urlpatterns`` как показано ниже.

.. code-block:: python
	

	urlpatterns = patterns('',
	    # Examples:
	    # url(r'^$', 'tango_with_django_project_17.views.home', name='home'),
	    # url(r'^blog/', include('blog.urls')),

	    url(r'^admin/', include(admin.site.urls)),
	    url(r'^rango/', include('rango.urls')), # ADD THIS NEW TUPLE!
	)

The added mapping looks for url strings that match the patterns ``^rango/``. When a match is made the remainder of the url string is then passed onto and handled by ``rango.urls`` (which we have already configured). This is done with the help of the ``include()`` function from within ``django.conf.urls``. Think of this as a chain that processors the URL string - as illustrated in Figure :num:`fig-url-chain`. In this chain, the domain is stripped out and the remainder of the url string (``rango/``) is passed on to tango_with_django project, where it finds a match and strips away ``rango/`` leaving and empty string to be passed on to the application rango. Rango now tries to match the empty string, which it does, and this then dispatches the ``index()`` view that we created.

Перезапустите сервер для разработки Django и откройте страницу ``http://127.0.0.1:8000/rango``. Если Вы сделали всё правильно, выдолжны увидеть текст ``Rango says hello world!``. Он должен выглядеть как на снимке экрана, показанном на Рисунке :num:`fig-rango-hello-world`.

.. _fig-url-chain:

.. figure:: ../images/url-chain.svg
	:figclass: align-center
	
	An illustration of a URL, showing how the different parts of the URL are the responsibility of different ``url.py`` files.

.. _fig-rango-hello-world:

.. figure:: ../images/rango-hello-world.png
	:figclass: align-center

	Снимок экрана браузера Google Chrome, в котором показана наша первая веб страница, созданная с помощью Django. Hello, Rango!

Within each application, you will create a number of URL to view mappings. This initial mapping is quite simple. As we progress, we will create more sophisticated mappings that using allow the URLs to be parameterised.

It's important to have a good understanding of how URLs are handled in Django. If you are still bit confused or would like to know more check out the `official Django documentation on URLs <https://docs.djangoproject.com/en/1.7/topics/http/urls/>`_ for further details and further examples.

.. note:: The URL patterns use `regular expressions <http://en.wikipedia.org/wiki/Regular_expression>`_ to perform the matching. It is worthwhile familiarising yourself on how to use regular expressions in Python. The official Python documentation contains a `useful guide on regular expressions <http://docs.python.org/2/howto/regex.html>`_ , while regexcheatsheet.com provides a `neat summary of regular expressions <http://regexcheatsheet.com/>`_.

Basic Workflows
---------------
What you've just learnt in this chapter can be succinctly summarised into a list of actions. Here, we provide these lists for the two distinct tasks you have performed. You can use this section for a quick reference if you need to remind yourself about particular actions.

Создание нового Django проекта
.............................
#. Чтобы создать проект, выполните команду ``python django-admin.py startproject <name>``, где ``<name>`` - это название проекта, который Вы хотите создать.

Создание нового Django приложения
.................................
#. To create a new application run, ``$ python manage.py startapp <appname>``, where ``<appname>`` is the name of the application you wish to create.
#. Tell your Django project about the new application by adding it to the ``INSTALLED_APPS`` tuple in your project's ``settings.py`` file.
#. In your project ``urls.py`` file, add a mapping to the application.
#. In your application's directory, create a ``urls.py`` file to direct incoming URL strings to views.
#. In your application's ``view.py``, create the required views ensuring that they return a ``HttpResponse`` object.

Упражнения
---------
Congratulations! You have got Rango up and running. This is a significant landmark in working with Django. Creating views and mapping URLs to views is the first step towards developing more complex and usable web applications. Now try the following exercises to reinforce what you've learnt.

* Revise the procedure and make sure you follow how the URLs are mapped to views.
* Now create a new view called ``about`` which returns the following: ``Rango says here is the about page.``
* Now map the this view to ``/rango/about/``. For this step, you'll only need to edit the ``urls.py`` of the rango application.
* Revise the ``HttpResponse`` in the ``index`` view to include a link to the about page.
* In the ``HttpResponse`` in the ``about`` view include a link back to the main page.
* If you haven't done so already, it is a good point to go off an complete part one of the official `Django Tutorial <https://docs.djangoproject.com/en/1.7/intro/tutorial01/>`_. 

Подсказки к упражнениям
.....
If you're struggling to get the exercises done, the following hints will hopefully provide you with some inspiration on how to progress.

* Your ``index`` view should be updated to include a link to the ``about`` view. Keep it simple for now - something like ``Rango says: Hello world! <br/> <a href='/rango/about'>About</a>`` will suffice. We'll be going back later to improve the presentation of these pages.
* The regular expression to match ``about/`` is ``r'^about/'`` - this will be handy when thinking about your URL pattern.
* The HTML to link back to the index page is ``<a href="/rango/">Index</a>``. The link uses the same structure as the link to the ``about`` page shown above.

.. rubric:: Примечания
.. [#f1] Предполагается, что вы используете IP адресс 127.0.0.1 и порт 8000 при запуске Вашего Django веб-сервера для разработки. Если Вы явно не указываете порт, который будет использоваться для запуска сервера для разработки, Django по умолчанию использует порт 8000.

.. [#f2] There are many applications available out there that you can use in your project. Take a look at `PyPI <https://pypi.python.org/pypi?%3Aaction=search&term=django&submit=search>`_ and `Django Packages <https://www.djangopackages.com/>`_ to search for reusable apps which you can drop into your projects.
