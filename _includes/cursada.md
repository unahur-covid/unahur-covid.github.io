{% assign clases = cursada | sort %}
{% for clase_hash in clases reversed %}
{% assign numero_clase = clase_hash[0] | plus:0 %}
{% assign clase = clase_hash[1] %}

## [Semana {{numero_clase}} - {{ clase.titulo }}](#clase-{{numero_clase}}){: .titulo-clase}
{{clase.descripcion}}

{% if clase.borrador %}

### EN CONSTRUCCIÓN. Puede que no ande nada de lo que está abajo.

{% endif %}

{% if clase.videos %}

### Videos
{% for video in clase.videos %}
* [{{video.nombre}}]({{video.url}}). {{video.descripcion}}
{% endfor %}

{% endif %}

{% if clase.entrega %}

### Ejercicios obligatorios
{% assign fecha = clase.entrega.fecha %}
La fecha límite para la entrega de esta semana es el <strong>{% include fecha-formato-humano.md fecha=fecha %}</strong>.

{% assign ejercicios = clase.entrega.ejercicios %}
{% if ejercicios %}
{% include ejercicios-github.html ejercicios=ejercicios %}
{% endif %}

{% assign guias = clase.entrega.mumuki %}
{% if guias %}
**Mumuki**
{% include ejercicios-mumuki.md guias=guias %}
{% endif %}

{{clase.entrega.descripcion}}

{% endif %}

{% if clase.ejercicios %}

### Actividades complementarias
{% assign ejercicios = clase.ejercicios %}
{% include ejercicios-github.html ejercicios=ejercicios %}

{% if clase.textoEjercicios %}
{{clase.textoEjercicios}}
{% endif %}

{% endif %}

{% if clase.mumuki %}

### Mumuki

Te recomendamos resolver las guías:
{% assign guias = clase.mumuki %}
{% include ejercicios-mumuki.md guias=guias %}

{% endif %}

{% if forloop.last == false %}
<hr class="titulo-clase">
{% endif %}

{% endfor %}
