# Django Contexto Global

**`context_processors`**é uma lista de caminhos Python pontilhados para callables que são usados para preencher o contexto quando um modelo é renderizado com uma solicitação. Esses callables pegam um objeto de solicitação como argumento e retornam um **`[dict](https://docs.python.org/3/library/stdtypes.html#dict)`**dos itens a serem mesclados no contexto.

exemplo: 

```python
def context_mytext(request):
    return {'mytext': 'Exibir este contexto em qualquer lugar do meu site!'}
```

### Configuração

Criar arquivo context_processors.py. Pode ser em qualquer app.

Nesse caso vou criar no projeto core.

***core/context_processors.py*** 

```python
def context_mytext(request):
    return {'mytext': 'Exibir este contexto em qualquer lugar do meu site!'}
```

***core/settings.py***

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
                # Apps
                'core.context_processors.context_mytext', 
            ],
        },
    },
]
```

Feito isso, em qualquer lugar do seu template pode chamar o context.

```html
{% extends 'base.html' %}

{% block title %}Pagina 1{% endblock %}

{% block content %}
	<h1>Pagina 1</h1>

	<p>Testando o context Global</p>
	<p>{{mytext}}</p>
	
	<!-- Resposta -->
	<!-- <p>Exibir este contexto em qualquer lugar do meu site!</p> -->
	
{% endblock %}
```

