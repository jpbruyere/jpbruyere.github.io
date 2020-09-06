---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

{% for post in site.posts %}
<div class="post-list">
    <table style="width:100%">
        <tr>
            <td class="date">{{ post.date | date_to_long_string}}</td>
            <td class="title"><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></td>
        </tr>
        <!--<tr>
            <td/>
            <td class="excerpt">
                {{ post.excerpt}}
            </td>
        </tr>-->
        <tr>
            <td/>
            <td>
                {% for tag in post.tags %}
                    <span class="tag">{{ tag }}</span>
                {% endfor %}            
            </td>
        </tr>
    </table>

</div>
{% endfor %}