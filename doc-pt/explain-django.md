- [voltar](https://github.com/0joseDark/modules/blob/main/README.md)
### O que é Django?
**Django** é um framework de alto nível para desenvolvimento web em Python. Ele ajuda os programadores a criar aplicações web de forma rápida, escalável e segura. Foi criado com o objetivo de tornar o processo de desenvolvimento mais eficiente, fornecendo ferramentas prontas para tarefas comuns em aplicações web, como:

- Gestão de utilizadores e autenticação.
- Ligações a bases de dados.
- Criação de interfaces administrativas.
- Manipulação de rotas (URLs) e templates (HTML dinâmico).
- Suporte a APIs REST (com Django REST Framework, se necessário).

O Django segue a arquitetura **Model-View-Template (MVT)**, que organiza o código em três componentes principais:

1. **Model (Modelo)**: Representa os dados e a lógica de negócios (estrutura da base de dados).
2. **View (Vista)**: Contém a lógica que conecta os modelos aos templates.
3. **Template (Modelo de Apresentação)**: Define como os dados serão apresentados ao utilizador (HTML dinâmico).

---

### Porquê usar o Django?

1. **Rápido**: Permite desenvolver aplicações rapidamente, com ferramentas que automatizam muitas tarefas.
2. **Seguro**: Inclui proteção contra ataques comuns, como injeção de SQL e falsificação de pedidos (CSRF).
3. **Escalável**: Projetado para crescer com as aplicações, suportando grandes volumes de tráfego.
4. **Versátil**: Pode ser usado para criar desde blogs simples até plataformas complexas, como redes sociais ou APIs REST.

---

### Como instalar e configurar o Django?

#### 1. **Pré-requisitos**

- **Python** instalado no sistema.  
  Verifica a instalação:
  ```bash
  python --version
  ```

#### 2. **Instalar o Django**

1. Cria um ambiente virtual para o projeto:
   ```bash
   python -m venv venv
   ```

2. Ativa o ambiente virtual:
   ```bash
   venv\Scripts\activate
   ```

3. Instala o Django:
   ```bash
   pip install django
   ```

4. Verifica a instalação:
   ```bash
   django-admin --version
   ```

---

### Criar um projeto Django

1. Cria um novo projeto:
   ```bash
   django-admin startproject nome_do_projeto
   ```
   Este comando cria uma estrutura inicial com:
   - `manage.py`: Script para gerir o projeto.
   - Uma pasta com o mesmo nome do projeto, contendo ficheiros de configuração (`settings.py`, `urls.py`, etc.).

2. Navega até a pasta do projeto:
   ```bash
   cd nome_do_projeto
   ```

3. Inicia o servidor de desenvolvimento:
   ```bash
   python manage.py runserver
   ```
   No navegador, acede a `http://127.0.0.1:8000/`. Deverás ver a página inicial do Django.

---

### Estrutura de um projeto Django

Após criar um projeto, a estrutura será semelhante a esta:

```
nome_do_projeto/
│
├── manage.py               # Gerir o projeto
├── nome_do_projeto/
│   ├── __init__.py         # Marca como módulo Python
│   ├── settings.py         # Configurações do projeto
│   ├── urls.py             # Rotas do projeto
│   ├── asgi.py             # Configuração para servidores ASGI
│   └── wsgi.py             # Configuração para servidores WSGI
```

---

### Criar uma aplicação Django

Uma aplicação no Django é um componente modular que pode ser reutilizado em diferentes projetos.

1. Cria uma aplicação:
   ```bash
   python manage.py startapp blog
   ```
   A estrutura será criada dentro de `blog/`:
   ```
   blog/
   ├── migrations/         # Histórico de alterações na base de dados
   ├── __init__.py         # Marca como módulo Python
   ├── admin.py            # Regista modelos na interface administrativa
   ├── apps.py             # Configuração da aplicação
   ├── models.py           # Define os modelos (tabelas)
   ├── tests.py            # Testes automatizados
   ├── views.py            # Controladores (lógica da aplicação)
   ```

2. Adiciona a aplicação no ficheiro `settings.py`:
   ```python
   INSTALLED_APPS = [
       ...,
       'blog',
   ]
   ```

---

### Exemplo prático: Criar um blog simples

#### 1. Criar um modelo para os posts

Define a estrutura da base de dados em `blog/models.py`:
```python
from django.db import models

class Post(models.Model):
    titulo = models.CharField(max_length=100)
    conteudo = models.TextField()
    data_criacao = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.titulo
```

#### 2. Criar a base de dados

Gera e aplica as migrações:
```bash
python manage.py makemigrations
python manage.py migrate
```

#### 3. Criar uma vista para listar posts

Em `blog/views.py`:
```python
from django.shortcuts import render
from .models import Post

def lista_posts(request):
    posts = Post.objects.all()
    return render(request, 'blog/lista_posts.html', {'posts': posts})
```

#### 4. Configurar as rotas

Adiciona a URL da aplicação em `blog/urls.py`:
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.lista_posts, name='lista_posts'),
]
```

Inclui a aplicação no ficheiro principal de URLs (`urls.py`):
```python
from django.urls import include, path

urlpatterns = [
    path('blog/', include('blog.urls')),
]
```

#### 5. Criar um template HTML

Em `blog/templates/blog/lista_posts.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Lista de Posts</title>
</head>
<body>
    <h1>Posts</h1>
    <ul>
        {% for post in posts %}
            <li>{{ post.titulo }} - {{ post.data_criacao }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

#### 6. Executar o servidor

Inicia o servidor:
```bash
python manage.py runserver
```
Acede a `http://127.0.0.1:8000/blog/` para ver a lista de posts.

---

### O que aprendemos?

- Instalar e configurar o Django.
- Criar um projeto e uma aplicação.
- Definir um modelo de dados.
- Criar vistas e rotas.
- Utilizar templates para exibir dados.

O Django oferece muitos outros recursos, como autenticação, APIs REST, cache, e-mail, entre outros.
