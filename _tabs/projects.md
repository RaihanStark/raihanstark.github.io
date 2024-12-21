---
# the default layout is 'page'
icon: fas fa-briefcase
order: 1
type: project-list
---

<div id="post-list" class="flex-grow-1 px-xl-1">
  <div class="row row-cols-1 row-cols-md-2 g-4">
    {% for post in site.projects %}
    <div class="col">
            <a href="{{ post.url | relative_url }}" class="text-decoration-none h-100">
    <article class="card-wrapper card h-100">
      {% assign card_body_col = '12' %}
      {% if post.image %}
        {% assign card_body_col = '12' %}
      {% endif %}

      <div class="post-preview row g-0 flex-md-row-reverse h-100">
        {% if post.image %}
          {% assign src = post.image.path | default: post.image %}
          {% unless src contains '//' %}
            {% assign src = post.media_subpath | append: '/' | append: src | replace: '//', '/' %}
          {% endunless %}

          {% assign alt = post.image.alt | xml_escape | default: 'Preview Image' %}

          {% assign lqip = null %}
          {% if post.image.lqip %}
            {% capture lqip %}lqip="{{ post.image.lqip }}"{% endcapture %}
          {% endif %}

          <div class="col-md-12">
              <img src="{{ src }}" alt="{{ alt }}" style="object-fit: cover;object-position: top;border-radius: 10px;" {{ lqip }}>
          </div>
        {% endif %}

        <div class="col-md-{{ card_body_col }}">
          <div class="card-body d-flex flex-column">
              <h1 class="card-title my-2 mt-md-0">{{ post.title }}</h1>

              <div class="card-text content mt-0 mb-3">
                <p>{% include post-description.html %}</p>
              </div>

              <div class="post-meta flex-grow-1 d-flex align-items-end">
                <div class="me-auto">
                  <!-- posted date -->
                  <i class="far fa-calendar fa-fw me-1"></i>
                  {% include datetime.html format="%Y" date=post.date lang=lang %}

                  <!-- categories -->
                  {% if post.categories.size > 0 %}
                    <i class="far fa-folder-open fa-fw me-1"></i>
                    <span class="categories">
                      {% for category in post.categories %}
                        {{ category }}
                        {%- unless forloop.last -%},{%- endunless -%}
                      {% endfor %}
                    </span>
                  {% endif %}
                </div>

                {% if post.pin %}
                  <div class="pin ms-1">
                    <i class="fas fa-thumbtack fa-fw"></i>
                    <span>{{ site.data.locales[lang].post.pin_prompt }}</span>
                  </div>
                {% endif %}
              </div>
              <!-- .post-meta -->
          </div>
          <!-- .card-body -->
        </div>
      </div>
    </article>
    </a>
    </div>
    {% endfor %}

  </div>
</div>
