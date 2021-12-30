---
layout: post
title: Publication Feed
subtitle: Adding a second independent feed to Jekyll
cover-img: /assets/img/banner_001.jpg
tags: [blog]
---


This article is dedicated to all the self-made bloggers and wanna-bees out there looking for a somewhat modern-looking layout and easy-to-use and adaptive blogging setup.
If you just like to start writing without many stones in your way build your blog with [Jekyll](https://jekyllrb.com) and [GitHubPages](https://docs.github.com/en/pages).
Its free, open-source, works right out of the box and is straightforward to adapt as will be shown in this article.
A valuable starting point I stumbled across is [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll).
Indeed as the name anticipates a beautiful template using [Jekyll](https://jekyllrb.com).
[Jekyll](https://jekyllrb.com) is a static site generator, which takes in plain
[Markdown](https://www.markdownguide.org) and spits out a static website
ready to be read.
It's coded in [Ruby](https://www.ruby-lang.org) and thus comes as a *gem*, which
is how the [Ruby](https://www.ruby-lang.org)-Community terms their packages.
All required packages or *gems* of an application are collected in a *gemfile*.
These dependencies are managed by the [bundler](https://rubygems.org/gems/bundler).
This enables the straightforward local deployment by just hitting `bundle exec jekyll serve`.
Feel free to use my forked and modified [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll)
as a template for your endeavors. This, however, does not apply to the articles published here, which is self-explanatory, I reckon.

If you are a scientific writer and researcher as I am, then one significant
feature missing in the vanilla blog design is a publication feed that will hold all your scientific papers and journals.
In this article, we go through the steps required to add a publication page and feed to the [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll) template.
Hit the publication tag in the top bar above and gasp the result of the journey described here.

<!-- Well, to start this with a frank statement, I have to confess that my web dev
skills are on a more or less nooby level. Nonetheless,
This article is dedicated to all the gears keeping this website up and running. -->
<!-- One of my early attempts to build a dynamic website was based on
[Flask](https://flask.palletsprojects.com) as a lightweight Python web framework.
Hosting was done via [PythonAnywhere](https://www.pythonanywhere.com).
This hosting platform provides a full Python environment and you do not have
to bother about setting up your own web server. However, the free
account limits the creativity to a few MB storage this is no long-term option
when you are looking for a solution without any financial investments. -->


## Define publication items
[Jekyll](https://jekyllrb.com) has a static folder [structure](https://jekyllrb.com/docs/structure).
For a publication feed, we can adapt the implementation of post feeds. Posts are stored in the `_posts` folder.
The prefix `_` is a [Jekyll](https://jekyllrb.com) indicator and links to variables, which can be used later on.
We can create a `_pubs` folder and dump in all publications as explicit property files.
Like articles in the `_posts` directory, each file in `_pubs` has to follow a certain naming convention (permalink): the concatenation of the date and some title, like `2021-06-15-some-fancy-title.md`.
The title is only necessary to avoid naming conflicts if you are eagerly writing more than one article per day.
[Jekyll](https://jekyllrb.com) will parse this and directly extract the release date of your publication.
This becomes handy if you would like to have your publication sorted by the reverse date (newest first). More on this later.

Let us dive into the content of a possible property file in `_pubs`. Each file represents a single publication.
I called them deliberately property files since they should just hold things like the title, authors, conference, and a URL to link to the proceeding page for people to read your paper.
This is different from articles in `_posts`, which hold the entire content of the article. So, here is the content of an example publication property file:
```
---
layout: none
title: 'Attention: I did nothing and suddenly my experiments work.'
abstract: 'I do not know myself what I am publishing here.'
author:
  - Johann Schmidt
  - Somebody Else
conference: 'ABC'
link: 'johschm.github.io/blog'
tags: [Awesomeness]
---
```
We define and assign value to seven variables, which we utilize later.
All of those should be quite self-explanatory, perhaps except the `layout`.
Setting the `layout` to `none` does not mean the design is running wild.
The `layout` variable specifies the parent design this object is inheriting from. We do not need this and define it on your own.

## Bringing in some CSS flavor
The layout will be specified in the `beautifuljekyll.css` in `assets/css`.
The publication items will be rendered based on what we specify here.
Let us create a visually appealing feed by adding in some straightforward CSS blocks.

Each item (publication) in the feed comprises a title and an abstract, as well as some meta information, like the authors, the publication date, and the conference. The entire item should link to the paper for interested readers. Lets start chronologically with the title of the item.
{% raw %} ```
.pub-title {
  font-family: 'Roboto';
  font-weight: 500;
  line-height: 1.0;
  font-size: 1rem;
  text-align: justify;
  color: {{ site.text-col | default: "#404040" }};
}
``` {% endraw %}
Note that, we use some [Liquid](https://shopify.github.io/liquid) logic here, where the [Liquid](https://shopify.github.io/liquid) syntax demands this double-curly-bracket wrapping.
We use this for querying the specified text color (see `_config.yml`) to ensure consistency among all texts. This is a powerful tool for you as a developer to straightforwardly implement modifications to the global text color and other properties.
But back to the CSS snippet above.
This will render the title a bit thicker via the increased `font-weight`.
The abstract on the other hand should be a bit thinner.
{% raw %} ```
.pub-abstract {
  font-family: 'Roboto';
  font-weight: 400;
  font-size: 1rem;
  text-align: justify;
  color: {{ site.text-col | default: "#404040" }};
}
``` {% endraw %}
In between, we would like to render the aforementioned metadata.
```
.pub-preview .pub-meta,
.pub-heading .pub-meta {
  color: #808080;
  font-size: 1rem;
  font-style: italic;
  margin: 0 0 0.1rem;
  font-family: 'Roboto';
}
```
Remember that the entire item is a link to the paper *per se*.
For a more professional looking appearance we overwrite the standard blue color-code of references and allow the highlighting only when hovered over.
{% raw %} ```
.pub-preview a {
  text-decoration: none;
  font-family: 'Roboto';
  color: {{ site.text-col | default: "#404040" }};
}

.pub-preview a:focus,
.pub-preview a:hover {
  text-decoration: none;
  color: {{ site.hover-col | default: "#0085A1" }};
}
``` {% endraw %}
Finally, we come to the design of the feed holding together all items.
For better readability items are separated by a thin line (`border-bottom`).
```
.pub-preview {
  padding: 1.25rem 0;
  border-bottom: 1px solid #eee;
  overflow: hidden;
}
```
However, this is useless for the last entry of the feed and can be removed.
```
.pub-preview:last-child {
  border-bottom: 0;
}
```
Now, with this just beautiful layout and the publication file dump at hand, we can go ahead and chain them together by some [Jekyll](https://jekyllrb.com) and HMTL logic.

## Get the gears turning
In the following, we implement the logical glue, which iterates over all property files in `_pubs`, reads them in, and renders them using the above-specified layout.
One ingredient of this glue is a new HTML layout file in the `_layout` directory, which we call `pub_feed.html`.
Ready to be thrown into cold waters first? Here is the content of this layout file and thus the publication feed logic:
{% raw %} ```
---
layout: page
---

{{ content }}

<div>
  {% assign pubs = site.pubs | sort: 'date' | reverse %}
  {% for pub in pubs %}
  <article class="pub-preview">

    <a href="{{ pub.link }}">
      <h2 class="pub-title">{{ pub.title }}</h2>

      <p class="pub-meta">
        {% for name in pub.author %}
        {% if name == site.author %}
        <b>{{ name }}</b>
        {% else %}
        {{ name }}
        {% endif %}
        &nbsp;
        {% endfor %}
      </p>

      <p class="pub-meta">
        {% assign date_format = site.date_format_pubs | default: "%B, %Y" %}
        Published on {{ pub.date | date: date_format }}
        in {{ pub.conference }}
      </p>

      {% if pub.abstract %}
        <h3 class="pub-abstract">
        {{ pub.abstract }}
        </h3>
      {% endif %}
    </a>

   </article>
  {% endfor %}
</div>
``` {% endraw %}
Alight, you can skip the next few paragraphs if everything is clear.
For all others, lets dive into the details by deciphering this snippet above.
This layout inherits from the `page` layout, which particularize the generic appearance of all blog pages.
All the generic content like header and footer are comprised in the {% raw %}`{{ content }}`{% endraw %} [Liquid](https://shopify.github.io/liquid) variable. Afterwards, things are getting more interesting by adding some individual spice to the dish.
{% raw %} ```
<div>
  {% assign pubs = site.pubs | sort: 'date' | reverse %}
  {% for pub in pubs %}
  <article class="pub-preview">
    ...
  </article>
  {% endfor %}
</div>
``` {% endraw %}
This iterates over all publications, which are sorted by their release dates (newest first by piping to `reverse`).
Originally, the publications are stored in the `site.pubs` variable.
For now, assume this as given, we will pick up on that later.
Each publication is then wrapped in the `pub-preview` class, which will add some padding and the separation line below as discussed in the previous section.
Each item is linked to the paper proceeding via {% raw %}`<a href="{{ pub.link }}">`{% endraw %}, where {% raw %}`pub.link`{% endraw %} stems from the property file of the publication.

<!-- {% raw %}```
<h2 class="pub-title">{{ pub.title | strip_html }}</h2>
```{% endraw %}
The liquid filter `strip_html` removes any HTML tags from the title string. -->

After rendering the title by employing the `pub.title` string, the meta data is displayed.
Often the own name is highlighted when providing the list of authors of a paper.
This can be trivially implemented by utilizing some basic [Liquid](https://shopify.github.io/liquid) logic
{% raw %}```
<p class="pub-meta">
  {% for name in pub.author %}
  {% if name == site.author %}
  <b>{{ name }}</b>
  {% else %}
  {{ name }}
  {% endif %}
  &nbsp;
  {% endfor %}
</p>
```{% endraw %}
We loop over all involved authors specified in the property file of the publication. Each name string is checked against the global variable `site.author`, which contains the authors' name of the website.
The name is rendered bold *iff* this is true.
For the sake of simplicity, names are visually separated by spaces `&nbsp;` since this does not require an exception statement for the last child.

Let us add another meta-information line, namely the release date and the conference.
The date information is extracted automatically by [Jekyll](https://jekyllrb.com) from the file name.
For brevity, we squeeze this into the date format *month, year*.

{% raw %}```
<p class="pub-meta">
  {% assign date_format = site.date_format_pubs | default: "%B, %Y" %}
  Published on {{ pub.date | date: date_format }}
  in {{ pub.conference }}
</p>
```{% endraw %}

Next up, we insert the abstract string, which is given the prior explanations quite straightforward.
More interesting is the tagging logic but this will be covered in another article.

<!-- ## Integration into tagging system
...
{% raw %}```
{% if site.feed_show_tags != false and pub.tags.size > 0 %}
<div class="pub-tags">
<span>Tags:</span>
{% for tag in pub.tags %}
<a href="{{ '/tags' | absolute_url }}#{{- tag -}}">{{- tag -}}</a>
{% endfor %}
</div>
{% endif %}
```{% endraw %}
After a first sanity check, if tagging is enabled and the publication has at least one tag specified, the tags are displayed.
The liquid tagging system ... -->

## Endgame: YAML config
Eventually, we have to put in some global variables and adapt some setups to get [Jekyll](https://jekyllrb.com) to render our publication page when triggered by the user.
Creating a new top bar tap is as easy as adding `Publications: "publications"` to your `navbar-links` in the `_config.yml`.
This will create the irresponsible tap visually but also call a `publication.md` file in the root directory if hit by the user.
This only needs to load the layout with the logic defined above.
{% raw %}```
---
layout: pub_feed
title: Publications
---
```{% endraw %}
Furthermore, we have to add a scope-value pair to the [Jekylls](https://jekyllrb.com) [Front Matter Defaults](https://jekyllrb.com/docs/configuration/front-matter-defaults/).
{% raw %}```
defaults:
  - scope:
      type: "pubs"
    values:
      layout: "none"
```{% endraw %}
The `pubs` type gives [Jekyll](https://jekyllrb.com) the nudge to look into `_pubs` for files to iterate over.
That is it.

Happy Coding!
