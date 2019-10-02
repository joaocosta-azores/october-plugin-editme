# In-context editor plugin

This plugin allows in-context editing (click to edit) features to the [OctoberCMS](http://octobercms.com) front-end.

It needs the Rainlab.Translate plugin to work.

This plugin uses Rainlab.Editable plugin code as a base but uses translate strings instead of content blocks, so everything is saved in the database.

The editor has two modes: simple (only plain text and line breaks) and html (wysiwyg editor, it uses the same editor as in the backend).

Implementation is simply replacing the `{{ message|_ }}` translation tags with the component.

## Using the editme component

First you must ensure that the EditMe component is attached to the page or layout.

It can be displayed on the front end like this:

```
title = "A page"
url = "/a-page"

[editme]
==

<!-- This content will be editable -->
{% component 'editme' message='page.title' %}
```

For making the editable text html you only need to set the `type='richeditor'` attribute:

    {% component 'editme' message='page.description' type='richeditor' %}


## Replacing existing translation tags with editable tags.

An example translation tag:

    {{ page.title|_ }}

This tag can be made editable by using the following instead:

    {% component 'editme' message='page.title' %}

## Editing text fields in models

From version 1.0.2 you can edit any model text fields. For example, if you are using Rainlab.Blog plugin you can do this in you blog post page:

    {% component 'editme' message='title' model=post %}

In this case the content will be loaded from the 'title' field in 'post'. And it will be saved in the same place. It also works in loops:

    {% for post in posts %}
        {% component 'editme' message='title' model=post %}
    {% endfor %}

## Permissions

Only administrator with the permission *Manage content* are able to edit content. Administrators must also be logged in to the back-end.

## Front-end JavaScript and StyleSheet

The components in this plugin provide custom stylesheet and javascript files to function correctly on the front-end. Ensure that you have `{% scripts %}` and `{% styles %}` in your page or layout.

The styles also depend on the October JavaScript Framework, so ensure the `{% framework %}` tag is also included in your page or layout.