# Sistema para Portal Biblioteca

<p align="center">
  <a href="#">
    <img src="https://img.shields.io/badge/Aula-Biblioteca-brightgreen.svg" alt="Aula-Biblioteca">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Python-blue.svg" alt="Python">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Django-orange.svg" alt="Django">
  </a>
</p>

Aula Djando 02. Projeto utilizando o Django para ser desenvolvido na Aula de GAC116 - Programação Web.

O objetivo desse projeto é criar um sistema para gestão de biblioteca.

Este tutorial foi elaborado baseado no tutorial disponível no [curso de django da w3schools](https://www.w3schools.com/django/index.php).

## Linguagens Utilizadas

* Python - [link](https://www.python.org/)
* JavaScript - [link](https://www.javascript.com/)
* HTML - [link](https://html.com/)
* CSS - [link](https://www.w3schools.com/css/)

## Framework Utilizados

* Django - [link](https://www.djangoproject.com/)
* Bootstrap - [link](https://getbootstrap.com/)
* Chart.js - [link](https://www.chartjs.org/)

## Ferramentas Utilizadas

* Visual Studio Code - [link](https://code.visualstudio.com/)
* SQLite Online - [link](https://sqliteonline.com/)
* DB Browser for SQLite - [link](https://sqlitebrowser.org/)
* Pip - [link](https://pypi.org/project/pip/)
* VirtualEnv - [link](https://virtualenv.pypa.io/)

## Comandos utilizados na criação deste projeto

### Baixando o Repositório

Inicilamente, baixe o repositório do [link](https://github.com/ufla-prog-web/aula-django-02) clicando em `Code` e `Download ZIP`.

### Criação da Pasta do Projeto

Em seguida, crie a pasta do projeto dentro da pasta baixada do github:

```bash
mkdir portal_biblioteca
cd portal_biblioteca/
```

### Instalação do Python

Se necessário, instale o Python (testado na versão 3.10.12) [link](https://www.python.org/downloads/).

Verifique a versão instalada do Python (para ter certeza que tudo ocorreu bem):

```bash
python3 --version
```

### Instalação do Pip

Se necessário, instale o pip (testado na versão 23.2.1):

```bash
sudo apt install python3-pip
```

Verifique a versão instalada do pip (para ter certeza que tudo ocorreu bem):

```bash
pip3 --version
```

### Instalação do VirtualEnv

Se necessário, instale o virtualenv (testado na versão 20.24.1):

```bash
pip3 install virtualenv
```

Verifique a versão instalada do virtualenv (para ter certeza que tudo ocorreu bem):

```bash
virtualenv --version
```

### Criação do Ambiente Virtual

Crie o ambiente virtual para isolar as instalações Python:

```bash
virtualenv venv
```

Ativei o ambiente virtual para fazer as instalações de forma isolada:

**Sistema Operacional:** Unix/Mac OS:

```bash
source venv/bin/activate
```

**Sistema Operacional:** Windows

```bash
venv\Scripts\activate.bat
```

Quando desejar sair do ambiente virtual, basta digitar:

```bash
(venv) ... $ deactivate
```

### Instalação do Django

Instale o django dentro do ambiente virtual criado (testado na versão 4.2.5):

```bash
(venv) ... $ pip3 install django
```

Verifique a versão instalada do django (para ter certeza que tudo ocorreu bem):

```bash
(venv) ... $ django-admin --version
```

### Criação do Projeto Django

Crie um projeto em django:

```bash
(venv) ... $ django-admin startproject portal_biblioteca .
```

### Executando o Projeto

Inicie a execução do projeto django criado:

```bash
(venv) ... $ python3 manage.py runserver
```

Acesse através do navegdor web a página [http://127.0.0.1:8000/](http://127.0.0.1:8000/). Uma página padrão do django deve aparecer.

### Criando um Aplicativo

Execute o comando abaixo para criar um aplicativo chamado `biblioteca` dentro do projeto `portal_biblioteca`:

```bash
(venv) ... $ python3 manage.py startapp biblioteca
```

o comando abaixo também faz a mesma coisa:

```bash
(venv) ... $ django-admin startapp biblioteca
```

### Criando a primeira View no Django

Edite o arquivo de `views.py` (na pasta `biblioteca`) e coloque o seguinte conteúdo:

```python
from django.shortcuts import render
from django.http import HttpResponse

def teste(request):
    return HttpResponse("Olá Mundo! - Portal Biblioteca")
```

Em seguida, crie um arquivo nomeado `urls.py` na mesma pasta do arquivo `views.py` e digite este código nele:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('teste/', views.teste, name='teste'),
]
```

Existe um arquivo chamado `urls.py` na pasta `biblioteca`, abra esse arquivo e coloque o seguinte conteúdo nesse arquivo.

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('biblioteca.urls')),
    path('admin/', admin.site.urls),
]
```

Em seguida, execute o projeto django (veja se está tudo funcionando):

```bash
(venv) ... $ python3 manage.py runserver
```

OBS: deve aparecer uma mensagem de erro (Page not found) na página [http://127.0.0.1:8000](http://127.0.0.1:8000).

OBS: assim, teste a url: [http://127.0.0.1:8000/teste/](http://127.0.0.1:8000/teste/`)

### Criando o primeiro Template no Django

Crie uma pasta `templates` dentro da pasta `biblioteca` e crie um arquivo HTML chamado `paginateste.html`.

Abra o arquivo HTML e insira o seguinte:

```html
<!DOCTYPE html>
<html>
<body>

<h1>Olá Mundo!</h1>

<p>Bem-vindo ao meu primeiro projeto Django!</p>

</body>
</html>
```

Agora é necessário modificar a visualização. Abra o arquivo `views.py` e substitua o método de visualização `teste` por este:

```python
from django.http import HttpResponse
from django.template import loader

def teste(request):
    template = loader.get_template('paginateste.html')
    return HttpResponse(template.render())
```

Para poder trabalhar com coisas mais complicadas do que "Hello World!", temos que dizer ao Django que um novo aplicativo foi criado. Isso é feito no arquivo `settings.py` da pasta `portal_biblioteca`. Procure a lista `INSTALLED_APPS[]` e adicione o aplicativo `biblioteca` que foi criado assim:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'biblioteca',  # inclua o app criado aqui
]
```

Em seguida, execute este comando:

```bash
(venv) ... $ python3 manage.py migrate
```

Em seguida, execute o projeto django (veja se está tudo funcionando):

```bash
(venv) ... $ python3 manage.py runserver
```

Em seguida, acesse a URL [http://127.0.0.1:8000/teste/](http://127.0.0.1:8000/teste/`)

### Melhorando as Telas do Django

Agora, iremos criar a tela principal do nosso sistema.

Assim, edite o arquivo `urls.py` na pasta `biblioteca` e coloque o seguinte conteúdo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.principal, name='principal'),
    path('teste/', views.teste, name='teste'),
]
```

Em seguida, edite o arquivo `views.py` na pasta `biblioteca` e coloque o seguinte conteúdo:

```python
from django.http import HttpResponse
from django.template import loader

def principal(request):
    template = loader.get_template('principal.html')
    return HttpResponse(template.render())

def teste(request):
    template = loader.get_template('paginateste.html')
    return HttpResponse(template.render())
```

Em seguida, crie um arquivo HTML com nome `principal.html` na pasta `templates` com o seguinte conteúdo:

```html
{% load static %}

<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="{% static 'mystyles.css' %}"> 
        <title>Portal Biblioteca</title>
    </head>
    <body>
        <div class="topnav">
            <a href="/">PRINCIPAL</a> |
            <a href="/livros">LIVROS</a> |
            <a href="/tccs">TCCs</a> |
            <a href="/dashboard">DASHBOARD</a> |
            <a href="/login">LOGIN</a> |
            <a href="/cadastre-se">CADASTRE-SE</a>
        </div>
        <div class="main">
            <h1>Portal Biblioteca</h1>
            <img src="{% static 'logo-portal.png' %}" alt="logo-portal" width="400" height="300">
        </div>
    </body>
</html>
```

Em seguida, crie uma pasta chamada `staticfiles` na raiz do projeto. Crie também uma pasta chamada `productionfiles` também na raiz do projeto.

Em seguida, crie um arquivo CSS chamado `mystyles.css` na pasta `staticfiles` com o seguinte conteúdo:

```css
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600&display=swap');
body {
  margin:0;
  font: 600 18px 'Source Sans Pro', sans-serif;
  letter-spacing: 0.64px;
  color: #585d74;
}
.topnav {
  background-color:#375BDC;
  color:#ffffff;
  padding:10px;
}
.topnav a:link, .topnav a:visited {
  text-decoration: none;
  color: #ffffff; 
}
.topnav a:hover, .topnav a:active {
  text-decoration: underline;
}
.mycard {
  background-color: #f1f1f1;
  background-image: linear-gradient(to bottom, #375BDC, #4D70EF); 
  background-size: 100% 120px;
  background-repeat: no-repeat;
  margin: 40px auto;
  width: 600px;
  border-radius: 5px;
  box-shadow: 0 5px 7px -1px rgba(51, 51, 51, 0.23); 
  padding: 20px;
}
.mycard h1 {
  text-align: center;
  color:#ffffff;
  margin: 20px 0 60px 0;
}
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
li {
  background-color: #ffffff;
  background-image: linear-gradient(to right, #375BDC, #4D70EF); 
  background-size: 50px 60px;
  background-repeat: no-repeat;
  cursor: pointer;
  transition: transform .25s;
  border-radius: 5px;
  box-shadow: 0 5px 7px -1px rgba(51, 51, 51, 0.23);
  padding: 15px;
  padding-left: 70px;
  margin-top: 5px;
}
li:hover {
  transform: scale(1.1);
}
a:link, a:visited {
  color: #375BDC; 
}
.main, .main h1 {
  text-align:center;
  color:#375BDC;
}
```

Em seguida, baixe o arquivo chamado `logo-portal.png` do github e coloque dentro da pasta `staticfiles`.

Em seguida, no final do arquivo `settings.py` na pasta `portal_biblioteca` adicione o seguinte conteúdo:

```python
STATIC_ROOT = BASE_DIR / 'productionfiles'

STATIC_URL = 'static/'

#Add this in your settings.py file:
STATICFILES_DIRS = [
    BASE_DIR / 'staticfiles'
]
```

Em seguida, execute o seguinte comando abaixo:

```bash
(venv) ... $ python3 manage.py collectstatic
```

OBS: O comando acima informa ao Django para entrar nas pastas com arquivos estáticos e fazer uma cópia de todos os arquivos dessas pastas para a pasta `productionfiles`.

Em seguida, execute o projeto django:

```bash
(venv) ... $ python3 manage.py runserver
```

Em seguida, acesse a URL [http://127.0.0.1:8000](http://127.0.0.1:8000`)

Repare que os links para as outras páginas ainda não funcionam. Isso é esperado visto que ainda não criamos as outras páginas e rotas.

### Criando a Página Livros no Django

Agora, iremos criar a tela da página de Livros do nosso sistema.

Assim, edite o arquivo `urls.py` na pasta `biblioteca` e coloque o seguinte conteúdo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.principal, name='principal'),
    path('livros', views.livros, name='livros'),
]
```

**OBS:** Foi removida a linha de teste do arquivo `urls.py`.

Em seguida, edite o arquivo `views.py` na pasta `biblioteca` e coloque o seguinte conteúdo:

```python
from django.http import HttpResponse
from django.template import loader

def principal(request):
    template = loader.get_template('principal.html')
    return HttpResponse(template.render())

def livros(request):
    template = loader.get_template('livros.html')
    context = {
        'livros': [
            {
                "nome": "O Senhor dos Anéis",
                "autor": "J.R.R. Tolkien",
                "ano": 1954
            },
            {
                "nome": "1984",
                "autor": "George Orwell",
                "ano": 1949
            },
            {
                "nome": "Dom Quixote",
                "autor": "Miguel de Cervantes",
                "ano": 1605
            },
            {
                "nome": "Cem Anos de Solidão",
                "autor": "Gabriel García Márquez",
                "ano": 1967
            },
            {
                "nome": "Harry Potter e a Pedra Filosofal",
                "autor": "J.K. Rowling",
                "ano": 1997
            },
            {
                "nome": "Crime e Castigo",
                "autor": "Fiódor Dostoiévski",
                "ano": 1866
            },
            {
                "nome": "A Metamorfose",
                "autor": "Franz Kafka",
                "ano": 1915
            },
            {
                "nome": "O Grande Gatsby",
                "autor": "F. Scott Fitzgerald",
                "ano": 1925
            },
            {
                "nome": "Orgulho e Preconceito",
                "autor": "Jane Austen",
                "ano": 1813
            },
            {
                "nome": "Os Miseráveis",
                "autor": "Victor Hugo",
                "ano": 1862
            }
        ]
    }
    return HttpResponse(template.render(context, request))
```

**OBS:** Foi removida a função teste do arquivo `views.py`.

Em seguida, crie um arquivo HTML com nome `livros.html` na pasta `templates` com o seguinte conteúdo:

```html
{% load static %}

<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="{% static 'mystyles.css' %}"> 
        <title>Portal Biblioteca - Livros</title>
    </head>
    <body>
        <div class="topnav">
            <a href="/">PRINCIPAL</a> |
            <a href="/livros">LIVROS</a> |
            <a href="/tccs">TCCs</a> |
            <a href="/dashboard">DASHBOARD</a> |
            <a href="/login">LOGIN</a> |
            <a href="/cadastre-se">CADASTRE-SE</a>
        </div>
        <div class="mycard">
            <h1>Livros</h1>
            <ul>
                {% for l in livros %}
                <li>{{ l.nome }} | {{ l.autor }} | {{ l.ano }} </li>
                {% endfor %}
            </ul>
        </div>
    </body>
</html>
```

**OBS:** Remova o arquivo `paginateste.html` da pasta `templates`.

Em seguida, execute o projeto django:

```bash
(venv) ... $ python3 manage.py runserver
```

Em seguida, acesse a URL [http://127.0.0.1:8000](http://127.0.0.1:8000`) tanto na página principal quanto a página livros.

### Criando a Página TCCs no Django

Agora, iremos criar a tela da página de TCCs do nosso sistema.

Assim, edite o arquivo `urls.py` na pasta `biblioteca` e coloque o seguinte conteúdo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.principal, name='principal'),
    path('livros', views.livros, name='livros'),
    path('tccs', views.tccs, name='tccs'),
]
```

Em seguida, adicione ao arquivo `views.py` na pasta `biblioteca` o seguinte método:

```python
...

def tccs(request):
    template = loader.get_template('tccs.html')
    context = {
        'tccs': [
            {
                "id": 1,
                "titulo": "Sistemas de Recomendação Personalizados",
                "autor": "Maria Silva",
                "orientador": "Prof. João Santos",
                "ano": 2021
            },
            {
                "id": 2,
                "titulo": "Segurança de Redes em Ambientes Corporativos",
                "autor": "Pedro Oliveira",
                "orientador": "Profa. Ana Rodrigues",
                "ano": 2020
            },
            {
                "id": 3,
                "titulo": "Inteligência Artificial Aplicada à Análise de Dados",
                "autor": "Luana Costa",
                "orientador": "Prof. André Martins",
                "ano": 2019
            },
            {
                "id": 4,
                "titulo": "Desenvolvimento de Aplicativos Móveis para Saúde",
                "autor": "Carlos Santos",
                "orientador": "Profa. Maria Pereira",
                "ano": 2018
            },
            {
                "id": 5,
                "titulo": "Aprendizado de Máquina na Detecção de Fraudes",
                "autor": "Rafael Ferreira",
                "orientador": "Prof. Marcos Lima",
                "ano": 2017
            }
        ]
    }
    return HttpResponse(template.render(context, request))
```

Em seguida, crie um arquivo HTML com nome `tccs.html` na pasta `templates` com o seguinte conteúdo:

```html
{% load static %}

<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="{% static 'mystyles.css' %}"> 
        <title>Portal Biblioteca - TCCs</title>
    </head>
    <body>
        <div class="topnav">
            <a href="/">PRINCIPAL</a> |
            <a href="/livros">LIVROS</a> |
            <a href="/tccs">TCCs</a> |
            <a href="/dashboard">DASHBOARD</a> |
            <a href="/login">LOGIN</a> |
            <a href="/cadastre-se">CADASTRE-SE</a>
        </div>
        <div class="mycard">
            <h1>Trabalhos de Conclusão de Curso</h1>
            <ul>
                {% for tcc in tccs %}
                <li><em>Título:</em> {{ tcc.titulo }} <br> <em>Autor:</em> {{ tcc.autor }} </li>
                {% endfor %}
            </ul>
        </div>
    </body>
</html>
```

Em seguida, execute o projeto django:

```bash
(venv) ... $ python3 manage.py runserver
```

Em seguida, acesse a URL [http://127.0.0.1:8000](http://127.0.0.1:8000`) na página principal, acesse a página livros e a página de TCCs.

### Adicionando Tela de Detalhes aos TCCs

Agora, iremos adicionar uma tela de detalhes sobre os TCCs em nosso sistema.

Assim, edite o arquivo `urls.py` na pasta `biblioteca` e coloque o seguinte conteúdo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.principal, name='principal'),
    path('livros', views.livros, name='livros'),
    path('tccs', views.tccs, name='tccs'),
    path('tccs/detalhes/<int:id>', views.tcc_detalhes, name='tcc_detalhes'),#adicionado
]
```

Em seguida, adicione ao arquivo `views.py` na pasta `biblioteca` o seguinte método:

```python
...

def tcc_detalhes(request, id):
    tccs = [
        {
            "id": 1,
            "titulo": "Sistemas de Recomendação Personalizados",
            "autor": "Maria Silva",
            "orientador": "Prof. João Santos",
            "ano": 2021
        },
        {
            "id": 2,
            "titulo": "Segurança de Redes em Ambientes Corporativos",
            "autor": "Pedro Oliveira",
            "orientador": "Profa. Ana Rodrigues",
            "ano": 2020
        },
        {
            "id": 3,
            "titulo": "Inteligência Artificial Aplicada à Análise de Dados",
            "autor": "Luana Costa",
            "orientador": "Prof. André Martins",
            "ano": 2019
        },
        {
            "id": 4,
            "titulo": "Desenvolvimento de Aplicativos Móveis para Saúde",
            "autor": "Carlos Santos",
            "orientador": "Profa. Maria Pereira",
            "ano": 2018
        },
        {
            "id": 5,
            "titulo": "Aprendizado de Máquina na Detecção de Fraudes",
            "autor": "Rafael Ferreira",
            "orientador": "Prof. Marcos Lima",
            "ano": 2017
        }
    ]
    tcc = tccs[id-1]
    template = loader.get_template('tcc_detalhes.html')
    context = {
        'tcc': tcc,
    }
    return HttpResponse(template.render(context, request))
```

Em seguida, crie um arquivo HTML com nome `tcc_detalhes.html` na pasta `templates` com o seguinte conteúdo:

```html
{% load static %}

<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="{% static 'mystyles.css' %}"> 
        <title>Portal Biblioteca - TCCs - Detalhes</title>
    </head>
    <body>
        <div class="topnav">
            <a href="/">PRINCIPAL</a> |
            <a href="/livros">LIVROS</a> |
            <a href="/tccs">TCCs</a> |
            <a href="/dashboard">DASHBOARD</a> |
            <a href="/login">LOGIN</a> |
            <a href="/cadastre-se">CADASTRE-SE</a>
        </div>
        <div class="mycard">
            <h1>Trabalho de Conclusão de Curso</h1>
            <p><em>Título:</em> {{ tcc.titulo }} </p>
            <p><em>Autor:</em> {{ tcc.autor }}</p>
            <p><em>Orientador:</em> {{ tcc.orientador }}</p>
            <p><em>Ano:</em> {{ tcc.ano }}</p>
        </div>

        <p><center>Volte para <a href="/tccs">TCCs</a></center></p>
        
    </body>
</html>
```

Em seguida, edite o HTML com nome `tccs.html` na pasta `templates` com o seguinte conteúdo:

```html
...
            <ul>
                {% for tcc in tccs %}
                <li onclick="window.location = 'tccs/detalhes/{{ tcc.id }}'"><em>Título:</em> {{ tcc.titulo }} <br> <em>Autor:</em> {{ tcc.autor }} </li>  <!--Linha editada -->
                {% endfor %}
            </ul>
...
```

Em seguida, execute o projeto django:

```bash
(venv) ... $ python3 manage.py runserver
```

Em seguida, acesse a URL [http://127.0.0.1:8000](http://127.0.0.1:8000`) na página principal, a página de TCCs e clique sobre um TCC para ver os detalhes.

### Adicionando Template Mestre no Django

A seguir iremos adicionar um template mestre (base) no Django.

Se você analisar os códigos HTMLs das páginas `principal.html`, `livros.html`, `tccs.html` e `tcc_detalhes.html` você perceberá que tem muitos códigos duplicados. O Django fornece uma maneira de criar um "modelo pai" que você pode incluir em todas as páginas para evitar repetição de código.

Comece criando um template chamado `base.html` dentro da pasta `template`, com o seguinte conteúdo:

```html
{% load static %}

<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="{% static 'mystyles.css' %}"> 
        <title>{% block titulo %}{% endblock %}</title>
    </head>
    <body>
        <div class="topnav">
            <a href="/">PRINCIPAL</a> |
            <a href="/livros">LIVROS</a> |
            <a href="/tccs">TCCs</a> |
            <a href="/dashboard">DASHBOARD</a> |
            <a href="/login">LOGIN</a> |
            <a href="/cadastre-se">CADASTRE-SE</a>
        </div>
        {% block conteudo %}
        {% endblock %}
    </body>
</html>
```

Agora precisamos modificar os templates (páginas) anteriormente criados. Todas as páginas `principal.html`, `livros.html`, `tccs.html` e `tcc_detalhes.html` precisam ser modificadas para extender da página base/mestre nomeada de `base.html`.

Isso é feito incluindo o modelo mestre com a tag `{% extends %}`  e inserindo um bloco `titulo` e um bloco `conteudo`:

Primeiro, modifique a página `principal.html` para o seguinte conteúdo:

```html
{% extends "base.html" %}

{% load static %}

{% block titulo %}
    Portal Biblioteca
{% endblock %}

{% block conteudo %}
    <div class="main">
        <h1>Portal Biblioteca</h1>
        <img src="{% static 'logo-portal.png' %}" alt="logo-portal" width="400" height="300">
    </div>
{% endblock %}
```

Em seguida, modifique a página `livros.html` para o seguinte conteúdo:

```html
{% extends "base.html" %}

{% block titulo %}
    Portal Biblioteca - Livros
{% endblock %}

{% block conteudo %}
    <div class="mycard">
        <h1>Livros</h1>
        <ul>
            {% for l in livros %}
            <li>{{ l.nome }} | {{ l.autor }} | {{ l.ano }} </li>
            {% endfor %}
        </ul>
    </div>
{% endblock %}
```

Em seguida, modifique a página `tccs.html` para o seguinte conteúdo:

```html
{% extends "base.html" %}

{% block titulo %}
    Portal Biblioteca - TCCs
{% endblock %}

{% block conteudo %}
    <div class="mycard">
        <h1>Trabalhos de Conclusão de Curso</h1>
        <ul>
            {% for tcc in tccs %}
            <li onclick="window.location = 'tccs/detalhes/{{ tcc.id }}'"><em>Título:</em> {{ tcc.titulo }} <br> <em>Autor:</em> {{ tcc.autor }} </li>
            {% endfor %}
        </ul>
    </div>
{% endblock %}
```

Em seguida, modifique a página `tcc_detalhes.html` para o seguinte conteúdo:

```html
{% extends "base.html" %}

{% block titulo %}
    Portal Biblioteca - TCCs - Detalhes
{% endblock %}

{% block conteudo %}
    <div class="mycard">
        <h1>Trabalho de Conclusão de Curso</h1>
        <p><em>Título:</em> {{ tcc.titulo }} </p>
        <p><em>Autor:</em> {{ tcc.autor }}</p>
        <p><em>Orientador:</em> {{ tcc.orientador }}</p>
        <p><em>Ano:</em> {{ tcc.ano }}</p>
    </div>

    <p><center>Volte para <a href="/tccs">TCCs</a></center></p>
{% endblock %}
```

### Criando nosso Primeiro Modelo

Até esse momento fizemos a nossa aplicação web com interface, com URLs e algum processamento, mas não trabalhamos com Banco de Dados. Os dados estavam inseridos diretamente no código.

Iremos agora criar o nosso modelo para representar Livros e TCCs no Banco de Dados SQLite disponível no Django. No Django, os dados são criados em objetos, chamados Modelos, e na verdade são tabelas em um banco de dados.

Primeiramente, iremos criar uma classe chamada `Livro`. Para isso abra o arquivo `models.py` na pasta `biblioteca` e digite o seguinte conteúdo:

```python
from django.db import models

class Livro(models.Model):
    nome = models.CharField(max_length=255)
    autor = models.CharField(max_length=255)
    ano = models.IntegerField()
```

O código acima irá criar uma Tabela chamada Livro no BD SQLite. Os campos `nome` e `autor` são campos de texto e estão configurados para ter no máximo 255 caracteres. O campo `ano` é um campo numérico inteiro.

OBS: Quando criamos o projeto Django, obtivemos um banco de dados SQLite vazio. Ele estava na raiz da pasta portal_biblioteca e possui o nome de arquivo db.sqlite3. Por padrão, todos os modelos criados no projeto Django serão criados como tabelas neste banco de dados.

Em seguida, execute o código abaixo para que seja criado a tabela Livro no banco de dados de fato:

```bash
(venv) ... $ python3 manage.py makemigrations biblioteca
```

O que resultará nesta saída:

```bash
Migrations for 'biblioteca':
  biblioteca/migrations/0001_initial.py
    - Create model Livro
```

O Django cria um arquivo descrevendo as alterações e armazena o arquivo na pasta `/biblioteca/migrations/` com nome `0001_initial.py`. Abra esse arquivo para analisar o conteúdo. Observe que o Django insere um campo `id` para suas tabelas, que é um número auto incrementado.

A tabela ainda não foi criada, você terá que executar mais um comando, então o Django criará e executará uma instrução SQL, baseada no conteúdo do novo arquivo da pasta `/biblioteca/migrations/`.

Execute o comando de migração:

```bash
(venv) ... $ python3 manage.py migrate
```

O que resultará nesta saída:

```bash
Operations to perform:
  Apply all migrations: admin, auth, biblioteca, contenttypes, sessions
Running migrations:
  Applying biblioteca.0001_initial... OK
```

Usaremos o interpretador Python (Python Shell) para adicionar alguns livros a tabela criada no BD. Para abrir um shell Python, digite este comando:

```bash
(venv) ... $ python3 manage.py shell
```

O que resultará nesta saída:

```bash
Python 3.10.12 (main, Jun 11 2023, 05:26:28) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
(InteractiveConsole)
>>>
```

Na parte inferior, após os três, `>>>` escreva o seguinte:

```bash
>>> from biblioteca.models import Livro
```

Pressione [enter] e escreva isto para ver a tabela Livro vazia:

```bash
>>> Livro.objects.all()
```

Isso deve fornecer um objeto QuerySet vazio, como este:

```bash
<QuerySet []>
```

Um QuerySet é uma coleção de dados de um banco de dados.

Adicione um registro à tabela, executando estas duas linhas:

```bash
>>> livro = Livro(nome='O Senhor dos Anéis', autor='J.R.R. Tolkien', ano=1954)
>>> livro.save()
```

Execute este comando para ver se a tabela Livro possui um membro:

```bash
Livro.objects.all().values()
```

O que resultará nesta saída:

```bash
<QuerySet [{'id': 1, 'nome': 'O Senhor dos Anéis', 'autor': 'J.R.R. Tolkien', 'ano': 1954}]>
```

Para sair do ambiente shell digite:

```bash
quit()
```

### Ambiente Administrativo do Django

O Django Admin é uma ferramenta ótima do Django, na verdade é uma interface de usuário CRUD (Criar, Ler, Atualizar, Excluir) para todos os seus modelos!

Para entrar na interface do usuário administrativo, inicie o servidor com este comando:

```bash
(venv) ... $ python3 manage.py runserver
```

Na janela do navegador, digite na barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

A razão pela qual esta URL vai para a página de login do administrador do Django pode ser encontrada no arquivo `urls.py` do seu projeto:

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('biblioteca.urls')),
    path('admin/', admin.site.urls),
]
```

A lista `urlpatterns[]` recebe solicitações na rota `admin/` e as envia para `admin.site.urls`, que faz parte de um aplicativo integrado que vem com o Django e contém muitas funcionalidades e interfaces de usuário, sendo uma delas a interface de usuário de login.

### Criando um Usuário no Django

Para poder fazer login no ambiente administrativo do Django, precisamos criar um usuário. Isso é feito digitando este comando:

```bash
(venv) ... $ python3 manage.py createsuperuser
```

O que dará um prompt como esse:

```bash
Username: admin
Email address: 
Password: 
Password (again): 
The password is too similar to the username.
This password is too short. It must contain at least 8 characters.
This password is too common.
Bypass password validation and create user anyway? [y/N]: y
```

**OBS:** Aqui você deve inserir: nome de usuário, endereço de e-mail (você pode simplesmente deixar em branco ou escolher um endereço de e-mail falso) e senha. Em meu caso coloquei usuário `admin` email em branco e senha `admin`.

Minha senha não atendeu aos critérios, mas este é um ambiente de teste, e opto por criar usuário mesmo assim, digitando `y` gerando assim a saída:

```bash
Superuser created successfully.
```

Agora reinicie o servidor:

```bash
(venv) ... $ python3 manage.py runserver
```

Na janela do navegador, digite na barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

Preencha o formulário com o nome de usuário e senha corretos (`admin` e `admin`):

Na tela aberta você pode criar, ler, atualizar e excluir grupos e usuários, mas onde está o modelo de Livro?

O modelo Livro está faltando, como deveria estar. Você tem que informar ao Django quais modelos devem estar visíveis na interface administrativa.

Para incluir o modelo Livro na interface administrativa, temos que dizer ao Django que este modelo deve estar visível na interface administrativa.

Isso é feito em um arquivo chamado `admin.py`, e está localizado na pasta do seu aplicativo, que no nosso caso é a pasta `biblioteca`.

Abra-o, o mesmo deve estar assim:

```python
from django.contrib import admin

# Register your models here.
```

Insira algumas linhas aqui para tornar o modelo Livro visível na página de administração:

```python
from django.contrib import admin
from .models import Livro

admin.site.register(Livro)
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

Clique em Livros e veja o registro de livros que inserimos anteriormente neste tutorial:

Na lista de Livros, vemos "Livro object (1)", "Livro membro (2)" etc., que podem não ser os dados que você deseja que sejam exibidos na lista. Seria melhor exibir "nome" e "autor".

Para mudar isso para um formato mais fácil de ler, temos duas opções:

* Alterar a função de representação de string `__str__()` do modelo de Livro.
* Defina a propriedade `list_details` do modelo de Livro.

Para alterar utilizando a primeira forma, devemos alterar a função de representação de string `__str__()` do modelo de Livro. Para isso faça o seguinte no arquivo `models.py` dentro da pasta `biblioteca`:

```python
from django.db import models

class Livro(models.Model):
    nome = models.CharField(max_length=255)
    autor = models.CharField(max_length=255)
    ano = models.IntegerField()

    def __str__(self):  #definição de função adionada
        return f"{self.nome} - {self.autor}" 
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

Para alterar utilizando a segunda forma (RECOMENDADA), devemos definir a propriedade `list_display` do arquivo `admin.py`. Primeiro crie uma classe `LivroAdmin()` e especifique a tupla `list_display`, assim:

```python
from django.contrib import admin
from .models import Livro

class LivroAdmin(admin.ModelAdmin):
    list_display = ("nome", "autor", "ano")

admin.site.register(Livro, LivroAdmin)
```

*OBS:* Lembre-se de adicionar LivroAdmin como um argumento no arquivo, como em: `admin.site.register(Livro, LivroAdmin)`.

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

### Adicionando novos Livros

Agora podemos criar, atualizar e excluir livros em nosso banco de dados.

Iremos adicionar mais dois livros, clique no botão "ADD LIVRO" no canto superior direito:

Você receberá um formulário vazio onde poderá preencher os campos do livro. Utilize as informações a seguir para preenchimento:

```json
{
    "nome": "1984",
    "autor": "George Orwell",
    "ano": 1949
},
{
    "nome": "Dom Quixote",
    "autor": "Miguel de Cervantes",
    "ano": 1605
}
```

Preencha os campos e clique em `SAVE`:

### Carregando a Interface Livro com Dados do BD

Até aqui vimos como trabalhar com o Banco de Dados, mas a interface da nossa aplicação (livro) ainda não está fazendo a leitura dos dados do BD.

Agora iremos atualizar a interface para puxar/pegar os dados do BD.

Assim, é necessário atualizar o código `views.py` da pasta `biblioteca`. Devemos remover os dados que estavam inseridos estaticamente nesse arquivo.

```python
...
from .models import Livro    # adicione esta importação

...

def livros(request):         # atualize esta função
    livros = Livro.objects.all().values()
    template = loader.get_template('livros.html')
    context = {
        'livros': livros,
    }
    return HttpResponse(template.render(context, request))
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/livros](127.0.0.1:8000/livros)

Repare que os livros listados são somente os livros cadastrados no Banco de Dados.

### Configuração do Projeto Django em Português

No arquivo `settings.py` (na pasta `biblioteca`), pode-se definir o idioma utilizado pela aplicação django como sendo o português:

```python
LANGUAGE_CODE = 'pt-BR'
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

### Carregando a Interface TCC com Dados do BD

Até aqui criamos apenas uma Tabela no BD que é Livro. Agora iremos criar uma Tabela TCC no Modelo do BD.

Primeiramente, iremos criar uma classe chamada `TCC`. Para isso abra o arquivo `models.py` na pasta `biblioteca` e digite o seguinte conteúdo:

```python
from django.db import models

class Livro(models.Model):
    nome = models.CharField(max_length=255)
    autor = models.CharField(max_length=255)
    ano = models.IntegerField()

    def __str__(self):
        return f"{self.nome} - {self.autor}"

class TCC(models.Model):    # classe adiconada
    titulo = models.CharField(max_length=255)
    autor = models.CharField(max_length=255)
    orientador = models.CharField(max_length=255)
    ano = models.IntegerField()

    def __str__(self):
        return f"{self.titulo} - {self.autor}"
```

O código acima irá criar uma Tabela chamada TCC no BD SQLite.

Em seguida, execute o código abaixo para que seja criado a tabela TCC no banco de dados de fato:

```bash
(venv) ... $ python3 manage.py makemigrations biblioteca
```

O que resultará nesta saída:

```bash
Migrations for 'biblioteca':
  biblioteca/migrations/0002_tcc.py
    - Create model TCC
```

A tabela ainda não foi criada, execute o comando de migração para que a tabela seja de fato criada:

```bash
(venv) ... $ python3 manage.py migrate
```

O que resultará nesta saída:

```bash
Operations to perform:
  Apply all migrations: admin, auth, biblioteca, contenttypes, sessions
Running migrations:
  Applying biblioteca.0002_tcc... OK
```

Agora iremos informar ao Django quais modelos devem estar visíveis na interface administrativa. Para incluir o modelo TCC na interface administrativa, temos que dizer ao Django que este modelo deve estar visível na interface administrativa.

Isso é feito em um arquivo chamado `admin.py`, e está localizado na pasta do seu aplicativo, que no nosso caso é a pasta `biblioteca`. Digite o seguinte código:

```python
from django.contrib import admin
from .models import Livro
from .models import TCC

class LivroAdmin(admin.ModelAdmin):
    list_display = ("nome", "autor", "ano")

class TCCAdmin(admin.ModelAdmin):
    list_display = ("titulo", "autor", "orientador", "ano")

admin.site.register(Livro, LivroAdmin)
admin.site.register(TCC, TCCAdmin)
```

Agora reinicie o servidor:

```bash
(venv) ... $ python3 manage.py runserver
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/admin/](127.0.0.1:8000/admin/)

Agora podemos criar, atualizar e excluir TCCs em nosso banco de dados.

Iremos adicionar mais três TCCs, clique no botão "ADICIONAR TCC" no canto superior direito:

Você receberá um formulário vazio onde poderá preencher os campos do TCC. Utilize as informações a seguir para preenchimento:

```json
{
    "titulo": "Sistemas de Recomendação Personalizados",
    "autor": "Maria Silva",
    "orientador": "Prof. João Santos",
    "ano": 2021
},
{
    "titulo": "Segurança de Redes em Ambientes Corporativos",
    "autor": "Pedro Oliveira",
    "orientador": "Profa. Ana Rodrigues",
    "ano": 2020
},
{
    "titulo": "Inteligência Artificial Aplicada à Análise de Dados",
    "autor": "Luana Costa",
    "orientador": "Prof. André Martins",
    "ano": 2019
}
```

Preencha os campos e clique em `SAVE`:

Agora iremos atualizar a interface do TCC para puxar/pegar os dados do BD.

Assim, é necessário atualizar o código `views.py` da pasta `biblioteca`.

```python
...
from .models import TCC    # adicione esta importação

...

def tccs(request):         # atualize esta função
    tccs = TCC.objects.all().values()
    template = loader.get_template('tccs.html')
    context = {
        'tccs': tccs,
    }
    return HttpResponse(template.render(context, request))
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/tccs](127.0.0.1:8000/tccs)

Repare que os TCCs listados são somente os TCCs cadastrados no Banco de Dados.

Ainda no código `views.py` da pasta `biblioteca` atualize a função `tcc_detalhes` para que a mesma pegue os dados também do banco de dados baseado no `id`.

```python
...
def tcc_detalhes(request, id):
    tcc = TCC.objects.get(id=id)
    template = loader.get_template('tcc_detalhes.html')
    context = {
        'tcc': tcc,
    }
    return HttpResponse(template.render(context, request))
```

### Incluindo código JavaScript no Projeto

Até o presente momento não temos código javascript no nosso projeto. A fim de ilustração iremos fazer uma pequena tela de dashboard em nosso projeto com gráficos em JavaScript.

Assim, na pasta `templates` crie um arquivo chamado `dashboard.html`. Nesse arquivo coloque o seguinte conteúdo:

```html
{% extends "base.html" %}

{% block titulo %}
    Portal Biblioteca - Dashboard
{% endblock %}

{% block conteudo %}
    <div class="mycard">
        <h1>Dashboard</h1>
        <div>
            <canvas id="graficoNumVolumes"></canvas>
        </div>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        const ctx = document.getElementById('graficoNumVolumes');

        new Chart(ctx, {
            type: 'bar',
            data: {
            labels: ['Livros', 'TCCs', 'Dissertações', 'Teses', 'Apostilas', 'Jornais'],
            datasets: [{
                label: 'Número de Volumes',
                data: [12, 19, 8, 5, 2, 10],
                borderWidth: 1
            }]
            },
            options: {
            scales: {
                y: {
                    beginAtZero: true
                }
            }
            }
        });
    </script>
{% endblock %}
```

Agora, precisamos atualizar o arquivo de `urls.py` na pasta `biblioteca`. No arquivo adicione a linha destacada:

```python
...

urlpatterns = [
    ...
    path('dashboard', views.dashboard, name='dashboard'), # adicione esta linha
]
```

Agora, precisamos atualizar o arquivo de `views.py` nas pasta `biblioteca`. Adicione a função abaixo nesse arquivo.

```python
...

def dashboard(request): # adicione essa função
    template = loader.get_template('dashboard.html')
    return HttpResponse(template.render())
```

Agora reinicie o servidor:

```bash
(venv) ... $ python3 manage.py runserver
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/dashboard](127.0.0.1:8000/dashboard)

Analise a página de dashboard construída.

Agora, iremos modularizar o nosso código melhor.

Assim, na pasta `staticfiles` crie um arquivo chamado `myscripts.js`. Coloque nesse arquivo o seguinte conteúdo:

```javascript
function graficoBarras() {
    const ctx = document.getElementById('graficoNumVolumes');

    new Chart(ctx, {
        type: 'bar',
        data: {
        labels: ['Livros', 'TCCs', 'Dissertações', 'Teses', 'Apostilas', 'Jornais'],
        datasets: [{
            label: 'Número de Volumes',
            data: [12, 19, 8, 5, 2, 10],
            borderWidth: 1
        }]
        },
        options: {
        scales: {
            y: {
                beginAtZero: true
            }
        }
        }
    });
}

graficoBarras()
```

Agora, precisamos atualizar o código do `dashboard.html` da pasta `templates`. O conteúdo desse arquivo deve ficar assim:

```html
{% extends "base.html" %}

{% load static %}

{% block titulo %}
    Portal Biblioteca - Dashboard
{% endblock %}

{% block conteudo %}
    <div class="mycard">
        <h1>Dashboard</h1>
        <div>
            <canvas id="graficoNumVolumes"></canvas>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="{% static 'myscripts.js' %}"></script>
{% endblock %}
```

Em seguida, execute o seguinte comando abaixo:

```bash
(venv) ... $ python3 manage.py collectstatic
```

Agora reinicie o servidor:

```bash
(venv) ... $ python3 manage.py runserver
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/dashboard](127.0.0.1:8000/dashboard)

Analise a página de dashboard construída.

Agora, iremos colocar um gráfico de pizza também no nosso dashboard. Assim, na pasta `staticfiles` atualize o arquivo `myscripts.js` com o seguinte conteúdo:

```javascript
function graficoBarras() {
    const ctx = document.getElementById('graficoNumVolumes');

    new Chart(ctx, {
        type: 'bar',
        data: {
        labels: ['Livros', 'TCCs', 'Dissertações', 'Teses', 'Apostilas', 'Jornais'],
        datasets: [{
            label: 'Número de Volumes',
            data: [12, 19, 8, 5, 2, 10],
            borderWidth: 1
        }]
        },
        options: {
        scales: {
            y: {
                beginAtZero: true
            }
        }
        }
    });
}

function graficoPizza(){
    const ctx = document.getElementById('graficoPizza');

    new Chart(ctx, {
        type: 'pie',
        data: {
        labels: ['Livros', 'TCCs', 'Dissertações', 'Teses', 'Apostilas', 'Jornais'],
        datasets: [{
            label: 'Número de Volumes',
            data: [12, 19, 8, 5, 2, 10],
            backgroundColor: [
                'rgb(255, 99, 132)',
                'rgb(54, 162, 235)',
                'rgb(255, 205, 86)',
                'rgb(80, 60, 200)',
                'rgb(255, 100, 86)',
                'rgb(54, 255, 150)'
            ],
            hoverOffset: 8
        }]
        }
    });
}

graficoBarras()

graficoPizza()
```

Agora, atualize o arquivo de `dashboard.html` na pasta `templates`.

```html
{% extends "base.html" %}

{% load static %}

{% block titulo %}
    Portal Biblioteca - Dashboard
{% endblock %}

{% block conteudo %}
    <div class="mycard">
        <h1>Dashboard</h1>
        <div>
            <canvas id="graficoNumVolumes"></canvas>
        </div>
        <br>
        <br>
        <div>
            <canvas id="graficoPizza"></canvas>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="{% static 'myscripts.js' %}"></script>
{% endblock %}
```

Em seguida, execute o seguinte comando abaixo:

```bash
(venv) ... $ python3 manage.py collectstatic
```

Agora reinicie o servidor:

```bash
(venv) ... $ python3 manage.py runserver
```

Agora volte para o navegador e atualize a barra de endereço [127.0.0.1:8000/dashboard](127.0.0.1:8000/dashboard)

Analise a página de dashboard construída.

Para mais informações sobre gráficos em javacript consulte a documentação da biblioteca [chart.js](https://www.chartjs.org/).

### Adicionando Aplicação de Controle de Usuários no Django

O Django possui já prontos diversos recursos para trabalhar com autenticação de usuários e controle de nível de acesso.

Agora, iremos adicionar em nosso projeto um sistema de gestão de usuários. Para criarmos na sequência as telas de login e cadastro na plataforma.

Para isso iremos criar uma outra aplicação/aplicativo web dentro do nosso projeto. Assim, digite o seguinte conteúdo.

```bash
(venv) ... $ python3 manage.py startapp usuarios
```

Agora, atualize a lista `INSTALLED_APPS` em `settings.py` na pasta `biblioteca`:

```python
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'biblioteca',
    'usuarios', #adicone seu app aqui 
]
...
```

Agora, crie na pasta `usuarios` um arquivo chamado `urls.py` com o seguinte conteúdo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('login', views.login, name='login'),
    path('cadastro', views.cadastro, name='cadastro'),
]
```

Agora, precisamos informar a nossa aplicação principal da existência dessas novas URLs. Assim, edite o código `urls.py` da pasta `porta_biblioteca` da seguinte forma:

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('biblioteca.urls')),
    path('', include('usuarios.urls')),  #adicione essa linha aqui
    path('admin/', admin.site.urls),
]
```

Agora, precisamos definir as views do nosso sistema de login e cadastro. Assim, digite o código abaixo:

```python
from django.http import HttpResponse
from django.template import loader

def login(request):
    template = loader.get_template('login.html')
    return HttpResponse(template.render())

def cadastro(request):
    template = loader.get_template('cadastro.html')
    return HttpResponse(template.render())
```

### Algumas Informações Adicionais

Caso queira ver o que foi feito no BD, basta digitar o comando abaixo com o número da migração:

```bash
(venv) ... $ python3 manage.py sqlmigrate biblioteca 0001
```

**Obs:** no comando acima `biblioteca` representa o nome da nossa aplicação web e o número 0001 é o número da migração.

A saída desse comando é algo parecido com:

```sql
BEGIN;
--
-- Create model Livro
--
CREATE TABLE "biblioteca_livro" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "nome" varchar(255) NOT NULL, "autor" varchar(255) NOT NULL, "ano" integer NOT NULL);
COMMIT;
```

Para vermos com detalhes o conteúdo do BD podemos utilizar a ferramenta [DB Browser for SQLite](https://sqlitebrowser.org/). Assim, basta abrir o arquivo do BD chamado `db.sqlite3` que está na raiz do projeto.

### Comandos Não Utilizados

Instale a biblioteca Pillow que dá suporte ao processamento de imagens no ambiente virtual criado:

```bash
(venv) ... $ pip3 install Pillow
```
