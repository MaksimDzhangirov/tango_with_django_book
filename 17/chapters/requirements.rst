.. _requirements-label:

Подготовка к Танго
======================
Давайте произведем настройку! Чтобы станцевать танго с Django, Вам необходимо убедиться, что Вы установили всё что необходимо на Ваш компьютер и что Вы четко понимаете для чего нужна каждая составляющая Вашей среды разработки. В этой главе пошагово рассматриваются необходимые Вам инструменты и обсуждается то, что Вы должны знать.

Для этого учебного пособия, Вам потребуется следующее программное обеспечение, без которого не возможна работа с этой книгой.

* Python версии 2.7.5+
* Django версии 1.7

Поскольку Django является фреймфорком для создания веб приложений, написанном на языке программирования Python, Вы должны иметь практические навыки программирования на этом языке. Если Вы не использовали язык Python до этого или просто хотите освежить свои знания, то мы настоятельно рекомендуем просмотреть и поработать с одним или несколькими из следующих руководств.

* **Краткое руководство** - Learn Python in 10 Minutes от Stavros, http://www.korokithakis.net/tutorials/python/.
* **Официальное руководство по Python** по адресу http://docs.python.org/2/tutorial/.
* **Блестящая книга**: Think Python: How to Think like a Computer Scientist, автор Allen B. Downey, доступная онлайн по адресу http://www.greenteapress.com/thinkpython/.
* **Изумительный онлайн курс**: Learn to Program, by Jennifer Campbell и Paul Gries по адресу https://www.coursera.org/course/programming1.

Использование терминала
------------------
Чтобы настроить Вашу среду разработки, действительно важно знать как использовать *Интерпретатор Командной Строки - ИКС (Command Line Interpreter - CLI)*, входящий в состав Вашей операционной системы. Во время работы с этим учебным пособием, вы будете постоянно взаимодействовать с ИКС. Если Вы уже знаете как использовать интерфейс командной строки, вы можете перейти непосредственно к разделу :ref:`Установка программного обеспечения <installing-software>`.

Все операционные системы на основе UNIX используют приблизительно одинаковый `терминал <http://www.ee.surrey.ac.uk/Teaching/Unix/unixintro.html>`_. На сегодняшний день доступны потомки, производные и клоны UNIX, включая `Apple's OS X <http://en.wikipedia.org/wiki/OS_X>`_  и `многие доступные дистрибутивы Linux <http://en.wikipedia.org/wiki/List_of_Linux_distributions>`_. Все эти операционные системы содержат базовый набор команд, которые помогут Вам перемещаться по Вашей файловой системе и запускать программы без использования графического интерфейса. В этом разделе приведены основные команды, с которыми Вы должны ознакомиться.

.. note:: Это учебное пособие ориентировано на пользователей операционных систем, основанных на UNIX или UNIX-подобных. Хотя Python и Django могут работать в среде Windows, многие команды, которые мы будем использовать в этой книге предназначены для терминалов, основанных на UNIX. Тем не менее, эти команды могут быть воспроизведены в Windows, используя графический интерфейс пользователя, `применяя соответствующую команду в командной строке Windows <http://www.ai.uga.edu/mc/winforunix.html>`_ или применяя `Windows PowerShell <http://technet.microsoft.com/en-us/library/bb978526.aspx>`_, который предоставляет ИКС подобный UNIX терминалу.

.. Примечание переводчика:: Командную строку в Windows 7 можно вызвать следующим образом. Откройте меню Пуск и в строке *Найти программы и файлы* введите cmd.exe.

После запуска нового окна терминала, Вы обычно видите что-то подобное:

.. code-block:: guess
	
	sibu:~ leif$

Это называется *приглашением командной строки*, и обозначает, что система ждет и готова к выполнению любой Вашей команды. Приглашение командной строки, которое Вы видите, может меняться в зависимости от используемой операционной системы, но все они похожи друг на друга. В вышеприведенном примере, обратите внимание на следующие три основных элемента:

* Ваше имя пользователя и имя компьютера (имя пользователя ``leif`` и имя компьютера ``sibu``);
* Ваш *текущий рабочий каталог* (тильда или ``~``); и
* привилегия учетной записи пользователя (знак доллара или ``$``).

Знак доллара (``$``) обычно обозначает, что пользователь использует стандартную пользовательскую учетную запись. Напротив, символ решетки (``#``) используется для обозначения того, что пользователь, вошедший в систему, имеет `привелегии типа root или суперпользователя <http://en.wikipedia.org/wiki/Superuser>`_. Не зависимо от того такой символ изображен, он используется, чтобы показать, что компьютер ожидает Вашего ввода. 

Откройте окно терминала и посмотрите как выглядит Ваше приглашение командной строки.

.. Примечание переводчика:: В ИКС cmd.exe приглашение командной строки выглядит как:

.. code-block:: guess

	Текущий рабочий каталог>

Изменить вид приглашения командной строки можно с помощью команды ``prompt``, например, ``prompt $$`` меняет вид приглашения на знак доллара.

Когда Вы используете терминал, важно знать в каком каталоге файловой системы Вы находитесь. Чтобы это узнать, Вы можете выполнить команду ``pwd``. Она отобразит Ваш текущий рабочий каталог. В качестве примера рассмотрим работу с терминалом, показанную ниже.

.. code-block:: guess
	
	Last login: Mon Sep 23 11:35:44 on ttys003
	sibu:~ leif$ pwd
	/Users/leif
	sibu:~ leif$

В этом примере текущий рабочий каталог - это: ``/Users/leif``.

Вы должны были также заметить, что приглашение указывает, что мой текущий рабочий каталог - это ~. Это связано с тем, что тильда (``~``) представляет Ваш *домашний каталог*. Основной каталог в любой файловой системе, основанной на UNIX, - это *корневой каталог*. Путь к корневому каталогу обозначается одним прямым слэшем (``/``).

Если вы находитесь не в своём домашнем каталоге, Вы можеет изменить каталог (``cd``) на домашний, выполнив следующую команду.

.. code-block:: guess
	
	$ cd ~

Давайте создадим каталог под названием ``code``. Для этого используйте команду (``mkdir``), как показано ниже.

.. code-block:: guess
	
	$ mkdir code

Чтобы перейти в только что созданный каталог ``code``, введите ``cd code``. Если теперь просмотреть Ваш текущий рабочий каталог, то он изменится на ``~/code/``. Это также может быть отражено в Вашем приглашении. Заметьте, что в приведенном ниже примере, текущий рабочий каталог выводится после имени компьютера ``sibu``.

.. Замечание:: Всякий раз говоря о ``<рабочем пространстве>``, мы будем иметь в виду Ваш каталог ``code``.

.. code-block:: guess
	
	sibu:~ leif$ mkdir code
	sibu:~ leif$ cd code
	sibu:code leif$ 
	sibu:code leif$ pwd
	/Users/leif/code

Чтобы получить список файлов, которые находятся в каталоге, Вы можете выполнить команду ``ls``. Чтобы увидеть скрытые файлы или каталоги - если таковые существуют - выполните команду ``ls -a``, где ключ ``a`` первая буква слова *all (все).* Если вернуться обратно в Ваш домашний каталог (``cd ~``) и затем выполнить ``ls``, Вы увидите, что существует нечто под названием ``code`` в Вашем домашнем каталоге.

Чтобы получить больше информации о том, что находится в Вашем каталоге, введите ``ls -l``. Эта команда выдает более подробный *список* Ваших файлов, а также информацию о том является ли файл каталогом или нет (для этого используется символ ``d`` в начале строки).

.. code-block:: guess
	
	sibu:~ leif$ cd ~ 
	sibu:~ leif$ ls -l 
	
	drwxr-xr-x   36 leif  staff    1224 23 Sep 10:42 code

Выводимый текст также содержит информацию о `правах доступа связанных с каталогом <http://www.elated.com/articles/understanding-permissions/>`_, кто его создал (``leif``), группе пользователей (``staff``), размере, дате/времени, когда файл был изменен и, конечно, его название.

.. Примечание переводчика:: В ИКС cmd.exe для просмотра содержимого каталога используйте команду ``dir``.

Также полезно иметь возможность редактировать файлы, используя Ваш терминал. Существует много редакторов, которые Вы можете использовать - причем некоторые из них могут быть уже установлены на Вашем компьютере. Редактор `nano <http://www.nano-editor.org/>`_, например, является простым редактором, в отличие от `vi <http://en.wikipedia.org/wiki/Vi>`_, для изучения которого потребуется некоторое время. Ниже приводится список часто используемых UNIX команд, которые могут оказаться полезны.

Основные команды
*************
Все операционные системы, основанные на UNIX, содержат список встроенных команд - большинство из которых предназначено исключительно для работы с файлами. Команды, которые Вы будете использовать чаще всего, приведены ниже, с коротким пояснением того, что они деляют и как их использовать.

- ``pwd``: Выводит на экран терминала Ваш текущий *рабочий каталог*. Отображается полный путь того каталога, в котором Вы сейчас находитесь.
- ``ls``: Выводит список файлов в текущем рабочем каталоге на экран терминала. По умолчанию, размер файлов не выводится - если он необходим необходимо добавить к команде ``ls`` ключ ``-lh``, т. е. ввести команду ``ls -lh``.
- ``cd``: Позволяет Вам *изменить* Ваш текущий рабочий *каталог* с учетом пути. Например, команда ``cd /home/leif/`` изменяет текущий рабочий каталог на ``/home/leif/``. Вы также можете перемещаться на один уровень каталогов вверх без указания `полного пути <http://www.uvsc.edu/disted/decourses/dgm/2120/IN/steinja/lessons/06/06_04.html>`_, используя две точки, например ``cd ..``.
- ``cp``: Копирует файлы и/или каталоги. Вы должны указать *источник* (откуда копировать) и *назначение* (куда копировать). Например, чтобы скопировать файл ``input.py`` в тот же каталог, Вы можете ввести команду ``cp input.py input_backup.py``.
- ``mv``: Перемещает файлы/каталоги. Как и ``cp``, Вы должны указать *источник* и *назначение*. Эта команда также используется для переименовывания файлов. Например, чтобы переименовать ``numbers.txt`` в ``letters.txt``, выполните команду ``mv numbers.txt letters.txt``. Чтобы переместить файл в другой каталог, необходимо указать абсолютный или относительный путь как часть назначения - например, ``mv numbers.txt /home/david/numbers.txt``.
- ``mkdir``: Создает каталог в текущем рабочем каталоге. Вы должны указать название нового каталога после команды ``mkdir``. Например, если Выш текущий рабочий каталог - это ``/home/david/`` и Вы ввели ``mkdir music``, то будет создан каталог ``/home/david/music/``. Выполните команду ``cd имя каталога``, чтобы перейти в только что созданный каталог.
- ``rm``: сокращение от *remove (удалить)*, эта команда удаляет файлы из Вашей файловой системы. Вы должны указать имя файла(ов), которые хотите удалить. При выполнении команды ``rm``, появляется предупреждающее сообщение о том, действительно ли Вы хотите удалить выбранный файл(ы). Вы также можете удалять каталоги, `используя рекурсивный ключ <http://www.computerhope.com/issues/ch000798.htm>`_. Будьте осторожны при использовании этой команды - восстановить удаленные файлы очень сложно, если вообще возможно!
- ``rmdir``: Альтернативная команда для удаления каталогов из Вашей файловой системы. Нужно указать каталог, который Вы хотите удалить. Опять, будьте осторожны: система не предложит подтвердить свои намерения.
- ``sudo``: Программа, которая позволяет Вам запускать команды с привилегиями безопасности другого пользователя. Обычно она используется для запуска других программ от имени ``root`` - `суперпользователя <http://en.wikipedia.org/wiki/Superuser>`_ любой операционной системы, основанной на UNIX или UNIX-подобной.

.. Замечание:: Это только краткий список команд. Просмотрите документацию Ubuntu `Использование терминала <https://help.ubuntu.com/community/UsingTheTerminal>`_  для более подробного обзора или `Шпаргалку 
 <http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/>`_ от FOSSwire для краткого справочного руководства.

 .. Примечание переводчика:: В ИКС cmd.exe для копирования файлов используйте команду ``copy``, перемещения файлов/каталогов - ``move``, удаления файлов - ``del``. Полную справку по всем командам можно найти `по адресу <http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/cmd.mspx?mfr=true>`_

.. _installing-software:

Установка программного обеспечения
-----------------------
Теперь, когда Вы достаточно понимаете как взаимодействовать с терминалом, Вы можете начать устанавливать программное обеспечение, требуемое для этого учебного пособия.

Установка Python
*****************
Итак, как насчет того, чтобы установить Python 2.7.5 на Ваш компьютер? Возможно Python уже установлен на Вашем компьютере - а, если Вы используете дистрибутив Linux или OS X, то безусловно он установлен. Это связано с тем, что некоторые функциональные возможности Вашей операционной системы `реализованы на Python <http://en.wikipedia.org/wiki/Yellowdog_Updater,_Modified>`_, поэтому возникает необходимость использования интерпретатора!

К сожалению, почти все современные операционные системы используют более старую версию Python, чем мы требуем для этого учебного пособия. Существует множество способов установки Python и многие из них к сожалению сложно в реализации. Мы покажем наиболее часто используемые способы и дадим ссылки, которые можно использовать для получения дополнительной информации.

.. Предупреждение:: В этом разделе будет подробно описано как запустить Python 2.7.5 *не зависимо от* Вашей текущей установки Python. Считается прохой практикой удалять установку Python по умолчанию, произведенную Вашей операционной системой и заменять её новой версией. Это может вывести из строя некоторые компоненты Вашей операционной системы!

Apple OS X
..........
Самый простой способ установить Python 2.7.5 на Ваш Mac - это скачать и запустить простой установщик с официального веб сайта Python. Вы можете скачать установшик, посетив веб страницу по адресу http://www.python.org/getit/releases/2.7.5/.

.. Предупреждение:: Убедитесь, что Вы скачали ``.dmg`` файл, который подходит для Вашей конкретной версии установки OS X!

#. После того как Вы скачали ``.dmg`` файл, дважды щелкните на нём в Finder.
#. Файл смонируется как отдельный диск и появится новое окно Finder.
#. Дважды щелкните на файле ``Python.mpkg``. Это запустит установщик Python.
#. Следуйте дальнейшим инструкциям на экране, пока не дойдете до места, где программа будет готова к установке программного обеспечения. Введите свой пароль для подтвердждения того, чтоы Вы хотите установить программное обеспечение.
#. После завершения, закройте установщик и извлеките диск с Python. Теперь Вы можете удалить загруженный ``.dmg`` файл.

Теперь у Вас должна быть установлена обновленная версия Python и можно начинать установку Django! Легко, не правда ли?

Дистрибутивы Linux
...................
Unfortunately, there are many different ways in which you can download, install and run an updated version of Python on your Linux distribution. To make matters worse, methodologies vary from distribution to distribution. For example, the instructions for installing Python on `Fedora <https://github.com/yyuu/pyenv>`_ may differ from those to install it on an `Ubuntu <http://www.ubuntu.com/>`_ installation.

However, not all hope is lost. An awesome tool (or a *Python environment manager*) called `pyenv <https://github.com/utahta/pythonbrew>`_ can help us address this difficulty. It provides an easy way to install and manage different versions of Python, meaning you can leave your operating system's default Python installation alone. Hurrah!

Taken from the instructions provided from `the pyenv GitHub page <https://github.com/yyuu/pyenv>`_, the following steps will install Python 2.7.9 on your Linux distribution.

1. Open a new terminal instance.
2. Install curl
::
	$ sudo apt-get install curl
3. Install ``pyenv``
::
	$ curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
This will download the installer and run it within your terminal for you. This installs pyenv into the directory ``~/.pyenv``. Remember, the tilde (``~``) represents your home directory!

4. Add to `.bashrc`
::
	$ nano ~/.bashrc

	export PATH="$HOME/.pyenv/bin:$PATH"
	eval "$(pyenv init -)"
	eval "$(pyenv virtualenv-init -)"
`pyenv` will likely tell you to do this once installed.
To edit the file ``~/.bashrc`` in a text editor (such as `gedit`, `nano`, `vi` or `emacs`)

5. Once you have saved the updated ``~/.bashrc`` file, close your terminal and open a new one. This allows the changes you make to take effect.

6. There are often `build problems <https://github.com/yyuu/pyenv/wiki/Common-build-problems>`_ to avoid these
::
	$ sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
	libreadline-dev libsqlite3-dev wget curl llvm

7. Install a Python version of your choosing
::
	$ pyenv install 2.7.9
This will install Python version 2.7.9 into `~/.pyenv/versions`

8. Now you can change the `local` or `global` version of Python
::
	$ pyenv versions
	* system
	  2.7.9

	$ pyenv global 2.7.9

.. note:: Directories and files beginning with a period or dot can be considered the equivalent of *hidden files* in Windows. `Dot files <http://en.wikipedia.org/wiki/Dot-file>`_ are not normally visible to directory-browsing tools, and are commonly used for configuration files. You can use the ``ls`` command to view hidden files by adding the ``-a`` switch to the end of the command, giving the command ``ls -a``.

.. _requirements-install-python-windows:

Windows
.......
By default, Microsoft Windows comes with no installations of Python. This means that you do not have to worry about leaving existing versions be; installing from scratch should work just fine. You can download a 64-bit or 32-bit version of Python from `the official Python website <http://www.python.org/download/>`_. If you aren't sure which one to download, you can determine if your computer is 32-bit or 64-bit by looking at the instructions provided `on the Microsoft website <http://windows.microsoft.com/en-gb/windows7/32-bit-and-64-bit-windows-frequently-asked-questions>`_.

#. When the installer is downloaded, open the file from the location to which you downloaded it.
#. Follow the on-screen prompts to install Python.
#. Close the installer once completed, and delete the downloaded file.

Once the installer is complete, you should have a working version of Python ready to go. By default, Python 2.7.5 is installed to the folder ``C:\Python27``. We recommend that you leave the path as it is.

Upon the completion of the installation, open a Command Prompt and enter the command ``python``. If you see the Python prompt, installation was successful. However, in certain circumstances, the installer may not set your Windows installation's ``PATH`` environment variable correctly. This will result in the ``python`` command not being found. Under Windows 7, you can rectify this by performing the following:

#. Click the *Start* button, right click *My Computer* and select *Properties*.
#. Click the *Advanced* tab.
#. Click the *Environment Variables* button.
#. In the *System variables* list, find the variable called *Path*, click it, then click the *Edit* button.
#. At the end of the line, enter ``;C:\python27;C:\python27\scripts``. Don't forget the semicolon - and certainly *do not* add a space.
#. Click OK to save your changes in each window.
#. Close any Command Prompt instances, open a new instance, and try run the ``python`` command again.

This should get your Python installation fully working. Windows XP, `has slightly different instructions <http://www.computerhope.com/issues/ch000549.htm>`_, and `so do Windows 8 installationsthis <http://stackoverflow.com/a/14224786>`_.

Setting Up the ``PYTHONPATH``
*****************************
With Python now installed, we now need to check that the installation was successful. To do this, we need to check that the ``PYTHONPATH``
`environment variable <http://en.wikipedia.org/wiki/Environment_variable>`_ is setup correctly. ``PYTHONPATH`` provides the Python interpreter with the location of additional Python `packages and modules <http://stackoverflow.com/questions/7948494/whats-the-difference-between-a-python-module-and-a-python-package>`_ which add extra functionality to the base Python installation. Without a correctly set ``PYTHONPATH``, we'll be unable to install and use Django!

First, let's verify that our ``PYTHONPATH`` variable exists. Depending on the installation technique that you chose, this may or may not have been done for you. To do this on your UNIX-based operating system, issue the following command in a terminal.

.. code-block:: guess
	
	$ echo $PYTHONPATH

On a Windows-based machine, open a Command Prompt and issue the following.

.. code-block:: guess
	
	$ echo %PYTHONPATH%

If all works, you should then see output that looks something similar to the example below. On a Windows-based machine, you will obviously see a Windows path, most likely originating from the C drive.

.. code-block:: guess
	
	/opt/local/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages:

This is the path to your Python installation's ``site-packages`` directory, where additional Python packages and modules are stored. If you see a path, you can continue to the next part of this tutorial. If you however do not see anything, you'll need to do a little bit of detective work to find out the path. On a Windows installation, this should be a trivial exercise: ``site-packages`` is located within the ``lib`` folder of your Python installation directory. For example, if you installed Python to ``C:\Python27``, ``site-packages`` will be at ``C:\Python27\Lib\site-packages\``.

UNIX-based operating systems however require a little bit of detective work to discover the path of your ``site-packages`` installation. To do this, launch the Python interpreter. The following terminal session demonstrates the commands you should issue.

.. code-block:: python
	
	$ python
	
	Python 2.7.5 (v2.7.5:ab05e7dd2788, May 13 2013, 13:18:45) 
	[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
	Type "help", "copyright", "credits" or "license" for more information.
	
	>>> import site
	>>> print site.getsitepackages()[0]
	
	'/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages'
	
	>>> quit()

Calling ``site.getsitepackages()`` returns a list of paths that point to additional Python package and module stores. The first typically returns the path to your ``site-packages`` directory - changing the list index position may be required depending on your installation. If you receive an error stating that ``getsitepackages()`` is not present within the ``site`` module, verify you're running the correct version of Python. Version 2.7.5 should include this function. Previous versions of the language do not include this function.

The string which is shown as a result of executing ``print site.getsitepackages()[0]`` is the path to your installation's ``site-packages`` directory. Taking the path, we now need to add it to your configuration. On a UNIX-based or UNIX-derived operating system, edit your ``.bashrc`` file once more, adding the following to the bottom of the file.


.. code-block:: guess
	
	export PYTHONPATH=$PYTHONPATH:<PATH_TO_SITE-PACKAGES>

Replace ``<PATH_TO_SITE-PACKAGES>`` with the path to your ``site-packages`` directory. Save the file, and quit and reopen any instances of your terminal.

On a Windows-based computer, you must follow the instructions shown in Section :num:`requirements-install-python-windows` to bring up the environment variables settings dialog. Add a ``PYTHONPATH`` variable with the value being set to your ``site-packages`` folder, which is typically ``C:\Python27\Lib\site-packages\``.

Использование Setuptools и Pip
************************
Установка и настройка Вашей среды разработки действительно важная часть любого проекта. 

Installing and setting up your development environment is a really important part of any project. While it is possible to install Python Packages such as Django separately, this can lead to numerous problems and hassles later on. For example, how would you share your setup with another developer? How would you set up the same environment on your new machine? How would you upgrade to the latest version of the package? Using a package manager removes much of the hassle involved in setting up and configuring your environment. It will also ensure that the package you install is the correct for the version of Python you are using, along with installing any other packages that are dependent upon the one you want to install.

In this book, we will be using *Pip*. Pip is a user-friendly wrapper over the *Setuptools* Python package manager. Because Pip depends on Setuptools, we are required to ensure that both are installed on your computer.

To start, we should download Setuptools from the `official Python package website <https://pypi.python.org/pypi/setuptools/1.1.6>`_. You can download the package in a compressed ``.tar.gz`` file. Using your favourite file extracting program, extract the files. They should all appear in a directory called ``setuptools-1.1.6`` - where ``1.1.6`` represents the Setuptools version number. From a terminal instance, you can then change into the directory and execute the script ``ez_setup.py`` as shown below.

.. code-block:: guess
	
	$ cd setuptools-1.1.6
	$ sudo python ez_setup.py

In the example above, we also use ``sudo`` to allow the changes to become system-wide. The second command should install Setuptools for you. To verify that the installation was successful, you should be able to see output similar to that shown below.

.. code-block:: guess
	
	Finished processing dependencies for setuptools==1.1.6

Of course, ``1.1.6`` is substituted with the version of Setuptools you are installing. If this line can be seen, you can move onto installing Pip. This is a trivial process, and can be completed with one simple command. From your terminal instance, enter the following.

.. code-block:: guess
	
	$ sudo easy_install pip

This command should download and install Pip, again with system-wide access. You should see the following output, verifying Pip has been successfully installed.

.. code-block:: guess
	
	Finished processing dependencies for pip

Upon seeing this output, you should be able to launch Pip from your terminal. To do so, just type ``pip``. Instead of an unrecognised command error, you should be presented with a list of commands and switches that Pip accepts. If you see this, you're ready to move on!

.. note:: With Windows-based computers, follow the same basic process. You won't need to enter the ``sudo`` command, however.

Установка Django
*****************
Once the Python package manager Pip is successfully installed on your computer, installing Django is easy. Open a Command Prompt or terminal window, and issue the following command.

.. code-block:: guess
	
	$ pip install -U django==1.7

If you are using a UNIX-based operating system and receive complaints about insufficient permissions, you will need to run the command with elevated privileges using the ``sudo`` command. If this is the case, you must then run the following command instead.

.. code-block:: guess
	
	$ sudo pip install -U django==1.7

The package manager will download Django and install it in the correct location for you. Upon completion, Django should be successfully installed. Note, if you didn't include the ``==1.7``, then a different version of Django may be installed.

Installing the Python Imaging Library
*************************************
During the course of building Rango, we will be uploading and handling images. This means we will need support from the `Pillow (Python Imaging Library) <https://pillow.readthedocs.org/en/latest/>`_. To install this package issue the following command.

.. code-block:: guess
	
	$ pip install pillow

Опять используйте ``sudo`` при необходимости. 


Installing Other Python Packages
********************************
It is worth noting that additional Python packages can be easily downloaded using the same manner. `The Python Package Index <https://pypi.python.org/pypi>`_ provides a listing of all the packages available through Pip.

To get a list of the packages installed, you can run the following command.

.. code-block:: guess
	
	$ pip list

Sharing your Package List
*************************
You can also get a list of the packages installed in a format that can be shared with other developers. To do this issue the following command.

.. code-block:: guess
	
	$ pip freeze > requirements.txt

If you examine ``requirements.txt`` using either the command ``more``, ``less`` or ``cat``, you will see the same information but in a slightly different format. The ``requirements.txt`` can then use to install the same setup by issuing the following command. This is incredibly useful for setting up your environment on another computer, for example.

::
	
	$ pip install -r requirements.txt

Integrated Development Environment
----------------------------------
While not absolutely necessary, a good Python-based integrated development environment (IDE) can be very helpful to you during the development process. Several exist, with perhaps JetBrains' `*PyCharm* <http://www.jetbrains.com/pycharm/>`_ and *PyDev* (a plugin of the `Eclipse IDE <http://www.eclipse.org/downloads/>`_) standing out as popular choices. The `Python Wiki <http://wiki.python.org/moin/IntegratedDevelopmentEnvironments>`_ provides an up-to-date list of Python IDEs.

Research which one is right for you, and be aware that some may require you to purchase a licence. Ideally, you'll want to select an IDE that supports integration with Django. PyCharm and PyDev both support Django integration out of the box - though you will have to point the IDE to the version of Python that you are using.



Virtual Environments
********************
We're almost all set to go! However, before we continue, it's worth pointing out that while this setup is fine to begin with, there are some drawbacks. What if you had another Python application that requires a different version to run? Or you wanted to switch to the new version of Django, but still wanted to maintain your Django 1.7 project?

The solution to this is to use `virtual environments <http://simononsoftware.com/virtualenv-tutorial/>`_. Virtual environments allow multiple installations of Python and their relevant packages to exist in harmony. This is the generally accepted approach to configuring a Python setup nowadays.  


They are pretty easy to setup, once you have pip installed, and you know the right commands. You need to install a couple of additional packages.

::
	
	$ pip install virtualenv
	$ pip install virtualenvwrapper
	

The first package provides you with the infrastructure to create a virtual environment.  See `a non-magical introduction to Pip and Virtualenv for Python Beginners <http://dabapps.com/blog/introduction-to-pip-and-virtualenv-python/>`_ by Jamie Matthews for details about using virtualenv. However, using just *virtualenv* alone is rather complex. The second package provides a wrapper to the functionality in the virtualenv package and makes life a lot easier. 


If you are using a linux/unix based OS, then to use the wrapper you need to call the following shell script from your command line:
::

	$ source virtualenvwrapper.sh

It is a good idea to add this to your bash/profile script. So you dont have to run it each and every time you want to use virtualenvironments.

Однако, если Вы используете Windows, то установите пакет `virtualenvwrapper-win <https://pypi.python.org/pypi/virtualenvwrapper-win>`_:


::

	$ pip install virtualenvwrapper-win
	

	
Now you should be all set to create a virtual environment:

::

	$ mkvirtualenv rango

You can list the virtual environments created with ``lsvirtualenv``, and you can activate a virtual environment as follows:

::

	$ workon rango
	(rango)$
	
Your prompt with change and the current virtual environment will be displayed, i.e. rango. Now within this environment you will be able to install all the packages you like, without interferring with your standard or other environements. Try ``pip list`` to see you dont have Django or Pillow installed in your virtual environment. You can now install them with pip so that they exist in your virtual environment.

Later on when we go to deploy the application, we will go through a similar process see Chapter :ref:`Deploying your Application<virtual-environment>` and set up a virtual environment on PythonAnywhere.

Репозиторий с кодом
***************
Мы также должны отметить, что при разработке кода, Вы должны всегда хранить свой код в репозитории системы контроля версий, такой как `SVN <http://subversion.tigris.org/>`_ или `GIT <http://git-scm.com/>`_. Мы не будем уделять этому время сейчас, так как это помешает приступить к немедленной разработке приложения в Django. Однако, мы даем ссылку на :ref:`краткий курс по GIT <git-crash-course>`. Мы настоятельно рекомендуем, чтобы Вы настроили GIT репозиторий для Ваших собственных проектов. Это может спасти Вас от многих проблем.


Упражнения
---------
To get comfortable with your environment, try out the following exercises.

* Установите Python 2.7.5+ и Pip.
* Play around with your CLI and create a directory called ``code``, which we use to create our projects in.
* Install the Django and Pillow packages.
* Setup your Virtual Environment
* Setup your account on GitHub
* Download and setup a Integrated Development Environemnt (like PyCharm)
* We have made the code for the book and application that you build available on GitHub, see `Tango With Django Book <https://github.com/leifos/tango_with_django_book>`_  and  `Rango Application <https://github.com/leifos/tango_with_django>`_ .
	* If you spot any errors or problem with the book, you can make a change request! 
	* If you have any problems with the exercises, you can check out the repository and see how we completed them.

