---
layout: post
title: JavaScript Assets in Rails
postHero: /images/Background.png
author: Thomas Callum Brook
authorTwitter:
gravatar: https://www.gravatar.com/avatar/57d16d81be9c66bf3381299cbc62613b?s=200
postFooter:
---
It's been forever since I've posted, so I thought I'd start a theme. Whenever I solve a mini problem I've experienced in my new web dev career, I'll make a mini post about it. The title will be the problem, and the post my solution. This will serve as a reminder to myself how I fixed the issue, should I encounter it again and also as a possible helping hand to others in future should I make the blog more far reaching.

***JavaScript Assets:***

In Rails, the asset pipeline precompiles all your JS and CSS into neatly processed and minified files and should be the main way of encorporating any new scripts.

When I start adding some simple JS, I usually begin by inserting it into the relevant page within the normal **'\<script\>'** tags. It's the quick and dirty method when your first testing whether the code is doing as expected, and requires no big picture thinking for your app.

Once I had pieced together the code I wanted for a couple of different pages however, I was ready to move it to the pipeline: here begins the issue.

The default asset pipeline config is great for generic code which isn't page specific, and doesn't rely on specific data or DOM elements in order to excute correctly. It all gets loaded in by application.js under the simple line **'//= require_tree .'**

What happens if you don't want each file to be loaded in on each page though? In my example the page specfic JS would raise an error searching for non-existant DOM elements on incorrect pages. At this point the remaining JS won't be executed and a very boring web page provided solely by the HTML template is all that is displayed.

**SOLUTION:**

Some quick googling revealed that:


- Removal of require tree line in application.js (ensuring all other necessary js files are still listed).

- Including each page specific js file via **<%= javascript_include_tag "\<js-file\>" %>** in the relevant view html.erb file.

- Adding the line **'Rails.application.config.assets.precompile += %w( \<js-file.js\> \<js-file2.js\> )'** to config/initializers/assets.rb.


Allows my js files to still be precompiled in production, whilst ensuring they are only used on the required page.


All in all, a quick fix :)

*Tom*
