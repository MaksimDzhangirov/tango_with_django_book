.. _overview-label:

Вступление
========
Цель этой книги - стать практическим руководством по веб разработке, используя *Django 1.7.* Эта книга создана главным образом для студентов, обеспечивая пошаговое руководство, необходимое для создания и запуска Ваших первых веб приложений, а также развертывания их на веб-сервере.

Эта книга создана, чтобы дополнить `официальное руководство по Django <https://docs.djangoproject.com/en/1.7/intro/tutorial01/>`_ и многие другие прекрасные руководства доступные онлайн. Собрав всё необходимое в одном месте, эта книга заполняет многие пробелы в официальной документации по Django, что позволяет изучить фреймворк Django, используя метод обучения, основанный на примерах. Более того, эта книга является введением во многие особенности, необходимые, чтобы стать специалистом в области разработки веб приложений.

Почему стоит использовать эту книгу?
------------------------
**Эта книга съэкономит Ваше время.** On many occasions we've seen clever students get stuck, spending hours trying to fight with Django and other aspects of web development. More often than not, the problem was usually because a key piece of information was not provided, or something was not made clear. While the occasional blip might set you back 10-15 minutes, sometimes they can take hours to resolve. We've tried to remove as many of these hurdles as possible. This will mean you can get on with developing your application, and not have to sit there scratching your head.

**This book will lower the learning curve.** Web application frameworks can save you a lot of hassle and lot of time. Well, that is if you know how to use them in the first place! Often the learning curve is steep. This book tries to get you going - and going fast. By showing you how to put together a web application with all the bells and whistle from the onset, the book shortens the learning curve. 

**This book will improve your workflow.** Using web application frameworks requires you to pick up and run with a particular design pattern - so you only have to fill in certain pieces in certain places. After working with many students, we heard lots of complaints about using web application frameworks - specifically about how they take control away from them (i.e. inversion of control).  To help you, we've created a number of workflows to focus your development process so that you can regain that sense of control and build your web application in a disciplined manner.

**Эта книга не создана ТОЛЬКО для чтения.** Whatever you do, do not read this book! It is a hands-on guide to building web applications in Django. Reading is not doing. To increase the value you gain from this experience, go through and develop the application. When you code up the application, *do not just cut and paste the code.* Type it in, think about what it does, then read the explanations we have provided to describe what is going on. If you still do not understand, then check out the Django documentation, go to `Stack Overflow <http://stackoverflow.com/questions/tagged/django>`_ or other helpful websites and fill in this gap in your knowledge. If you think it is worth mentioning, please get in touch with us so that we can improve the book - we already have a number of contributors and we will happily acknowledge your contribution!

Чему Вы научитесь
-------------------
In this book, we will be taking an exampled-based approach (or inquiry-based learning). В этой книге будет показано как спроектировать веб приложение, названное *Rango* (смотри Design Brief в разделе :ref:`overview-design-brief-label` ниже). По ходу повествования, мы покажем как решить следующие задачи.

* Настроить среду окружения - включая то как использовать терминал, Pip инсталятор, как работать с Git и т. д..
* Настроить Django проект и создать базовое Django приложение.
* Configure the Django project to serve static media and other media files.
* Работать с шаблоном проектирования Django's *Модель-Представление-Шаблон*.
* Create database models and use the object relational mapping functionality provided by Django.
* Создавать формы, которые могут использовать Ваши модели из базы данных, чтобы создавать динамически генерируемые страницы.
* Использовать службы аутентификации пользователя, существующие в Django.
* Добавлять внешние службы в приложение.
* Включать *Каскадные таблицы стилей (CSS)* и *JavaScript* в веб приложение.
* Проектировать и применять CSS, чтобы улучшить внешний вид и представление о веб приложении.
* Работать с cookies и сессиями в Django.
* Include more advanced functionality like *AJAX* into your application.
* Развернуть Ваше приложение на веб сервере, используя *PythonAnywhere.*

At the end of each chapter, we have included a number of exercises designed to push you harder and to see if you can apply what you have learned. The later chapters of the book provide a number of open development exercises along with coded solutions and explanations. Наконец, весь код доступен из *GitHub* по адресу https://github.com/leifos/tango_with_django.

Чтобы увидеть законеченную, работоспособную версию приложения, Вы можете также посетить веб-сайт `How to Tango with Django <http://www.tangowithdjango.com/>`_ по адресу http://www.tangowithdjango.com/rango/.

Технологии и службы
-------------------------
При изучении этой книги мы будем использовать различные технологии и внешние службы, включая:

* Python, http://www.python.org
* Pip, http://www.pip-installer.org
* Django, https://www.djangoproject.com
* Git, http://git-scm.com 
* GitHub, https://github.com
* HTML, http://www.w3.org/html/
* CSS, http://www.w3.org/Style/CSS/
* Javascript
* JQuery, http://jquery.com
* Twitter Bootstrap, http://getbootstrap.com/
* Bing Search API via Azure Datamarket, http://datamarket.azure.com
* PythonAnywhere, https://www.pythonanywhere.com

We've selected these technologies and services as they are either fundamental to web development, and/or enable us to provide examples on how to integrate your web application with CSS toolkits (like *Twitter Bootstrap*), external services like (those provided by *Microsoft Azure*) and deploy your application quickly and easily (with PythonAnywhere).

Rango: Initial Design and Specification
---------------------------------------
As previously mentioned, the focus of this book will be to develop an application called *Rango*. As we develop this application, it will cover the core components that need to be developed when building any web application.

.. _overview-design-brief-label:

Design Brief
............
Your client would like you to create a website called *Rango* that lets users browse through user-defined categories to access various web pages. In Spanish, the word rango is used to mean *"a league ranked by quality"* or *"a position in a social hierarchy"* (see https://www.vocabulary.com/dictionary/es/rango).

* For the *main page* of the site, they would like visitors to be able to see:
	* the 5 most viewed pages;
	* the five most rango'ed categories; and
	* some way for visitors to browse or search through categories.
* When a user views a *category page*, they would like it to display:
	* the category name, the number of visits, the number of likes;
	* along with the list of associated pages in that category (showing the page's title and linking to its url); and.
	* some search functionality (via Bing's Search API) to find other pages that can be linked to this category.
* For a particular category, the client would like the name of the category to be recorded, the number of times each category page has been visited, and how many users have clicked a "like" button (i.e. the page gets rango'ed, and voted up the social hierarchy).
* Each category should be accessible via a readable URL - for example, ``/rango/books-about-django/``.
* Only registered users will be able to search and add pages to categories. And so, visitors to the site should be able to register for an account.

At first glance, the application to develop seems reasonably straightforward. In essence, it is just a list of categories which link to pages, right? However, there are a number of complexities and challenges that need to be addressed. First, let's try and build up a better picture of what needs to be developed by laying down some high-level designs.

Exercises
---------
Before going any further, think about these specifications and draw up the following design artefacts.

* An N-Tier or System Architecture diagram.
* Wireframes of the Main Page and the Category Page.
* The URL Mappings.
* An Entity-Relationship diagram to describe the data model that we'll be implementing.

N-Tier Architecture
-------------------
The high-level architecture for most web applications is a *3-Tier architecture.* Rango will be a variant on this architecture as it interfaces with an external service.

.. _fig-ntier:

.. figure:: ../images/rango-ntier-architecture.svg
	:scale: 100%
	:figclass: align-center
	
	Overview of the system architecture for Rango. Note the inclusion of an external Search *Application Programming Interface (API).*

Since we are building a web application with Django, we will use the following technologies for the following tiers.

* The *client* will be a web browser (i.e Chrome, Firefox, Safari, etc.) which will render HTML/CSS pages.
* The *middleware* will be a Django application, and will be dispatched through Django's built-in development web server while we develop.
* The *database* will be the Python-based *SQLite3* Database engine.
* The *search API* will be the *Bing Search API.*

For the most part, this book will focus on developing the middleware, though it should be quite evident from Figure :num:`fig-ntier` that we will have to interface with all the other components.

Wireframes
----------
Wireframes are great way to provide clients with some idea of what the application should look like when complete. They save a lot of time, and can vary from hand drawn sketches to exact mockups depending on the tools that you have available. For Rango, we'd like to make the index page of the site look like the screen shot shown in Figure :num:`fig-index-page`. Our category page is shown in Figure :num:`fig-cat-page`.

.. _fig-index-page:

.. figure:: ../images/ch1-rango-index.png
	:scale: 60%
	:figclass: align-center

	The index page with the categories bar on the left, also showing the top five pages and top five categories.

.. _fig-cat-page:

.. figure:: ../images/ch1-rango-cat-page.png
	:scale: 60%
	:figclass: align-center
	
	The category page showing the pages in the category (along with the number of views). Below, a search for *Python* has been conducted, with the results shown underneath.

Pages and URL Mappings
----------------------
From the specification, we have already identified two pages that our application will present to the user at different points in time. To access each of these pages we will need to describe in some fashion the URL mappings. Think of a URL mapping as the text a user will have to enter into a browser's address bar to reach the given page. The basic URL mappings for Rango are shown below.

* ``/rango/`` will point to the main (or index) page view.
* ``/rango/about/`` will point to an about page view.
* ``/rango/category/<category_name>/`` will point to the category page view for ``<category_name>``, where the category might be:
	* games;
	* python recipes; or
	* code and compilers.
* ``/rango/etc/``, where ``etc`` could be replaced with a URL for any later function we wish to implement.

As we build our application, we will probably need to create other URL mappings. However, the ones listed above will get us started. We will also at some point have to transform category names in a valid URL string, as well as handle scenarios where the supplied category name does not exist. 

As we progress through the book, we will flesh out how to construct these pages using the Django framework and use its Model-View-Template design pattern. However, now that we have a gist of the URL mappings and what the pages are going to look like, we need to define the data model that will house the data for our web application.

Entity-Relationship Diagram
---------------------------
Given the specification, it should be clear that we have at least two entities: a *category* and a *page*. It should also be clear that a *category* can house many *pages*. We can formulate the following ER Diagram to describe this simple data model.

.. _fig-rango-erd:

.. figure:: ../images/rango-erd.svg
	:scale: 100%
	:figclass: align-center

	The Entity Relationship Diagram of Rango's two main entities.

Note that this specification is vague. One page may be in one or many categories. So we could model the relationship as a many-to-many. This approach however introduces a number of complexities, so we will make the simplifying assumption that *one category contains many pages, but one page is assigned to one category.* This does not preclude that the same page can be assigned to different categories - but the page would have to be entered twice, which may not be ideal.

It's good practice to note down any working assumptions like this. You never know when they may come back to haunt you! By noting them down, this means you can communicate it with your development team and make sure that the assumption is sensible and that they are happy to proceed under such an assumption.

The resulting tables are shown below, where ``Str`` denotes a ``string`` or ``char`` field, ``Int`` denotes an ``integer`` field, ``URL`` denotes a URL field and ``FK`` denotes a Foreign Key.

.. raw:: html
	
	<style type="text/css">
		
		#ch1-tables table {
			width: 80%;
			margin: auto;
			margin: 
		}
		
		#ch1-tables table tr th {
			border-bottom: 2px solid black;
			text-align: center;
		}
		
		#ch1-tables table tr.table-header th {
			border-bottom: none;
			margin: 10px 0 10px;
			font-size: 12pt;
			font-style: italic;
		}
		
		#ch1-tables table tr td {
			text-align: center;
			border-bottom: 1px solid lightgray;
		}
		
		#ch1-tables table th.none, #ch1-tables table td.none {
			border: none;
		}
	
	</style>
	
	<div id="ch1-tables">
		<table>
			
			<tr class="table-header">
				<th colspan="2">Category Table</th>
				<th class="none">&nbsp;</th>
				<th colspan="2">Page Table</th>
			</tr>
			
			<tr>
				<th style="width: 20%;">Field</th>
				<th style="width: 20%;">Type</th>
			
				<th class="none"></th>
			
				<th style="width: 20%;">Field</th>
				<th style="width: 20%;">Type</th>
			</tr>
		
			<tr>
				<td>name</td>
				<td>Str</td>
			
				<td class="none">&nbsp;</td>
			
				<td>category</td>
				<td>FK</td>
			</tr>
			
			<tr>
				<td>views</td>
				<td>Int</td>
			
				<td class="none">&nbsp;</td>
			
				<td>title</td>
				<td>Str</td>
			</tr>
			
			<tr>
				<td>likes</td>
				<td>Int</td>
			
				<td class="none">&nbsp;</td>
			
				<td>url</td>
				<td>URL</td>
			</tr>
			
			<tr>
				<td class="none">&nbsp;</td>
				<td class="none">&nbsp;</td>
		
				<td class="none">&nbsp;</td>
		
				<td>views</td>
				<td>Int</td>
			</tr>
	
		</table>
	</div>

We will also have a ``User`` table - which we have not shown here, but shall introduce later in the book. In the following chapters will we see how to instantiate these data models in Django and how to use Django's Object Relational Mapping to connect to the database. 

Summary
-------
These high level design and specifications will serve as a useful reference point when building our web application. While we will be focusing on using specific technologies, these steps are common to most database driven web sites. It's a good idea to become familiar and comfortable with producing such specifications and designs.

If you already have Python 2.7 and Django 1.7 installed, you have a good working knowledge of the command line, configured your paths, then you can skip straight to the :ref:`Django Basics <django-basics>` chapter. Otherwise, get started with Chapter :ref:`requirements-label`.

Working with The Official Django Tutorials
..........................................
We suggest undertaking the `Official Django Tutorials <https://docs.djangoproject.com/en/1.7/intro/tutorial01/>`_ as part of the exercises associated with each of this book's chapters. You can find a mapping between the tutorial exercises and book chapters below. The tutorial exercises will help reinforce your understanding of the Django framework, and also help you build up your skills.

.. raw:: html
	
	<style type="text/css">
		
		#ch1-tables table {
			width: 80%;
			margin: auto;
			margin: 
		}
		
		#ch1-tables table tr th {
			border-bottom: 2px solid black;
			text-align: center;
		}
		
		#ch1-tables table tr.table-header th {
			border-bottom: none;
			margin: 10px 0 10px;
			font-size: 12pt;
			font-style: italic;
		}
		
		#ch1-tables table tr td {
			text-align: center;
			border-bottom: 1px solid lightgray;
		}
		
		#ch1-tables table th.none, #ch1-tables table td.none {
			border: none;
		}
	
	</style>
	
	<div id="ch1-tables">
		<table>
			
			<tr>
				<th style="width: 20%;">Танго с Django</th>
				<th style="width: 20%;">Учеюное пособие по Django</th>
			</tr>
			
			<tr>
				<td>Глава 3</td>
				<td><a href="https://docs.djangoproject.com/en/1.7/intro/tutorial01/">Часть 1 - Модели</a></td>
			</tr>
			
			<tr>
				<td>Глава 5</td>
				<td><a href="https://docs.djangoproject.com/en/1.7/intro/tutorial02/">Часть 2 - Интерфейс администратора</a></td>
			</tr>
			
			<tr>
				<td>Глава 6</td>
				<td><a href="https://docs.djangoproject.com/en/1.7/intro/tutorial03/">Часть 3 - URLы и Представления</a></td>
			</tr>
			
			<tr>
				<td>Глава 7</td>
				<td><a href="https://docs.djangoproject.com/en/1.7/intro/tutorial04/">Часть 4 - Шаблоны</a></td>
			</tr>
			
			<tr>
				<td>Часть 18</td>
				<td><a href="https://docs.djangoproject.com/en/1.7/intro/tutorial05/">Часть 5 - Тестирование</a></td>
			</tr>
			
			<tr>
				<td>Часть 11</td>
				<td><a href="https://docs.djangoproject.com/en/1.7/intro/tutorial06/">Часть 6 - CSS</a></td>
			</tr>
	
		</table>
	</div>





