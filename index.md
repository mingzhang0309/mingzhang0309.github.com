---
layout: home
---

<div class="index-content blog">
    <div class="section">
    	<ul class="artical-cate">
            <li class="on"><a href="/"><span>Blog</span></a></li>
            <li style="text-align:center"><a href="/opinion"><span>Opinion</span></a></li>
            <li style="text-align:right"><a href="/project"><span>Project</span></a></li>
        </ul>

        <div class="cate-bar"><span id="cateBar"></span></div>

        <ul class="artical-list">
        {% for post in site.categories.blog %}
            <li>
                <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
                <div class="title-desc">{{ post.description }}</div>
            </li>
        {% endfor %}
        </ul>

	<!-- 分页
        
	<div id="post-pagination" class="pagination">
            {% if paginator.previous_page %}
                <p class="previous">
      		{% if paginator.previous_page == 1 %}
        	<a href="/">Previous</a>
      		{% else %}
        	<a href="{{ paginator.previous_page_path }}">Previous</a>
      		{% endif %}
    		</p>
  	    {% else %}
    		<p class="previous disabled">
      		<span>Previous</span>
    		</p>
  	    {% endif %}

  	    <ul class="pages">
    		<li class="page">
      		{% if paginator.page == 1 %}
        	    <span class="current-page">1</span>
     		{% else %}
        	    <a href="/">1</a>
      		{% endif %}
    		</li>

    		{% for count in (2..paginator.total_pages) %}
		    <p>{{ count }} ++++++++</p>
      		    <li class="page">
                	{% if count == paginator.page %}
          		<span class="current-page">{{ count }}</span>
        		{% else %}
          		<a href="/page{{ count }}">{{ count }}</a>
        		{% endif %}
      		    </li>
    		{% endfor %}
  	    </ul>

            {% if paginator.next_page %}
    		<p class="next">
      		<a href="{{ paginator.next_page_path }}">Next</a>
    		</p>
  	    {% else %}
                <p class="next disabled">
      		<span>Next</span>
    		</p>
  	    {% endif %}
	</div>
        -->

    </div>
    

    <div class="aside">
    </div>
</div>

