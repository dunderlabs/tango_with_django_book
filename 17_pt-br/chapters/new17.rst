.. _new17-label:



Novidades em TwD 1.7
==============

.. warning:: Aviso: Por favor, note que esta versão do livro ainda está em fase de construção. Embora ele funcione bem, alguns links e imagens precisam ser atualizados. Por favor, reporte qualquer erro, problemas, etc, ou envie solicitações de mudanças via GitHub: https://github.com/indacode/tango_with_django_book/tree/master/17_pt-br


In this version of the online tutorial / book, we have updated and added a number of things:
Nesta versão online do livro/tutorial, nós atualizamos e adicionamos uma série de coisas:

* O código foi portado para trabalhar com Django 1.7
	
	* A interação do banco de dados foi atualizada de ``syncdb`` para ``migratesql`` e  ``migrate``
	* Renderização do(s) response(s) foi atualizado de ``render_to_response`` para ``render``. Então agora não há necessidade de requisitar (request) o contexto (context) em cada view.
	* A template tag ``url`` agora está sendo usada em templates, que fornece uma referência relativa para urls em vez de uma referência absoluta...
	* Carregamento de arquivos estátivos nos templates agora é feito com {% load staticfiles %}
	* Usando ``slugify`` para criar strings URL bem formadas.

* Um novo capítulo sobre autênticação foi adicionado

	* Quando o login e registro é feito com Django-Registration-Redux (veja o Capítulo :ref:`login-redux-label`)

* O capítulo Bootstrap foi atualizado para usar Bootstrap 3.2.0 (veja o Capítulo :ref:`bootstrap-chapter`)

	* Além disso, incluso algumas notas sobre como usar Django-Bootstrap-Toolkit
	
* Um novo capítulo sobre o uso de template tags foi adicionado (veja o Capítulo :ref:`template-tag-chapter` )

* Adicionado um capítulo sobre o uso de JQuery com Django (veja o Capítulo :ref:`jquery`)

* O capítulo sobre testes foi expandido - mas o trabalho continua em andamento (veja o Capítulo :ref:`test-chapter`)

	* Incluso como usar o pacote ``coverage`` para medir a cobertura do teste (veja http://nedbatchelder.com/code/coverage/ )
	
	

	
	
	
