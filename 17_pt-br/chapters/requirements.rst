.. _requirements-label:

Preparando-se para o Tango
==========================
Vamos começar a instalação! Para dançar com Django, você precisará garantir que você tem tudo que você precisa instalado no seu computador e que você tem um bom entendimento do seu ambiente de desenvolvimento. Este capítulo leva você através do que você precisa e o que tem que saber.

Para este tutorial, você necessitará das seguintes peças-chave de software.

* Python versão 2.7.5+
* Django versão 1.7

Como Django é um framework para aplicações web escrito na linguagem de programação Python, você vai ser obrigado a ter um conhecimento prático de Python. Se você não tiver usando Python antes ou você deseja simplesmente aperfeiçoar suas habilidades, então nós recomendamos fortemente que você confira e trabalhe em um ou mais dos seguintes guias.

* **Um rápido tutorial** - Aprenda Python em 10 minutos, por Stavros, http://www.korokithakis.net/tutorials/.
* **O Tutorial Oficial de Python** em http://docs.python.org/2/tutorial/.
* **Um brilhante livro**: Pense Python: Como pensar como um Cientista da Computação, por Allen B. Downey, disponível online em http://www.greenteapress.com/thinkpython/.
* **Um curso online incrível**: Aprenda a programar, por Jennifer Campbell e Paul Gries em https://www.coursera.org/course/programming1.

Usando o Terminal
-----------------
A fim de criar seu ambiente, aprender como usar o *Interpretador em Linha de Comando (CLI)* fornecido pelo seu sistema operacional é realmente importante. Ao longo do curso deste tutorial, você estará interagindo com o CLI rotineiramente. Se você já está familiarizado com o uso da interface da linha de comando, você pode pular diretamente para a seção :ref:`Instalando o Software <installing-software>`.

Todos os Sistemas Operacionais baseados no UNIX usam um `terminal <http://www.ee.surrey.ac.uk/Teaching/Unix/unixintro.html>`_ de aparência semelhante. Descendentes, derivador e clones do UNIX incluindo o `Apple's OS X <http://en.wikipedia.org/wiki/OS_X>`_ e as `muitas distribuições Linux <pt.wikipedia.org/wiki/Lista_de_distribuições_de_Linux>`_ disponíveis atualmente. Todos esses sistemas operacionais contêm um conjunto básico de comandos que ajudam você a navegar através do seu sistemas de arquivos e rodar programas, tudo sem a necessidade de qualquer interface gráfica. Esta seção fornece os comandos que você deve se familiarizar.

.. note:: Este tutorial é focado para usuários de sistemas operacionais baseados em UNIX ou dericados. Embora Python e Django possam rodar em um ambiente Windows, muitos dos comandos que nós usamos neste livro são paa terminais baseados em UNIX. Esses comandos podem, entretanto, serem repetidos no Windows usando a interface gráfica do usuário, `usando o comando relativo em um tela de comando Windows<http://www.ai.uga.edu/mc/winforunix.html>`_, ou usando `Windows PowerShell <http://technet.microsoft.com/en-us/library/bb978526.aspx>`_ que fornece um CLI similar ao terminal UNIX.

Após abrir uma nova instância do terminal, você será tipicamente apresentado com algo como:

.. code-block:: guess
	
	sibu:~ leif$

Isto é chamado de *prompt*, e indica quando o sistema está esperando para executar cada comando seu. O prompt que você vê varia dependendo do sistema operacional que você está usando, mas todos geralmente são muito parecidos. No exemplo acima, existem três peças chaves de informação para observar:

* seu nome de usuário (username) e o nome do computador (username do ``leif`` e o nome do computador ``sibu``);
* seu *diretório atual de trabalho* (o til, ou ``~``); e
* o privilégio da sua conta de usuário (o sinal de dólar, ou ``$``).

O sinal de dólar (``$``) geralmente indica que o usuário é uma conta de usuário padrão. Por outro lado, um jogo da velha (``#``) pode ser usado para significar que o usuário logado tem `privilégios root <http://pt.wikipedia.org/wiki/Superusu%C3%A1rio>`_. Seja qual for o símbolo, é usado para significar que o computador está esperando sua entrada.

Abra uma janela do terminal e veja como seu prompt parece.

Quando você usar o terminal, é importante saber onde você está no sistema de arquivos. Para descobrir onde você está, você pode executar o comando ``pwd``. Isto mostraá seu atual diretório. Por exemplo, cheque a interação no terminal abaixo.

.. code-block:: guess
	
	Last login: Mon Sep 23 11:35:44 on ttys003
	sibu:~ leif$ pwd
	/Users/leif
	sibu:~ leif$

Você pode ver que o diretório atual neste exemplo é: ``Users/leif``.

Você também notará que o prompt indica que meu diretório atual é ~. Isto é porque o til (``~``) representa seu *diretócial inicial* (que chamaremos de home). O diretório base em qualquer sistema de arquivos baseados em UNIX é o *diretório raiz* (que chamaremos de root). O caminho do diretório raiz é denoado por uma simples barra (``/``).

Se você não está no seu diretório home você pode mudar o diretório (``cd``) para ele ao executar o seguinte comando.

.. code-block:: guess
	
	$ cd ~

Vamos criar um diretório chamado ``code``. Para fazer isso, use o comando que cria diretórios (``mkdir``), como mostrado abaixo.

.. code-block:: guess
	
	$ mkdir code

Para mover para entrar no diretório ``code`` recentemente criado, digite ``cd code``. Se você agora checar seu diretório de trabalho atual, você notará que você estará em ``~/code/``. Isto Isto pode também ser refletido pelo seu prompt. Note no exemplo abaixo que o diretório de trabalho atual está impresso depois do nome do computador ``sibu``.

.. note:: Sempre que nos referirmos para ``<workspace>``, nós estaremos nos referindo para seu diretório ``code``.

.. code-block:: guess
	
	sibu:~ leif$ mkdir code
	sibu:~ leif$ cd code
	sibu:code leif$ 
	sibu:code leif$ pwd
	/Users/leif/code

Para listar os arquivos que estão no diretório, você pode executar o comando ``ls``. Você pode também ver arquivos ou diretórios ocultos - if você tiver algum - você pode executar o comando ``ls -a``, onde ``a`` significa *all*. Se você voltar para o diretório home (``cd ~``) e então executar ``ls``, você verá que tem algo chamado ``code`` no seu diretório home.

Para saber um pouco mais sobre o que está no seu diretório, execute um ``ls -l``. Isto fornecerá uma *listagem* mais detalhada dos seus arquivos e se é um diretório ou não (denotado por um ``d`` no começo da linha).

.. code-block:: guess
	
	sibu:~ leif$ cd ~ 
	sibu:~ leif$ ls -l 
	
	drwxr-xr-x   36 leif  staff    1224 23 Sep 10:42 code

A saída também contêm informações sobre `permissões associadas ao diretório <http://www.infowester.com/linuxpermissoes.php>`_, quem criou (``leif``), o grupo (``staff``), o tamanho, a data/hora em que o arquivo foi modificado, e, claro, o nome.

Você também pode achar útil ser capaz de editar arquivos dentro do seu terminal. Existem muitos editores que você pode usar - alguns dos quais pode já estar instalado no seu computador. O editor `nano <http://www.nano-editor.org/>`_ por exemplo, é um editor simples, ao contrário do `vi <http://pt.wikipedia.org/wiki/Vi>`_ que pode levar algum tempo para aprender. Abaixo está uma lista de comandos UNIX costumeiramente usados que você achará útil.

Comandos Básicos
****************
Todos os sistemas operacionais baseados em UNIX vêm com uma série de comandos embutidos - com o foco maior exclusivamente para gerenciamento de arquivos. Os comandos que você usará mais frequentemente estão listados abaixo, cada um com uma pequena explicação sobre o que eles fazem e como usá-los.

- ``pwd``: *Imprime* na tela do seu terminal seu diretório de trabalho atual. O caminho completo de onde você está é mostrado.
- ``ls``: Mostra no terminal uma lista dos arquivos no seu diretório atual. Por padrão, você não pode ver os tamanhos dos arqvuiso - isto pode ser conseguido ao adicionar ``-lh`` ao ``ls``, dando o comando ``ls -lh``.
- ``cd``: Em conjunto com um caminho, permite você *mudar* seu *diretório* de trabalho. Por exemplo, o comando ``cd /home/leif`` muda o diretório de trabalho atual para ``/home/leif/``. Você pode também subir um nível de diretório sem ter que fornecer o `caminho absoluto <http://www.uvsc.edu/disted/decourses/dgm/2120/IN/steinja/lessons/06/06_04.html>`_ ao usar dois pontos, por exemplo, ``cd ..``.
- ``cp``: copia arquivos e/ou diretório. Você precisa fornecer o *original* e o *destino*. Por exemplo, para fazer uma cópia de um arquivo ``input.py`` no mesmo diretório, você executaria o comando ``cp input.py input_backup.py``.

- ``mv``: Move arquivos ou diretórios. Você precisa fornecer o *original* e o *destino*. Este comando é também usado para renomear arquivos. Por exemplo, para renomear ``numbers.txt`` para ``letters.txt``, execute o comando ``mv numbers.txt letters.txt``. Para mover um arquivo para um diretório diferente, você iria fornecer ou um caminho absoluto ou relativo como parte do destino - algo como isto ``mv numbers.txt /home/david/numbers.txt``.

- ``mkdir``: Cria um diretório no seu diretório atual. Você precisa fornece um nome para o novo diretório depois do comando ``mkdir``. Por exemplo, se o seu diretório atual era ``/home/david/`` e você executou ``mkdir music``, você deverá então ter um diretório ``/home/david/music``. Você precisará, em seguida, executar um ``cd`` para entrar no diretório recentemente criado.

- ``rm``: Abreviação para *remoção*, este comando remove ou deleta arquivos do seu sistema de arquivos. Você precisa fornecer o(s) nome(s) do(s) arquivo(s) que você deseja remover. Após executar um comando ``rm``, você será perguntado se você deseja deletar os arquivos selecionados. Você também pode remover diretórios `usando a opção recursiva <http://www.computerhope.com/issues/ch000798.htm>`_, Seja cuidadoso com este comando - recuperação de arquivos deletados é muito difícil, se não impossível!

- ``rmdir``: Um comando alternativo para remover diretórios do seu sistema de arquivos. Forneça um diretório que você deseja remover. Novamente, seja cuidadoso: você não será perguntado para confirmar suas intenções ao apagar.

- ``sudo``: Um programa que permite que você rode comando com os privilégios de segurança de outro usuário. Geralmente, o programa é usado para rodar outros programas como ``root`` - o `super usuário <http://pt.wikipedia.org/wiki/Superusuário>`_ de qualquer sistema operacional baseado ou derivado do UNIX.

.. note:: Isto é apenas um resumo da lista de comandos. Confira a documentação do ubuntu em `Usando o terminal <https://help.ubuntu.com/community/UsingTheTerminal>`_ para uma visão mais detalhada, ou o `Cheat Sheet <http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/>`_ feito por FOSSwire para ser um rápido guia de referências.

.. _installing-software:

Instalando os Softwares
---------------------
Agora que você tem um bom conhecimento de como interagir com o terminal, você pode começar a instalar os softwares requeridos para este tutorial.

Instalando Python
-----------------
Então, como é que você vai instalar o Python 2.7.5 no seu computador? Você pode já ter Python instalado no seu computador - e se você estiver usando uma distribuição Linux ou OS X, você definitivamente já o tem instalado. Algumas das funcionalidades desses sistemas operacionais `estão implementadas em Python <http://en.wikipedia.org/wiki/Yellowdog_Updater,_Modified>`_, daí a necessidade de um interpretador.

Infelizmente, quase todos os sistemas operacionais modernos utilizam uma versão do Python que mais antiga do que a que nós estamos requerendo para este tutorial. Existem muitas maneiras diferentes nas quais você pode instalar Python, e muitas delas são, infelizmente, bastante complicadas de realizar. Nós demonstraremos a abordagem mais comumente usada, e fornecer links adicionais de leitura para mais informações.

.. warning:: Esta seção detalhará como rodar Python 2.7.5 *ao lado* da sua atual instalação do Python. É considerada como má prática remover do seu sistema operacional a instalação Padrão do Python e substitui-la por uma nova versão. Fazer isso pode quebrar as funcionalidades do seu sistema operacional!

Apple OS X
..........
A maneira mais simples de ter Python 2.7.5 instalado no seu Mac é baixando e rodando o simples instalador fornecido no site oficial Python. Você pode baixar o instalador ao visitar a página em http://www.python.org/getit/releases/2.7.5/.

.. warning:: Garanta que você baixou o arquivo ``.dmg`` que é relevante para sua versão do OS X!

#. Depois que você baixou o arquivo ``.dmg``, dê um clique duplo no `Finder <http://pt.wikipedia.org/wiki/Finder>`_.
#. O arquivo monta como um disco separado e uma nova janela do Finder é aprensetada para você.
#. Duplo clique no arquivo ``Python.mpkg``. Isto iniciará o instalador Python.
#. Continue através das diversas tela até o ponto onde você já está pronto para instalar o software. Você pode ter que fornecer sua senha para confirmar que você deseja instalar.
#. Uma vez completada, feche o instalador e ejete o disco Python. Você pode agora deleter o arquivo ``.dmg`` baixado.

Você deve ter agora uma versão atualizada do Python instalada, pronta para o Django! Fácil, né?

Distribuições Linux
...................
Infelizmente, existem muitas maneiras diferentes em que você pode baixar, instalar e rodar uma versão atualizada do Python na sua distribuição Linux. Para piorar a situação, metodologias variam de distribuições para distribuições. Por exemplo, as instruções para instalar Python no `Fedora <http://fedoraproject.org/>`_ pode diferenciar daquelas para instalar no `Ubuntu <http://www.ubuntu.com/>`_.

Entretanto, nem toda esperança está perdida. Uma ferramenta incrível (ou um *Gerenciador de ambiente Python*) chamado `pythonbrew <https://github.com/utahta/pythonbrew>`_ pode nos ajudar a resolver este problema. Ela fornece uma maneira fácil para instalar e gerenciar diferentes versões do Python, o que significa que você pode deixar a instalação padrão do Python no seu sistema operacional sozinha. Irrá!

Retirando as instruções fornecidas `da página do pythonbrew no Github <https://github.com/utahta/pythonbrew>`_ e `desta thread na página do Stack Overflow <http://stackoverflow.com/questions/5233536/python-2-7-on-ubuntu>`_, os seguintes passos irão instalar o Python 2.7.5 na sua distribuição Linux.

#. Abra uma nova instância do Terminal
#. Execute o comando ``curl -kL http://xrl.us/pythonbrewinstall | bash``. Isto irá baixar o instalador e executar executá-lo dentro do seu terminal para você. Isto instala o pythonbrew dentro do seguinte diretório ``~/.pythonbrew``. Lembre, o til (``~``) representa o seu diretório home!
#. Você precisa então editar o arquivo ``~/.bashrc``. Em um editor de texto (como o ``gedit``, ``nano``, ``vi`` ou ``emacs``), e adicione o seguinte em uma nova linha no final do arquivo ``~/.bashrc``: ``[[ -s $HOME/.pythonbrew/etc/bashrc ]] && source $HOME/.pythonbrew/etc/bashrc``
#. Uma vez que você salvou as alterações no arquivo ``~/.bashrc``, feche seu terminal e abra um novo. Isto permitirar que as alterações sejam então aplicadas.
#. Execute o comando ``pythonbrew install 2.7.5`` para instalar o Python 2.7.5.
#. Você precisa então *mudar* para o Python 2.7.5 para *ativar* a nova instalação. Faça isto executando o comando ``pythonbrew switch 2.7.5``.
#. Python 2.7.5 deverá agora estar instalado e pronto para uso.

.. note:: Diretórios e arquivos que começam com um ponto podem ser considerados equivalentes aos *arquivos ocultos* do Windows.`Arquivos com ponto <http://en.wikipedia.org/wiki/Dot-file>`_ normalmente não são visíveis no visualizador de diretórios, e são comumente usados para configurações de arquivos. Você pode usar o comando ``ls`` para visualizar arquivos ocultos ao adicionar o ``-a`` no final do comando, ficando da seguinte forma ``ls -a``.

.. _requirements-install-python-windows:

Windows
.......
Por padrão, o Microsoft Windows vem sem nenhuma instalação do Python. Isto significa que você não tem que se preocupar em deixar versões diferentes juntas; instalando do início deve funcionar bem. Você pode baixar uma versão 64-bit ou 32-bit do Python a partir do `site oficial Python <http://www.python.org/download/>`_. Se você não está certo sobre qual baixar, você pode descobrir se o seu computador é 32-bit ou 64-bit ao olhar nas instruções fornecidas `no site da Microsoft <http://windows.microsoft.com/en-gb/windows7/32-bit-and-64-bit-windows-frequently-asked-questions>`_.

#. Quano o instalador estiver baixado, abra o arquivo no local onde baixou.
#. Siga os passos na tela para instalar o Python.
# Feche o instalador assim que completar a instalação, e delete os arquivos baixados.


Assim que o instalador terminou, você deve ter uma versão do Python pronta para uso. Por padrão, Python 2.7.5 está instalado na pasta ``C:\Python27``. Nós recomendamos que você deixe esse caminho como está.

Após a conclusão da instalação, abra um prompt de comando e execute o comando ``python``. Se você ver o prompt do Python, a instalação foi um sucesso. Entretanto, em algumas circunstâncias, o instalador pode não setar suas variáveis de ambiente do Windows no ``PATH`` corretamente. Isto resultará no comando ``python`` não ter sido encontrado. No Windows 7, você pode corrigir isto fazendo o seguinte:

#. Clique no *iniciar*, então com o botão direito clique em *Meu Computador* e selecione *Propriedades*.
#. Clique em *Avançado*.
#. Clique no botão *Variáveis de Ambiente*.
#. Na lista *Variáveis do Sistema*, procura a variável chamada *Path*, clique nela, e então clique no botão *Editar*.
#. No fim da linha, coloque ``;C:\python27;C:\python27\scripts``. Não esqueça do ponto e vírgula -  e certamente *não* adicione um espaço.
#. Cliquem em OK em cada janela para salvar suas mudanças.
#. Fecha qualquer janela do prompt de comandos aberta, e abra uma nova instância, e tenta agora rodar o comando ``python`` novamente.

Isto deve fazer a sua instalação do Python funcionar. No Windows XP, `tem instruções ligeiramente diferentes <http://www.computerhope.com/issues/ch000549.htm>`_, e `com o Windows 8 fazer desta forma <http://stackoverflow.com/a/14224786>`_.

Configurando o ``PYTHONPATH``
*****************************
Agora com Python instalado, nós precisamos verificar se a instalação foi bem sucedida. Para fazer isto, nós precisamos checar se a `variável de ambiente <http://pt.wikipedia.org/wiki/Vari%C3%A1vel_de_ambiente>`_ ``PYTHONPATH`` está configurada corretamente. ``PYTHONPATH`` fornece o interpretador Python com a localização dos `pacotes e módulos <http://stackoverflow.com/questions/7948494/whats-the-difference-between-a-python-module-and-a-python-package>`_ adicionais do Python que adicionam funcionalidades extras para a instalação base do Python. Sem a correta configuração do ``PYTHONPATH``, nós não seremos capazes de instalar e usar o Django!

Primeiro, vamos verificar se nossa variável ``PYTHONPATH`` existe. Dependendo da técnica de instalação que você escolheu, isto pode ou não ter sido feito pra você. Para fazer isto no seu sistema operacional baseado no UNIX, execute o seguinte comando no terminal.

.. code-block:: guess

	$ echo $PYTHONPATH

Em uma máquina Windows, abra o prompt de comando e execute o seguinte.

	$ echo %PYTHONPATH%

Se tudo funcionar, você deve então ver uma saída que parece com o exemplo abaixo. Em uma máquina Windows, você verá obviamente um caminho Windows, provavelmente proveniente da unidade C.

.. code-block:: guess
	
	/opt/local/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages:

Este é o caminho para o seu diretório ``site-packages`` da sua instalação Python, onde pacotes e módulos Python adicionais estão armazenados. Se você vê um caminho, você pode continuar para a próxima parte deste tutorial. Se, no entanto, você não vê nada, você precisará fazer um pequeno trabalho de detetive para descobrir o caminho. Em uma instalação Windows, isto deve ser um exercício trivial: ``site-packages`` está localizado dentro da pasta ``lib`` do diretório da sua instalação Python. Por exemplo, se você instalou Python em ``C:\Python27``, ``site-packages`` estará em ``C:\Python27\Lib\site-packages\``.



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

Using Setuptools and Pip
************************
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

Installing Django
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

Again, use ``sudo`` if required. 


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

However, if you are using windows, then install the `virtualenvwrapper-win <https://pypi.python.org/pypi/virtualenvwrapper-win>`_ package:


::

	$ pip install virtualenvwrapper-win
	

	
Now you should be all set to create a virtual environment:

::

	$ mkvirtualenv rango

You can list the virtual environments created with ``lsvirtualenv'', and you can activate a virtual environment as follows:

::

	$ workon rango
	(rango)$
	
Your prompt with change and the current virtual environment will be displayed, i.e. rango. Now within this environment you will be able to install all the packages you like, without interferring with your standard or other environements. Try ``pip list'' to see you dont have Django or Pillow installed in your virtual environment. You can now install them with pip so that they exist in your virtual environment.

Later on when we go to deploy the application, we will go through a similar process see Chapter :ref:`Deploying your Application<virtual-environment>` and set up a virtual environment on PythonAnywhere.

Code Repository
***************
We should also point out that when you develop code, you should always house your code within a version-controlled repository such as `SVN <http://subversion.tigris.org/>`_ or `GIT <http://git-scm.com/>`_. We won't be going through this right now so that we can get stuck into developing an application in Django. We have however provided a :ref:`crash course on GIT <git-crash-course>`. We highly recommend that you set up a GIT repository for your own projects. Doing so could save you from disaster.




Exercises
---------
To get comfortable with your environment, try out the following exercises.

* Install Python 2.7.5+ and Pip.
* Play around with your CLI and create a directory called ``code``, which we use to create our projects in.
* Install the Django and Pillow packages.
* Setup your Virtual Environment
* Setup your account on GitHub
* Download and setup a Integrated Development Environemnt (like PyCharm)
* We have made the code for the book and application that you build available on GitHub, see `Tango With Django Book <https://github.com/leifos/tango_with_django_book>`_  and  `Rango Application <https://github.com/leifos/tango_with_django>`_ .
	* If you spot any errors or problem with the book, you can make a change request! 
	* If you have any problems with the exercises, you can check out the repository and see how we completed them.


