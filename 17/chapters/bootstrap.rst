.. _bootstrap-chapter:

Использование Bootstrapp в приложении Rango
===========================================
В этой главе мы стилизуем приложение Rango c помощью набора инструментов *Twitter Bootstrap 3.2*. Мы не будем вдаваться в подробности работы Bootstrap, а будем предполагать, что Вы знакомы с CSS. Если нет - просмотрите CSS главу, чтобы понять основы, а затем прочитайте какие-нибудь учебные пособия по Bootstrap. Даже, если не знакомы с CSS Вы должны суметь выполнить задания из этого раздела, объединив новые знания с полученными ранее.

Для начала перейдем на сайт `Bootstrap 3.2.0 website <http://getbootstrap.com/>`_ - там приведен образец кода и примеры различных элементов, показано как стилизовать их добавив соответствующие теги стилей и т. д. На сайте Bootstrap также дается множество `образцовых макетов <http://getbootstrap.com/getting-started/#examples>`_, на основе которых мы можем спроектировать свой.

Мы считаем, что `стиль dashboard <http://getbootstrap.com/examples/dashboard/>`_ лучше всего удовлетворяет нашим потребностям с учетом макета Rango, т. е., он содержит верхнее меню, боковую панель (которую мы будем использовать для отображения категорий) и панель для основного содержимого. HTML код с сайта Bootstrap, необходимо немного доработать, прежде чем мы сможем его использовать. Мы уже сделали это, поэтому получившийся HTML код, который Вы можете скопировать, показан ниже:

* Были заменены все ссылки типа ``../../`` на ``http://getbootstrap.com``
* Была заменена ссылка на ``dashboard.css`` с относительной на абсолютную - ``http://getbootstrap.com/examples/dashboard/dashboard.css``
* Удалена форма поиска из верхней навигационной панели
* Удалено всё несущественное содержимое из HTML и заменено на ``{% block body_block %}{% endblock %}``
* Элементу title присвоено ``<title>Rango - {% block title %}How to Tango with Django!{% endblock %}</title>``
* Изменено название проекта на ``Rango``.
* Добавлены ссылки на главную страницу, страницу входа в систему, регистрации и т. д. в верхнюю навигационную панель.
* Добавлен боковой блок, т. е., ``{% block side_block %}{% endblock %}``.


Новый базовый шаблон
--------------------

.. code-block:: html

	<!DOCTYPE html>
	<html lang="en">
	  <head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <meta name="viewport" content="width=device-width, initial-scale=1">
	    <meta name="description" content="">
	    <meta name="author" content="">
	    <link rel="icon" href="http://getbootstrap.com/favicon.ico">

	    <title>Rango - {% block title %}How to Tango with Django!{% endblock %}</title>

	    <link href="http://getbootstrap.com/dist/css/bootstrap.min.css" rel="stylesheet">
	    <link href="http://getbootstrap.com/examples/dashboard/dashboard.css" rel="stylesheet">

	    <!--[if lt IE 9]>
	      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
	      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
	    <![endif]-->
	  </head>

	  <body>

	    <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
	      <div class="container-fluid">
	        <div class="navbar-header">
	          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target=".navbar-collapse">
	            <span class="sr-only">Toggle navigation</span>
	            <span class="icon-bar"></span>
	            <span class="icon-bar"></span>
	            <span class="icon-bar"></span>
	          </button>
	          <a class="navbar-brand" href="/rango/">Rango</a>
	        </div>
	        <div class="navbar-collapse collapse">
	          <ul class="nav navbar-nav navbar-right">
	                <li><a href="{% url 'index' %}">Home</a></li>
		            {% if user.is_authenticated %}
		                <li><a href="{% url 'restricted' %}">Restricted Page</a></li>
		                <li><a href="{% url 'auth_logout' %}?next=/rango/">Logout</a></li>
		                <li><a href="{% url 'add_category' %}">Add a New Category</a></li>
		            {% else %}
		                <li><a href="{% url 'registration_register' %}">Register Here</a></li>
		                <li><a href="{% url 'auth_login' %}">Login</a></li>
		            {% endif %}
					<li><a href="{% url 'about' %}">About</a></li>

		      </ul>
	        </div>
	      </div>
	    </div>

	    <div class="container-fluid">
	      <div class="row">
	        <div class="col-sm-3 col-md-2 sidebar">
	     	  	{% block side_block %}{% endblock %}
		
	        </div>
	        <div class="col-sm-9 col-sm-offset-3 col-md-10 col-md-offset-2 main">
	           <div>
	     	  	{% block body_block %}{% endblock %}
		        </div>
	        </div>
	      </div>
	    </div>

	    <!-- Bootstrap core JavaScript
	    ================================================== -->
	    <!-- Placed at the end of the document so the pages load faster -->
	    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
	    <script src="http://getbootstrap.com/dist/js/bootstrap.min.js"></script>
	    <!-- IE10 viewport hack for Surface/desktop Windows 8 bug -->
	    <script src="http://getbootstrap.com/assets/js/ie10-viewport-bug-workaround.js"></script>
	  </body>
	</html>

Если Вы внимательно посмотрите на исходный HTML код макета, то заметите, что большая часть структуры создается тегами ``<div>``. По сути страница разбита на две части - верхнюю навигационную панель и главную панель, которые обозначаются двумя ``<div class="container-fluid">``. В раздел с навигационной панелью мы вставили все ссылки на разные части нашего веб сайта. Внутри главной панели находятся две колонки: одна для ``side_block``, а другая для ``body_block``.

Быстрое изменение стиля
-----------------------
Вставьте в Ваш файл ``base.html`` вышеприведенный HTML код (предполагается, что Вы используетет пакет  django-registration-redux, в противном случае Вам необходимо обновить теги URL шаблонов). Перезагрузите Ваше приложение. Очевидно, что Вы должны быть подключены к Интернету, чтобы загрузить CSS, Javascript и другие требуемые файлы. Заметьте, насколько улучшился вид Вашего приложения всего лишь после одного изменения. Посетите разные страницы. Поскольку все они наследуют базовую страницу, они будут выглядеть намного лучше. Не идеально, но намного лучше.

.. note:: Вы можете скачать все необходимые файлы и сохранить их в каталоге для статических файлов. В этом случае просто внесите изменения в базовый шаблон, создав ссылки на статически файлы, сохраненные локально.

Теперь после настройки ``base.html``, можно начать улучшать приложение Rango, просмотрев элементы Bootstrap и выбрав наиболее подходящие для наших страниц.

Давайте обновим шаблон ``about.html``, добавив в него заголовок для страницы (http://getbootstrap.com/components/#page-header). Согласно примеру нам необходимо заключить тег h1 в ``<div>`` с классом ``class="page-header"``:

.. code-block:: html
	
	{% extends 'base.html' %}

	{% load staticfiles %}

	{% block title %}About{% endblock %}

	{% block body_block %}
	    <div class="page-header">
			<h1>About</h1>
	            </div>
		    <div>
		    <p></strong>.</p>

		    <img  width="90" height="100" src="{% static "images/rango.jpg" %}" alt="Picture of Rango" /> <!-- New line -->
		    </div>
	{% endblock %}

	

	

.. _fig-about-page-before:

.. figure:: ../images/ch4-rango-about.png
	:figclass: align-center

	Снимок экрана страницы About без нового стиля.

#TODO(leifos):update this screen shot.


.. _fig-about-page-after:

.. figure:: ../images/ch11-bootstrap-about.png
	:figclass: align-center

	Снимок экрана страницы About после применения Bootstrap стилизации.
	
	
#TODO(leifos):update this screen shot.

Добавьте в каждый шаблон заголовок для страницы. Не забудьте обновить все шаблоны в ``rango`` и ``registration``. Хотя приложение стало выглядеть намного лучше, всё ещё необходимо внести изменения на некоторые страницы. Например, на странице регистрации, поля не выровнены и кнопки выглядят как из прошлого века.

.. _fig-register-initial:

.. figure:: ../images/ch11-bootstrap-register-initial.png
	:figclass: align-center

	Снимок экрана страницы регистрации после применения стилизации Bootstrap, но без нашей дополнительной стилизации.
	
#TODO(leifos):update this screen shot.

Кроме того Вы вероятно заметили, что в боковой панели ничего нет. В следующей главе мы расположим в ней, некоторые полезные навигационные ссылки. Но сначала, давайте разберемся с главной страницей.

Главная Страница
................
Поскольку единственное, что мы сделали - это стилизовали заголовок страницы с помощью ``<div class="page-header">``, мы практически не использовали классы и стализацию, которую предоставляет Bootstrap. Поэтому здесь мы резиновые колонки и разместим в них 5 самых популярных категорий и страниц. Поскольку первоначальная страница имела четыре колонки, мы оставили две и сделали их больше, настроив размеры колонок. Измените шаблон ``index.html``, чтобы он выглядел следующим образом:


.. code-block:: html

	{% extends 'base.html' %}

	{% load staticfiles %}

	{% block title %}Index{% endblock %}

		{% block body_block %}
	{% if user.is_authenticated %}
	    <div class="page-header">

		        <h1>Rango says... hello {{ user.username }}!</h1>
		    {% else %}
		        <h1>Rango says... hello world!</h1>
		    {% endif %}
	</div>

	         <div class="row placeholders">
	            <div class="col-xs-12 col-sm-6 placeholder">
	               <h4>Categories</h4>

	              {% if categories %}
		            <ul>
		                {% for category in categories %}
		                 <li><a href="{% url 'category'  category.slug %}">{{ category.name }}</a></li>
		                {% endfor %}
		            </ul>
		        {% else %}
		            <strong>There are no categories present.</strong>
		        {% endif %}

	            </div>
	            <div class="col-xs-12 col-sm-6 placeholder">
	              <h4>Pages</h4>

	                {% if pages %}
		            <ul>
		                {% for page in pages %}
		                 <li><a href="{{page.url}}">{{ page.title }}</a></li>
		                {% endfor %}
		            </ul>
		        {% else %}
		            <strong>There are no categories present.</strong>
		        {% endif %}
	            </div>

	          </div>


	       <p> visits: {{ visits }}</p>
		{% endblock %}

Теперь страница стала выглядеть намного лучше. Но списки выглядят ужасно. Давайте воспользуемся стилем list-group, существующим в Bootstrap, http://getbootstrap.com/components/#list-group. Измените элементы ``<ul>`` на ``<ul class="list-group">`` и элементы ``<li>`` на ``<li class="list-group-item">``, после чего измените заголовки, используя стиль panel:

.. code-block:: html


	<div class="panel panel-primary">
    	<div class="panel-heading">
        	<h3 class="panel-title">Categories</h3>
        </div>
    </div>


	<div class="panel panel-primary">
		<div class="panel-heading">
			<h3 class="panel-title">Pages</h3>
		</div>
	</div>

Замените ``<h4>Categories</h4>`` и ``<h4>Pages</h4>`` соответственно. Теперь страница выглядит красиво.



.. _fig-index-page-before:

.. figure:: ../images/ch11-bootstrap-index-initial.png
	:figclass: align-center

	Снимок экрана главной страницы с основным содержимым.


.. _fig-index-page-after:

.. figure:: ../images/ch11-bootstrap-index-rows.png
	:figclass: align-center

	Снимок экрана главной страницы с измененной нами Bootstrap стилизацией.

Страница входа в систему
------------------------
Теперь давайте рассмотрим страницу входа в систему. На сайте Bootstrap видно, что они уже создали `хорошую форму для входа в систему <http://getbootstrap.com/examples/signin/>`_, смотри http://getbootstrap.com/examples/signin/. Если просмотреть код страницы, то Вы заметите множество классов, которые нужно добавить в базовую форму для входа в систему. Измените шаблон ``login.html`` следующим образом:

.. code-block:: html
	
	{% block body_block %}

        <link href="http://getbootstrap.com/examples/signin/signin.css" rel="stylesheet">

        <form class="form-signin" role="form" method="post" action=".">
        {% csrf_token %}

        <h2 class="form-signin-heading">Please sign in</h2>
        <input class="form-control" placeholder="Username" id="id_username" maxlength="254" name="username" type="text" required autofocus=""/>
        <input type="password" class="form-control" placeholder="Password" id="id_password" name="password"  required />

  		<button class="btn btn-lg btn-primary btn-block" type="submit" value="Submit" >Sign in</button>
		</form>

	{% endblock %}

Кроме добавления ссылки на файл ``signin.css`` Bootstrap и ряда изменений в классах, связанных с элементами, мы удалили код, который автоматически генерирует форму для входа в систему, т. е., ``form.as_p``. Вместо этого, мы использовали HTML теги элементов и что важно идентификаторы создаваемых элементов аналогичные тем, которые используются в Bootstrap форме.

Кнопке были присвоены классы ``btn`` и ``btn-primary``. Если Вы обратитесь к `Bootstrap разделу по кнопкам <http://getbootstrap.com/css/#buttons>`_, то увидите, что существует множество различных цветов, которые могут быть назначены кнопкам, смотри http://getbootstrap.com/css/#buttons.


.. _fig-register-page-after:

.. figure:: ../images/ch11-bootstrap-login-custom.png
	:figclass: align-center

	Снимок экрана страницы входа в систему с измененной нами Bootstrap стилизацией.
	
#TODO(Leifos): update the screen shot

Другие шаблоны, использующие форму
..................................
Можно проделать аналогичные изменения с шаблонами ``add_cagegory.html`` и ``add_page.html``. Шаблон ``add_page.html`` можно модифицировать следующим образом:

.. code-block:: html

	{% extends 'base.html' %}

	{% block title %}Add Page{% endblock %}


	{% block body_block %}
	{% if category %}

		        <form role="form"  id="page_form" method="post" action="/rango/category/{{category.slug}}/add_page/">
	            <h2 class="form-signin-heading">Add a Page to <a href="/rango/category/{{category.slug}}/"> {{ category.name }}</a></h2>
		            {% csrf_token %}
		            {% for hidden in form.hidden_fields %}
		                {{ hidden }}
		            {% endfor %}

		            {% for field in form.visible_fields %}
		                {{ field.errors }}
		                {{ field.help_text }}<br/>
		                {{ field }}<br/>
		            {% endfor %}

	                <br/>
	            <button class="btn btn-primary" type="submit" name="submit">Add Page</button>
		        </form>
	            {%  else %}
	            <p>This is category does not exist.</p>
	        {%  endif %}


		{% endblock %}

Точно также можно изменить шаблон ``add_category.html`` (здесь не показан).

Шаблон регистрации
------------------
Для ``registration_form.html`` можно изменить форму следующим образом:

.. code-block:: html


	{% extends "base.html" %}


	{% block body_block %}
     	<form role="form"  method="post" action=".">
  			{% csrf_token %}

        <h2 class="form-signin-heading">Sign Up Here</h2>

        <div class="form-group" >
         <p class="required"> <label for="id_username">Username:</label>
             <input class="form-control"  id="id_username" maxlength="30" name="username" type="text"  placeholder="Enter username"/></p>
        </div>
         <div class="form-group">
            <p class="required"><label for="id_email">E-mail:</label>
                <input class="form-control" id="id_email" name="email" type="email" placeholder="Enter email" /></p>
         </div>
        <div class="form-group">
            <p class="required"><label for="id_password1">Password:</label>
                <input class="form-control" id="id_password1" name="password1" type="password" placeholder="Enter password" /></p>
        </div>
        <div class="form-group">
            <p class="required"><label for="id_password2">Password (again):</label>
         <input class="form-control" id="id_password2" name="password2" type="password" placeholder="Enter password again" /></p>
        </div>

        <button type="submit" class="btn btn-default">Submit</button>

		</form>
	{% endblock %}
	

Опять мы вручную преобразовали форму, созданную тегом шаблона ``{{ form.as_p }}`` и добавили различные Bootstrap классы.


.. note:: Мне не нравится такое решение. Я бы предпочел, чтобы форма добавлялась автоматически. Это приводит к идее создания класса, наследующегося от Bootstrap, и необходимого для расширения Ваших HTML шаблонов.


Использование Django-Bootstrap-Toolkit
--------------------------------------
Простой альтернативой является использование ``django-bootstrap-toolkit``, смотри https://github.com/dyve/django-bootstrap-toolkit. Помните, что существуют и другие пакеты аналогичные этому. Чтобы установить ``django-bootstrap-toolkit`` выполните команду ``pip install django-bootstrap-toolkit``. Добавьте ``bootstrap_toolkit`` в кортеж ``INSTALLED_APPS`` файла ``settings.py``. Затем измените шаблон, как показано ниже:

.. code-block::html

	{% load bootstrap_toolkit %}

	<form action="/url/to/submit/" method="post">
	    {% csrf_token %}
	    {{ form|as_bootstrap }}
	    <div class="actions">
	        <button type="submit" class="btn primary">Submit</button>
	    </div>
	</form>
	
	
В этом случае шаблон ``category.html`` принимает вид:

.. code-block::html

	{% extends 'base.html' %}
	
	{% load bootstrap_toolkit %}
	
	{% block title %}Add Category{% endblock %}
		
	{% block body_block %}
		<form id="category_form" method="post" action="{% url 'add_category' %}">
			<h2 class="form-signin-heading">Add a Category</a></h2>
			
			{% csrf_token %}
			
			{{ form|as_bootstrap }}
			
			<br/>
			
			<button class="btn btn-primary" type="submit" name="submit">Create Category</button>
		</form>
	{% endblock %}
		

Это решение требует намного меньше кода и автоматизировано. Тем не менее оно  выглядит не красиво в браузере :-(. Вероятно необходима дополнительная настройка для улучшения внешнего вида.

Окончательный результат
-----------------------
Теперь, когда приложение Rango стало выглядеть лучше, можно вернуться к работе над самим приложением и добавить в него дополнительные функциональные возможности, объединяющие приложение в единое целое.

.. _fig-register-page-custom:

.. figure:: ../images/ch11-bootstrap-register-custom.png
	:figclass: align-center

	Снимок экрана страницы регистрации с измененной нами Bootstrap стилизацией.




