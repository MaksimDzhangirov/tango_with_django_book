.. _tango-too-label:

Улучшаем приложение Rango! Код и подсказки
==========================================

Надеемся Вы смогли выполнить упражнения, используя последовательность действий, которую мы привели; если нет или Вам необходима небольшая помощь, просмотрите фрагменты кода и используйте их для Вашей версии Rango.

Подсчет просмотра страниц
-------------------------

В настоящий момент, Rango выдает прямую ссылку на внешние страницы. Это не самый хороший вариант, если Вы хотите отслеживать количество щелчков и просмотров каждой страницы. Для подсчета количества просмотров страницы через Rango, Вам необходимо выполнить следующие действия:

Создать представление, анализирующее URL
........................................
Создайте новое представление под названием ``track_url()`` в файле ``/rango/views.py``, которое принимает параметризированный HTTP ``GET`` запрос (т. е., ``rango/goto/?page_id=1``) и обновляет число просмотров для страницы. Представление должно затем перенаправлять пользователя к фактическому URL.

.. code-block:: python	
	
	from django.shortcuts import redirect
	
	def track_url(request):
	    page_id = None
	    url = '/rango/'
	    if request.method == 'GET':
	        if 'page_id' in request.GET:
	            page_id = request.GET['page_id']
	            try:
	                page = Page.objects.get(id=page_id)
	                page.views = page.views + 1
	                page.save()
	                url = page.url
	            except:
	                pass
	
	    return redirect(url)

Удостоверьтесь, что Вы импортировали функцию ``redirect()`` в файл ``views.py``, если он не был импортирован до этого!

.. code-block:: python
	
	from django.shortcuts import redirect

Сопоставить представлению URL
.................
В файле ``/rango/urls.py`` добавьте следующий код в кортеж ``urlpatterns``.

.. code-block:: python
	
	url(r'^goto/$', views.track_url, name='goto'),


Обновить шаблон для категории
.............................
Обновите шаблон ``category.html`` так, чтобы в нём использовался URL ``rango/goto/?page_id=XXX`` вместо прямого URL в ссылке, на которую нажимает пользователь.

.. code-block:: html
	
    {% for page in pages %}
		<li>
        	<a href="{% url 'goto' %}?page_id={{page.id}}">{{ page.title }}</a>
            {% if page.views > 1 %}
            	({{ page.views }} views)
           	{% elif page.views == 1 %}
            	({{ page.views }} view)
            {% endif %}
		</li>
    {% endfor %}

Здесь видно, что мы добавили в шаблон некоторые управляющие операторы, которые используются для вывода слова ``view`` (при одном просмотре), ``views`` (если число просмотров больше 1) или ничего не выводят, в зависимости от значения ``page.views``.

Обновить представление Category
................................
Так как мы отслеживаем количество переходов по ссылке, теперь Вы можете обновить представление ``category()``, чтобы отсортировать страницы по количеству просмотров, т. е.:

.. code-block:: python


	pages = Page.objects.filter(category=category).order_by('-views')

Теперь убедитесь, что всё работает правильно, нажав на ссылки, и затем вернувшись на страницу категории. Не забудьте обновить страницу или перейдите в другую категорию, чтобы увидеть обновленную страницу.

.. #######################################################


Поиск на странице категории
---------------------------
Цель Rango - предоставить пользователям полезный каталог ссылок на страницы. На данный момент, функция поиска не зависима от категорий. Было бы лучше, если бы поиск был интегрирован в просмотр категории. Давайте предположим, что пользователи сначала просматривают интересующие их категории. Если они не нашли нужную им страницу, тогда они могут поискать её. Если они нашли в поиске подходящую страницу, они могут добавить её в категорию, в которой они находятся. Давайте решим первую задачу.
Сначала нужно удалить глобальную функцию поиска и позволять пользователям осуществлять поиск только внутри категории. Это означает, что мы можем удалить текущую страницу поиска и представление для поиска. После этого необходимо выполнить следующие действия.

Удоаляем глобальную функцию поиска
..................................
Удалите ссылку на глобальный *Поиск* из меню, отредактировав шаблон ``base.html``. Вы можете также удалить или закомментировать URL сопоставление в файле ``rango/urls.py``.

Создаем шаблон формы для поиска
...............................
Перенесите форму для поиска из ``search.html`` в ``category.html``. Удостоверьтесь, что атрибут ``action`` тега form ссылается на представление ``category()`` как показано ниже.

.. code-block:: html

    <form class="form-inline" id="user_form" method="post" action="{% url 'category'  category.slug %}">
    	{% csrf_token %}
        <!-- Отображаем элементы формы для поиска здесь -->
        <input class="form-control" type="text" size="50" name="query" value="{{query}}" id="query" />
        <input class="btn btn-primary" type="submit" name="submit" value="Search" />
   </form>

Также ниже добавьте ``<div>``, в котором будут находиться результаты поиска.

.. code-block:: html

	<div class="panel">
		{% if result_list %}
	    	<div class="panel-heading">
	        	<h3 class="panel-title">Results</h3>
	        	<!-- Отображаем результаты поиска в виде упорядоченного списка -->
	        	<div class="panel-body">
	            	<div class="list-group">
	                	{% for result in result_list %}
	                    <div class="list-group-item">
	                    	<h4 class="list-group-item-heading"><a href="{{ result.link }}">{{ result.title }}</a></h4>
	                        <p class="list-group-item-text">{{ result.summary }}</p>
	                    </div>
	                {% endfor %}
	            </div>
	        </div>
	    {% endif %}
	</div>
	
Обновляем представление Category
................................
Обновите представление для категории, чтобы оно могло обрабатывать HTTP ``POST`` запрос (который возникает, когда пользователь отправляет данные, введенные в форму для поиска) и добавьте список результатов в словарь контекста. Приведенный ниже код реализует эту новую функцию.

.. code-block:: python

	def category(request, category_name_slug):
	    context_dict = {}
	    context_dict['result_list'] = None
	    context_dict['query'] = None
	    if request.method == 'POST':
	        query = request.POST['query'].strip()

	        if query:
	            # Запускаем нашу функцию Bing, чтобы получить список результатов поиска!
	            result_list = run_query(query)

	            context_dict['result_list'] = result_list
	            context_dict['query'] = query

	    try:
	        category = Category.objects.get(slug=category_name_slug)
	        context_dict['category_name'] = category.name
	        pages = Page.objects.filter(category=category).order_by('-views')
	        context_dict['pages'] = pages
	        context_dict['category'] = category
	    except Category.DoesNotExist:
	        pass

	    if not context_dict['query']:
	        context_dict['query'] = category.name

	    return render(request, 'rango/category.html', context_dict)


Обратите внимание, что в словарь ``context_dict``, который мы передали шаблону ``rango/category.html`` мы добавили ``result_list`` (список результатов поиска) и ``query`` (поисковый запрос), причем если переменной ``query`` не существует, то используется поисковый запрос по умолчанию равный названию категории. Эта переменная будет отображаться в поле для ввода запроса.

	.. #########################################################################

..	View Profile 
	------------
	Чтобы добавить функцию просмотра профиля, выполните следующие шаги.
	
	Создайте шаблон для профиля
	...........................
	Сначала создайте новый шаблон под названием ``profile.html``. В этот шаблон добавьте следующий код.
	
	.. code-block:: html
	
		{% extends "rango/base.html" %}

		{% block title %}Profile{% endblock %}

		{% block body_block %}
		<div class="hero-unit">
		    <h1> Profile <h1> <br/>
		    <h2>{{ user.username }}</h2>
		    <p>Email: {{ user.email }}</p>
        
		    {% if userprofile %}
		        <p>Website: <a href="{{ userprofile.website }}">{{ userprofile.website }}</a></p>
		        <br/>
		        {% if userprofile.picture %}
		            <img src="{{ userprofile.picture.url }}"  />
		        {% endif %}
		    {% endif %}
		</div>
		{% endblock %}


	Создайте представление для профиля
	..................................
	Создайте представление под названием ``profile`` и добавьте в него следующий код.
	
	.. code-block:: python
	
		from django.contrib.auth.models import User
	
		@login_required
		def profile(request):
		    context = RequestContext(request)
		    cat_list = get_category_list()
		    context_dict = {'cat_list': cat_list}
		    u = User.objects.get(username=request.user)
	
		    try:
		        up = UserProfile.objects.get(user=u)
		    except:
		        up = None
	
		    context_dict['user'] = u
		    context_dict['userprofile'] = up
		    return render_to_response('rango/profile.html', context_dict, context)

	Сопоставление URL представлению для профиля	    
	...........................................
	Создайте сопоставление между URL ``/rango/profile`` и представлением ``profile()``. Для этого обновите кортеж ``urlpatterns`` в файле ``rango/urls.py`` так, чтобы содержал следующую строку.

	.. code-block:: python
	
		url(r'^profile/$', views.profile, name='profile'),

	Обновляем базовый шаблон
	........................
	В шаблоне ``base.html``, обновите код, добавив ссылку на страницу профиля в меню.

	.. code-block:: html
	
		{% if user.is_authenticated %}
		    <li><a href="/rango/profile">Profile</a></li>
		{% endif %}	
	
	.. #########################################################################

	Подсчет просмотра страниц
	-------------------------
	В настоящий момент, Rango выдает прямую ссылку на внешние страницы. Это не самый хороший вариант, если Вы хотите отслеживать количество щелчков и просмотров каждой страницы. Для подсчета количества просмотров страницы через Rango, Вам необходимо выполнить следующие действия:

	Создать представление, анализирующее URL
	........................................
	Создайте новое представление под названием ``track_url()`` в файле ``/rango/views.py``, которое принимает параметризированный HTTP ``GET`` запрос (т. е., ``rango/goto/?page_id=1``) и обновляет число просмотров для страницы. Представление должно затем перенаправлять пользователя к фактическому URL.

	.. code-block:: python	
	
		def track_url(request):
		    context = RequestContext(request)
		    page_id = None
		    url = '/rango/'
		    if request.method == 'GET':
		        if 'page_id' in request.GET:
		            page_id = request.GET['page_id']
		            try:
		                page = Page.objects.get(id=page_id)
		                page.views = page.views + 1
		                page.save()
		                url = page.url
		            except:
		                pass
	
		    return redirect(url)

	Удостоверьтесь, что Вы импортировали функцию ``redirect()`` в файл ``views.py``, если он не был импортирован до этого!

	.. code-block:: python
	
		from django.shortcuts import redirect

	Сопоставить представлению URL
	.................
	В файле ``/rango/urls.py`` добавьте следующий код в кортеж ``urlpatterns``.

	.. code-block:: python
	
		url(r'^goto/$', views.track_url, name='track_url'),


	Обновить шаблон для категории
	.............................
	Обновите шаблон ``category.html`` так, чтобы в нём использовался URL ``rango/goto/?page_id=XXX`` вместо прямого URL в ссылке, на которую нажимает пользователь.

	.. code-block:: html
	
		{% if pages %}
		<ul>
		    {% for page in pages %}
		    <li>
		        <a href="/rango/goto/?page_id={{page.id}}">{{page.title}}</a>
		        {% if page.views > 1 %}
		            - ({{ page.views }} views)
		        {% elif page.views == 1 %}
		            - ({{ page.views }} view)
		        {% endif %}
		    </li>
		    {% endfor %}
		</ul>
		{% else %}
		<strong>No pages currently in category.</strong><br/>
		{% endif %}

	Здесь видно, что мы добавили в шаблон некоторые управляющие операторы, которые используются для вывода слова ``view`` (при одном просмотре), ``views`` (если число просмотров больше 1) или ничего не выводят, в зависимости от значения ``page.views``.

	Обновить представление Category
	...............................
	Так как мы отслеживаем количество переходов по ссылке, теперь Вы можете обновить представление ``category()``, чтобы отсортировать страницы по количеству просмотров. Убедитесь, что всё работает правильно, нажав на ссылку и обновив представление для категории - щелчок по ссылке должен увеличить рейтинг страницы.
