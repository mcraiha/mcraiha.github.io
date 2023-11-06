---
title: Main Page
layout: page
---

This page is index for some of the coding/computer/pop culture related content I have produced.

## Blog posts
{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date_to_string }}
{% endfor %}
- Things that can muddle your replay feature (upcoming)
&nbsp;  
&nbsp;

## Tools
- Javascript/HTML for showing [BSON hex binary as JSON](http://mcraiha.github.io/tools/BSONhexToJSON/bsonhextojson.html)  
- Javascript/HTML for showing [BSON base64 as JSON](http://mcraiha.github.io/tools/BSONhexToJSON/bsonbase64tojson.html)  
- Javascript/HTML for showing [BSON file as JSON](http://mcraiha.github.io/tools/BSONhexToJSON/bsonfiletojson.html)  
&nbsp;  
&nbsp;

#### Latest update of this index
6th of Nov 2023

#### Contact
mc 📧 raiha.rocks