.. _login-redux-label:

Autenticação do Usuário com Django-Registration-Redux
=====================================================
Existem inúmeras aplicações complementares que foram desenvolvidas que fornecem mecanismos de login, cadastro e autenticação. Como a maioria das aplicações irá fornecer tais facilidades, há pouca necessidade de (re)escrever ou (re)fazer as URLs, views e templates. Neste capítulo, estaremos usando o pacote ``django-registration-redux`` para prover essas facilidades. Isso significará que nós vamos precisar refatorar nosso código - no entanto, isso vai nos fornecer uma boa experiência de usar aplicações de terceiros, e ver o quão facilmente elas podem ser plugadas no seu projeto Django, junto com facilidades de login e tudo mais. Também vai tornar nossa aplicação mais limpa.

.. note:: Esse capítulo não é obrigatório. Então você pode pulá-lo, mas estaremos assumindo no capítulo seguinte que você atualizou o mecanismo de autenticação.


Configurando o Django Registration Redux
----------------------------------------

Para começar, nós precisamos primeiro instalar o ``django-registration-redux``:

.. code-block:: bash

    $ pip install django-registration-redux


Agora que está instalado, precisamos falar ao Django que vamos usar essa aplicação. Abra o ``settings.py``, e atualize a tupla ``INSTALLED_APPS``:

.. code-block:: python

    INSTALLED_APPS = (
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'rango',
        'registration', # add in the registration package
    )

Aproveitando que você já está no ``settings.py``, você pode também adicionar:

.. code-block:: python

    REGISTRATION_OPEN = True        # Se for True, usuários podem se registrar
    ACCOUNT_ACTIVATION_DAYS = 7     # Janela de ativação de uma semana; você pode usar um valor diferente, se quiser.
    REGISTRATION_AUTO_LOGIN = True  # Se for True, o usuário será automaticamente logado.
    LOGIN_REDIRECT_URL = '/rango/'  # A página que você quer que os usuários sejam levados depois de se logar.
    LOGIN_URL = '/accounts/login/'  # A página que os usuários serão direcionados se eles não estiverem logados e
                                    # tentarem acessar uma página que requeira autenticação.
	

Essas configurações devem estar auto explicativas. Agora, no ``tango_with_django_project/urls.py`` você pode atualizar o ``urlpatterns``, de modo que ele inclua uma referência ao novo pacote de cadastro:

.. code-block:: python

    urlpatterns = patterns('',
        url(r'^admin/', include(admin.site.urls)),
        url(r'^rango/', include('rango.urls')),
        url(r'^accounts/', include('registration.backends.simple.urls')),
    )


O pacote ``django-registration-redux`` fornece uma série de backends diferentes de cadastro, dependendo das suas necessidades. Por exemplo, você pode querer um processo de cadastro em duas etapas, onde o usuário recebe um email de confirmação, e um link de verificação. Aqui vamos estar usando o processo de cadastro simples de um passo, onde o usuário configura a conta dele ao entrar com um username, email e senha, e é automaticamente logado.

Funcionalidades e Mapeamento de URL
-----------------------------------

O Django Registration Redux provê os mecanismos para diversas funções. No ``registration.backend.simple.urls``, ele fornece:

* cadastro -> ``/accounts/register/``
* cadastro completo -> ``/accounts/register/complete/``
* login -> ``/accounts/login/``
* logout -> ``/accounts/logout/``
* mudança de senha -> ``/password/change/``
* reset de senha -> ``/password/reset/``

Enquanto no ``registration.backends.default.urls`` ele também fornece as funções para ativar a conta em um processo de dois estágios:

* ativação completa (usada no cadastro de dois estágios) -> ``activate/complete/``
* falha na ativação (usada se a ação na conta falha) -> ``activite/<activation_key>/``
* email de ativação (notificação ao usuário que um email de ativação foi enviado)
	* corpo do email de ativação (uma arquivo de texto, que contém o texto do email de ativação)
	* assunto do email de ativação (um arquivo de texto, que contém a linha de assunto do email de ativação)


Agora a captura. Embora o Django Registration Redux forneça todas essas funcionalidades, ele não provê os templates. Então precisamos fornecer os templates associados com cada view.

Configurando os Templates
-------------------------
No `guia rápido da documentação <https://django-registration-redux.readthedocs.org/en/latest/quickstart.html>`_ do pacote, é fornecido uma visão geral de quais templates são necessários, mas não é claro de imediato sobre o que vai ou o que acontece em cada template.

No entanto, é possível baixar um conjunto de tempaltes a partir da conta do GitHub do `Anders Hofstee <https://github.com/macdhuibh/django-registration-templates>`_, e a partir daí você pode ver o que se passa dentro dos templates. Vamos usar esses templates como nosso guia.

Primeiro, crie uma nova pasta no diretório ``templates``, chamado ``registration``. Aí é onde nós vamos salvar todas as páginas associadas com a aplicação Django Registration Redux, bem como é aí que ele vai procurar pelos templates que precisa.

Template de Login
.................

No diretório ``templates/registration`` crie o arquivo ``login.html`` com o seguinte código:

.. code-block:: django

	{% extends "base.html" %}
	
	{% block body_block %}
	    <h1>Login</h1>
	    <form method="post" action=".">
  	        {% csrf_token %} 
  	        {{ form.as_p }}

  	        <input type="submit" value="Log in" />
  	        <input type="hidden" name="next" value="{{ next }}" />
	    </form>

	    <p>Not  a member? <a href="{% url 'registration_register' %}">Register</a>!</p>
	{% endblock %}

Perceba que sempre que uma url é referenciada, a template tag ``url`` é usada para referenciá-la. Se você visitar ``http://127.0.0.1:8000/accounts/`` então você verá a lista de mapeamentos de url, e os names associados com cada uma.

Template de Cadastro
....................
No mesmo diretório usado acima, crie o arquivo ``registration_form.html`` com o seguinte código:

.. code-block:: django

	{% extends "base.html" %}


	{% block body_block %}
	    <h1>Cadastre-se aqui</h1>
	    <form method="post" action=".">
  	        {% csrf_token %}
  	        {{ form.as_p }}

  	        <input type="submit" value="Submit" />
	    </form>
	{% endblock %}


Template de Cadastro Realizado
..............................
Ainda no mesmo diretório, crie o arquivo ``registration_complete.html`` com o seguinte código:

.. code-block:: django

	{% extends "base.html" %}

	{% block body_block %}
	    <h1>Cadastro completo</h1>
	    <p>Agora você está cadastrado!</p>
	{% endblock %}


Template de Logout
..................
Crie outro arquivo no diretório ``templates/registration``, chamado ``logout.html``, com o seguinte código:

.. code-block:: django

	{% extends "base.html" %}

	{% block body_block %}
	    <h1>Deslogado</h1>
	    <p>Agora você está deslogado.</p>
	{% endblock %}


Tente Realizar o Processo de Cadastro
.....................................
Rode o servidor e visite o link http://127.0.0.1:8000/accounts/register/

Note que o form de cadastro contém dois fields para senha - de modo que ela pode ser verificada. Tente registrar, mas entre com senhas diferentes, e veja o que acontece.

Refatorando seu Projeto
.......................

Agora você vai precisar atualizar o ``base.html`` para que as novas views/url sejam usadas:

* Atualize o link de cadastro para apontar para ``<a href="{% url 'registration_register' %}">``
* O link login deve apontar para ``<a href="{% url 'auth_login' %}">``, e
* o logout para ``<a href="{% url 'auth_logout' %}?next=/rango/">``
* No ``settings.py``, atualize ``LOGIN_URL`` para ser ``'/accounts/login/'``.

Perceba que para o logout, incluímos um ``?next=/rango/``. Isso é para quando o usuário deslogar, ele seja redirecionado para a página inicial do Rango. Se excluírmos isso, então ele será direcionado para a página de logout (mas isso não seria legal).


Modificar o Fluxo de Cadastro
.............................

Neste momento, quando usuários se cadastram, eles são levados para a página de cadastro completado com sucesso. Isso parece um pouco desajeitado, então ao invés disso, podemos pegá-lo e jogá-lo na página inicial. Isso pode ser feito ao sobrescrever o ``RegistrationView`` fornecido pelo ``registration.backends.simple.views``. Para fazer isso, no ``tango_with_django_project/urls.py``, importe  ``RegistrationView``, e adicione em uma nova classe de cadastro, e então atualize o urlpatterns como o seguinte exemplo:

.. code-block:: python

	from registration.backends.simple.views import RegistrationView
	
	# Crie uma nova classe que redirecione o usuário para a página inicial, se logar com sucesso
	class MyRegistrationView(RegistrationView):
	    def get_success_url(selfself,request, user):
	        return '/rango/'


	urlpatterns = patterns('',
	    url(r'^admin/', include(admin.site.urls)),
	    url(r'^rango/', include('rango.urls')),
	    # Adicione-a no urlpatterns para sobrescrever o pattern padrão em accounts.
	    url(r'^accounts/register/$', MyRegistrationView.as_view(), name='registration_register'),
	    url(r'^accounts/', include('registration.backends.simple.urls')),
	)




#TODO(leifos): Add in a customized registration form..



Exercícios
----------
* Forneça a funcionalidade de resetar a senha para os usuários
	