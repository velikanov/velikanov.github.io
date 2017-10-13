{{ site.data.series[post.series].title }} series:
{% for relatedPost in site.posts reversed %}
    {% if relatedPost.series == post.series %}
        {% if relatedPost != post %}
            <div><a href="{{ relatedPost.url | relative_url }}">{{ relatedPost.subtitle }}</a></div>
        {% else %}
            <div>{{ relatedPost.subtitle }}</div>
        {% endif %}
    {% endif %}
{% endfor %}