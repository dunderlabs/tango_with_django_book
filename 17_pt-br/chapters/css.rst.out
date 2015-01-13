.. _css-label:

Cascading Style Sheets
======================
In this chapter, we shall start to add some style to Rango. First we shall do this by creating our own style sheets to give you a feel for how to use CSS. Then we will use the Twitter Bootstrap Toolkit to skin Rango. If you haven't used CSS before it is worth going through the basic guide to CSS we have provided a Crash Course in Chapter :ref:`css-course-label` and then working through these tutorials. However, if you are familiar with the CSS basics you can dive straight in. Of course, if you've already used CSS then you might want to skip straight to the Bootstrap section
:ref:`css-bootstrap-label` .


.. _css-tutorial-label:

CSS and Rango
-------------
Assuming you have some basic CSS knowledge, we'll be taking you through the process
of designing a style sheet for Rango so it looks similar to the screen shots in Chapter one.

Creating and Referencing the Stylesheet
.......................................
Let's get started! First, we need to create a CSS file in which we will store Rango's styles and reference it from the base template. In our Django project's ``static`` directory, create a new subdirectory called ``css``. This will allow us to store all of our CSS files neatly in one location, without mixing them up with other kinds of static files. Within the new ``css`` directory, create a file called ``base.css``.


We now create a reference to the ``base.css`` file in Rango's ``base.html`` template. Open the template from Rango's ``templates`` directory, and modify the ``<head>`` portion of the file to include a new ``<link>`` tag, just like in the example below.

.. code-block:: html
	
	<head>
		...
	    <link rel="stylesheet" type="text/css" href="{% static 'css/base.css' %}" />
	    ...
	</head>


.. note:: Do you remember that we discussed serving static media files earlier in the book? If you do, you should be able to recall that we set up static media files to be served from the URL ``static/``. This means that our new ``base.css`` file should be accessible from the URL ``http://127.0.0.1:8000/static/css/base.css`` - but don't forget to change the server and port if you use different settings. Try it out now!


Some Basic CSS Tweaks
.....................
Now that we have a reference to the ``base.css`` stylesheet, we can begin to add some basic CSS styles to control the presentation of the Rango homepage. Specifically, we'll be adjusting some of the styling properties to prepare the homepage - and other pages - for some more in-depth work in the following sections.

Within the stylesheet, we want to create a CSS style that is applied to the ``<body>`` of our homepage. The ``body`` selector is appropriate for this scenario. Add the following CSS to your stylesheet.

.. code-block:: css
	
	body {
	    font-family: 'Arial', 'Helvetica', sans-serif;
	    font-size: 14pt;
	    margin: 0;
	}

These small changes can have a profound effect of the way in which the homepage is rendered. The first tweak we make is to change the default font that is used for the presentation of our website. Up until now, we've been using the default font that is used by your browser to render webpages. We can control this using the ``font-family`` property.

The font is set to one of either ``'Arial'`` (note the use of strings for font names), ``'Helvetica'``, or any `sans-serif <http://en.wikipedia.org/wiki/Sans-serif>`_ font. This is a cool feature, and is useful when a font specified is not installed on their computers. Developers can therefore use the ``font-family`` property to 'fall back' to another similar looking font. If no font is suitable,  a generic ``sans-serif`` term may be supplied to select any ``sans-serif`` font installed.

We also apply a font size of ``14pt`` to our ``<body>``, slightly larger than the default of ``12pt``. We use this property to demonstrate the many different *units* which you can apply to properties expecting a measurement unit as its corresponding value. There are a large number of units you can use - ranging from percentages (``%``) to pixels (``px``) and even centimetres (``cm``). Check out `this W3Schools page <http://www.w3schools.com/cssref/css_units.asp>`_ for a comprehensive list of the units you can use when specifying measurements. In the ``font-size`` example above, we use a font size of 14pt, much like you would use in a word processor.

Finally, we apply a ``margin`` of ``0`` to the ``<body>``. Note the lack of units specified here: *if you wish to use a zero-value for a particular measurement, you don't need to specify a unit.* Think about it - ``0px`` is equal to ``0pt``! We'll get back to explaining what the margin is later on in Section :num:`css-tutorial-box`, but you should be able to understand what the property does by checking out the before and after screenshots below in Figure :num:`fig-css-basic`, and by experimenting by providing different values for the ``margin``.

.. note:: Properties which we apply to the ``body`` style can cascade down into elements *within* the ``<body>`` in your markup. For example, all elements will now have a font set to one of either ``'Arial'``, ``'Helvetica'`` or another sans-serif font. However, the ``margin`` property does not extend in many cases - this is because its value is *overridden* by default stylings for other elements on your page.

.. _fig-css-basic:

.. figure:: ../images/css-basic.png
	:figclass: align-center
	
	Two screenshots of the Rango homepage: the one on the left is before, without any change to ``body`` styling. The screenshot on the right shows what happens when we apply our ``body`` style. Can you see what the ``margin`` property is doing?

Hardly Earth-shattering stuff, I'm sure you'll agree. However, web development is an incremental process. Patience is a virtue!

.. note:: When you make a change to your stylesheet or webpage, remember to *save the changes* and then *refresh the browser* tab that is looking at the rendered result!

.. _css-tutorial-layout:
Creating the Layout
...................
Now that we've made some basic tweaks to the presentation of Rango's homepage, we can begin to think about the structure of the homepage - and what CSS we'll need to implement the layout. Let's start off by considering Rango's homepage as it currently stands. By looking at Figure :num:`fig-css-blocks-before`, we can see that the page is split into a series of *blocks*, as highlighted by the red rectangles. In simplistic terms, we can consider a block as a portion of the webpage containing some content. In the case of Rango's homepage, we presently have three blocks:

- a block for the **page title**;
- a block containing links for the **available categories**; and
- a block containing **other Rango-related links.**

Thinking of a webpage in terms of blocks is a sensible approach. We can consider a content block as being analogous to both blocks within Django's template system, and so-called content *containers* within a webpage's markup. Webpages can become *modular*, meaning portions of a webpage can be freely added and removed as required.

.. _fig-css-blocks-before:

.. figure:: ../images/css-blocks-before.pdf
	:figclass: align-center
	
	A screenshot of Rango's homepage at present with red boxes, highlighting each unique content *block* that makes up the webpage.

If we further our approach of looking at a webpage in terms of blocks, we can now start to create a layout of a template which will mirror the design of our earlier wireframes. Looking at the wireframe for the homepage at the start of the book, we'll need to increase the number of blocks we use. Specifically, we'll be looking to create the following blocks.

- A **navigation bar** block, creating a nice dark bar at the top of the page.
- The navigation bar will contain the name of our application (**Rango**), along with our links - **Rango-related links** and **user-related links**. User-related links will also contain the name of the person logged in, or a registration link if no-one is.
- We also need a **header block**, which contains some attention-grabbing text for the user to look at.
- A **text block** should be provided to provide simple instructions for users, as well as briefly telling them what Rango is and does.
- A **category block** must be provided, which will contain links to the category pages available for a user to visit.
- The content of our page should also reside within a container of a particular width. The container must also be centred horizontally in the `viewport <http://www.w3.org/TR/CSS2/visuren.html#viewport>`_ of the user's web browser.

A lot to do, perhaps? Not so - a lot of the process is rather repetitive. You'll have it working before you know it, so don't feel overwhelmed! With so many blocks to create, it can be difficult to picture it all fitting together in your head. For your benefit, we included Figure :num:`fig-css-blocks` for you to have a look at. You can see all the blocks laid out within a mockup of a browser window.

We should also briefly consider the use of the block highlighted blue in Figure :num:`fig-css-blocks`. Why do we need it, and what benefits does it bring us? Our wireframe requires that content of the webpage be horizontally centred. By setting the size of the blue container to an arbitrary width, we can then centre this container horizontally, and place our content within the block. Think of it as a webpage within a webpage - at least, to a certain extent! We'll be looking to create our webpage with a minimum width of 960 pixels, `the generally accepted standard for today <http://stackoverflow.com/questions/7415758/why-width-960px>`_.

.. note:: It's good practice to get into the habit of drawing out the design you're looking to create before you even begin writing markup and CSS. Get a sheet of paper, and draw out the layout you wish to achieve in terms of blocks. You'll find as you go through the motions that having that sheet of paper by your side will make it easier to understand what containers correspond to what blocks...and you'll be less inclined to scream and shout in frustration.

.. _fig-css-blocks:

.. figure:: ../images/css-blocks.pdf
	:figclass: align-center
	
	A pictorial representation of the layout we wish to achieve for Rango's homepage, thinking in terms of blocks. There's quite a few, but when laid out, it all makes sense!

Let's work our way from the top of the page to the bottom, creating the bare-bones CSS and corresponding HTML markup to suit. To start, let's create the navigation bar at the very top of the page. We'll need two files open for this, so open up Rango's ``base.html`` template, and the new ``base.css`` stylesheet. Within the base template, we'll be looking to add some new markup to create an element across the very top of the page. Add the following markup just after the start of the ``<body>``.

.. code-block:: html
	
	<!-- Navigation bar (includes navigation links and user links) -->
	<div id="header-container">
	    <div class="content-container">
	        <span id="header-container-title"><a href="/rango/">Rango!</a></span>
	        
	        <span id="header-container-related">
	            Rango-related links
	        </span>
	        
	        <span id="header-container-user">
	            User-related links
	        </span>
	    </div>
	</div>

In the markup snippet above, we introduce two new HTML tags - ``<div>`` and ``<span>``. Essentially, these tags themselves are meaningless, and are only present to provide you with a way to contain and separate your page's content. ``<div>`` tags can be considered a *block-level element* used to contain other content. A block-level element will by default display a line break after it. Conversely, ``<span>`` tags can be considered as *inline elements*, and can be used as a container for text. The difference between block-level elements and inline elements are key - and explain why a ``<div>`` can contain ``<span>`` elements, but not vice versa. For an illustration of the difference between the two, check out Figure :num:`fig-css-nesting-blocks`. In the diagram provided, you see ``<div>`` and ``<span>`` elements represented as boxes. The diagram also hints at how you can nest blocks.

.. _fig-css-nesting-blocks:

.. figure:: ../images/css-nesting-blocks.pdf
	:figclass: align-center
	
	Diagram demonstrating how block-level elements and inline elements are rendered by default. With block-level elements as green, note how a line break is taken between each element. Conversely, inline elements can appear on the same line beside each other. You can also nest block-level and inline elements within each other, but block-level elements cannot be nested within an inline element.

.. note:: If you would like to read more information on the difference between *block* elements and *inline* elements, Check out `this excellent webpage <http://www.impressivewebs.com/difference-block-inline-css/>`_ which highlights the differences clearly for you.

Looking back at our markup, we can see that we follow the same basic pattern as illustrated in Figure :num:`fig-css-nesting-blocks`: a block-level element contains a series of inline elements. The inline elements themselves will contain the text and hyperlinks that we will create later on. We do however include an additional block-level element with class ``content-container``. As you will see from the corresponding CSS styles below, ``content-container`` is the block which keeps our content centred, and within the 960 pixel width that we wish to use. In other words, ``content-container`` is the blue-bound box in Figure :num:`fig-css-blocks`!

We can now add the corresponding group of CSS styles to Rango's ``base.css`` stylesheet. The sample styles are shown below. When entering the styles, remember what the ``#`` and ``.`` selectors do - which ones map to classes, and which one maps to unique element identifiers?

.. code-block:: css
	
	#header-container {
	    height: 40px;
	    line-height: 40px;
	    font-size: 11pt;
	    border: 1px solid #000000;
	}

	#header-container-title {
	    float: left;
	    font-size: 18pt;
	    padding-right: 10px;
	    border: 1px solid #000000;
	}

	#header-container-related {
	    float: left;
	    border: 1px solid #000000;
	}

	#header-container-user {
	    float: right;
	    border: 1px solid #000000;
	}

	.content-container {
	    width: 960px;
	    margin-left: auto;
	    margin-right: auto;
	}

The properties that we make use of above focus on laying out our blocks, rather than changing their appearance. We focus on setting heights, widths and font sizes. While we make use of the ``margin``, ``padding`` and ``float`` properties, we'll come back to these later in Section :num:`css-tutorial-positioning`. Check out `this blog post <http://joshnh.com/2012/10/12/how-does-line-height-actually-work/>`_ for more information on the ``line-height`` property that we set in the ``#header-container`` style.

.. note :: In our CSS example above, we apply a simple 1 pixel border around each element with the ``border`` property so that you can see where elements are positioned within your browser's viewport. If you're happy with the positioning of the navigation bar elements, you can safely remove the ``border`` property within each style to remove the border.

If you now save the two files and load up Rango's homepage in your web browser, you should see something like the screenshot shown in Figure :num:`fig-css-navbar-basic`. 

.. _fig-css-navbar-basic:

.. figure:: ../images/css-navbar-basic.png
	:figclass: align-center
	
	Our navigation bar, rendered with the basic CSS styling applied. Note the border generated around each element of the navigation bar's elements.
	
With our navigation bar now in place, we can now move down to our next block - the header. Within the ``base.html`` template, add the following markup underneath the navigation bar markup you inserted previously.

.. code-block:: html
	
	<!-- Header - including container for grey background -->
	<div id="h1-back">
	    <div class="content-container">
	        <h1>Page Header</h1>
	    </div>
	</div>

Our markup here is much more simple - but we do have fewer elements to contend with. We include our ``<h1>`` tag as we used for our headers previously, but wrap them within a ``content-container`` element to keep the header within our 960 pixel width limit. This is in turn contained within another ``<div>``, acting as the main container for the header block. If we add the following CSS styles into ``base.css``, we are presented with a result just like in the screenshot shown as Figure :num:`fig-css-h1-highlighting`.

.. code-block:: css
	
	h1 {
	    color: #FF0000;
	    font-size: 32pt;
	    margin: 0 0 10px 0;
	    padding: 0;
	}

	#h1-back {
	    padding: 20px 0 10px;
	    margin-bottom: 20px;
	    background: #D9D9D9;
	}

As previously mentioned, we'll get to the ``padding`` and ``margin`` properties in Section :num:`css-tutorial-positioning`. Other properties simply apply a light grey background colour to the element matching style ``#h1-back``, and setting the header text to red with a font size of 32pt.

.. _fig-css-h1-highlighting:

.. figure:: ../images/css-h1-highlighting.pdf
	:figclass: align-center
	
	A screenshot of Rango's homepage, complete with new header and grid lines superimposed to help you understand the positioning of blocks. The green vertical lines signify the edge of the 960 pixel extent. The red box signifies the ``<h1>`` tag and its contents, while the orange box can be matched to the ``h1-back`` ``<div>`` container.

Now that the header block is in, we should update our template to include a new Django block for the header text. Within your new ``<h1>`` tags, replace ``Page Header`` so that your header block now looks like the markup snippet below.

.. code-block:: html
	
	<div id="h1-back">
	    <div class="content-container">
	        <h1>{% block body_block %}Header{% endblock %}</h1>
	    </div>
	</div>

If you now refresh the homepage in your browser, the header will now read ``Header``. To make a custom header for the homepage, open Rango's ``index.html`` template. Locate the existing code that handled the creation of headers. To make things easier, you should look for ``{% if user.is_authenticated %}``. Cut this portion of code, and paste it within a new ``header_block`` Django template block, as shown in the snippet below. Note that we also update the text within the headers, too. **Remove the header tags, too: the tags are provided by our base template!**

.. code-block:: html
	
	{% block header_block %}
	    {% if user.is_authenticated %}
	    Welcome to Rango, {{ user.username }}!
	    {% else %}
	    Welcome to Rango!
	    {% endif %}
	{% endblock %}

Now refresh the page again. Your header should now read ``Welcome to Rango!`` if you aren't logged in, or ``Welcome to Rango`` followed by your username if you are. If this is the case, you've just set up a new block -  ``header_block`` - which can be used to supply custom headers for your various templates used as part of Rango. Easy!

Now that we have our header all sorted, we need to sort out the filler text. As this will be present only within our homepage, we should modify the ``body_block`` block of our ``index.html`` template. Add the following markup directly after the ``body_block`` starts to ensure that it appears above your old markup.

.. code-block:: html
	
	<!-- Filler text -->
	<div class="content-container">
	    Welcome to <em>Rango</em>, the website that lets you <strong>categorise</strong>
	    your favourite websites! Sign up today to get started, or pick a category from
	    below to check out the categorised websites so far.
	</div>

Easy - there's no additional styles to add for the filler text. Awesome! Now let's repeat the process for the category block. Directly underneath your filler text block in ``index.html``, add the following markup.

.. code-block:: html
	
	<!-- Category List -->
	<div id="category-container">
	    <div class="content-container">
	        Category List Here!
	    </div>
	</div>

Now add the following style to ``base.css`` for the ``category-container`` ``<div>`` element.

.. code-block:: css
	
	#category-container {
	    margin-top: 20px;
	}

To make your category list appear within our new container, you now need to perform some more cutting and pasting. In Rango's ``index.html`` template, select the Django template code conditional statement that begins with ``{% if categories %}``. Cut it, and paste it into your new block - removing the placeholder ``Category list here!`` text in the process. Your block should now look like the snippet shown below.

.. code-block:: html
	
	<!-- Category List -->
	<div id="category-container">
	    <div class="content-container">
	        {% if categories %}
	            <ul>
	                {% for category in categories %}
	                <li><a href="/rango/{{ category.url }}">{{ category.name }}</a></li>
	                {% endfor %}
	            </ul>
	        {% else %}
	            <strong>No categories at present.</strong>
	        {% endif %}
	    </div>
	</div>
	
With these changes applied, save all the files you have edited and refresh Rango in your web browser. Give yourself a pat on the back - you've just combined some pretty complex Django template code with your new, CSS-styled markup! We'll come back to make the list of categories really eye-catching in Section :num:`css-tutorial-positioning`.

While we're at it, let's do a quick tidy up of our existing ``index.html`` content. The links that we placed in ``index.html`` can be put into the Django-related links block we made available in the navigation bar. Simply select and cut the link code found at the bottom of the ``body_block`` in ``index.html``. Now paste this into ``base.html``, replacing the ``Rango-related links`` text. We can then move some links to the user links on the right-hand side of the page. Check out the snippet of ``base.html`` below - and note that we remove the line breaks between links (i.e. the ``<br />`` tags)!

.. code-block:: html
	
	<span id="header-container-related">
	    <a href="/rango/add_category/">Add a New Category</a>
	    
	    {% if user.is_authenticated %}
	    <a href="/rango/restricted/">Restricted Page</a>
	    {% endif %}
	</span>
	
	<span id="h-container-user">
	    {% if user.is_authenticated %}
	    Hello, {{ user.username }}!
	    <a href="/rango/logout/">Logout</a>
	    {% else %}
	    <a href="/rango/register/">Register</a>
	    <a href="/rango/login/">Login</a>
	    {% endif}
	</span>

As a final task for this section, let's go back to our navigation back and apply some presentational styling. Specifically, we're looking to make our navigation bar black in colour, with white text to contrast. First, open the ``base.css`` stylesheet and remove any ``border`` properties that were applied earlier to the navigation bar and its child elements. Next, alter the ``#header-container`` style to include a background colour and text colour.

.. code-block:: css
	
	#header-container {
	    height: 40px;
	    line-height: 40px;
	    font-size: 11pt;
	    background: #000000;
	    color: #FFFFFF;
	}

Save your templates and stylesheet, and reload Rango's homepage in your browser. You should see something similar to the screenshot shown in Figure :num:`fig-css-tidied`. While the hyperlinks in the navigation bar may be difficult to read at this stage, we'll be coming back in Section :num:`css-tutorial-linkstyling` to sort this out.

.. _fig-css-tidied:

.. figure:: ../images/css-tidied.png
	:figclass: align-center
	
	A screenshot of the page you should be seeing upon performing the quick tidy-up of your markup. Note now that links now appear in the navigation bar to the right of the ``Rango!`` hyperlink, but they may be pretty difficult to read at present. The webpage is starting to take shape!

If you've got this far, well done. You've sorted out the homepage template's blocks, and it already looks so much more professional than it was looking before! The following subsections cover in more detail several aspects of CSS which we have yet to cover, but are nevertheless important for your understanding. We also address several issues, such as fixing the link colours and making the lists that we use look cool and professional.

.. _css-tutorial-positioning:
Basic Element Positioning
.........................
An important concept that we have not yet covered in this CSS tutorial regards the positioning of elements within your webpage. Most of the time, you'll be satisfied with inline elements appearing alongside each other, and block-level elements appearing on newlines. However, there will be scenarios where you require a little bit more control on where everything goes. In this section, we'll briefly cover four important techniques for positioning elements within your webpage.

CSS *floats* are one of the most straightforward techniques for positioning elements within your webpage. Indeed, we've already made use of floats - have a look at the CSS styles that correspond to Rango's navigation bar! Using floats allows us to position elements to the left or right of a particular container - or the page.

Imagine that we have a ``<div>`` element that contains a series of nested ``<span>`` elements, as shown in Figure :num:`fig-css-positioning-float1`. Now, imagine that we wish to position the blue ``<span>`` elements to the right of our container, and the yellow ``<span>`` elements to their current position - at left of our container.

.. _fig-css-positioning-float1:

.. figure:: ../images/css-positioning-float1.pdf
	:figclass: align-center
	
	Our fictional ``<div>`` container, with four ``<span>`` child elements. Yellow ``<span>`` elements are to remain at the left, while blue ``<span>`` elements should be moved to the right.

Now, we can create two basic CSS styles - ``.yellow`` and ``.blue``, which map to the yellow and blue ``<span>`` elements respectively. The CSS is as follows:

.. code-block:: css
	
	#container {
	    background: #77DD77;
	}
	
	.yellow {
	    float: left;
	    background: #FFDB58;
	}
	
	.blue {
	    float: right;
	    background: #3366FF;
	}

Easy, huh? It makes perfect sense - the ``float: right;`` instructs your browser to float blue ``<span>`` elements to the right of the green container, while yellow elements are instructed to float to the left. The resultant output is shown at the top of Figure :num:`fig-css-positioning-float2`. There is however a slight issue with this - the container element no longer wraps around the ``<span>`` elements. You may not think that this is not much of an issue - but what if you have elements further down your page which depend on the ``<div>`` container to clear the ``<span>`` elements for them? Your layout could become a mess.

.. _fig-css-positioning-float2:

.. figure:: ../images/css-positioning-float2.pdf
	:figclass: align-center
	
	Our float example with two figures - the top without the ``overflow: hidden;`` trick applied, the second with the trick applied. Note how the container wraps around the floated elements in the bottom illustration, just like you would expect.

There are two ways to fix this issue. The first approach is to simply apply a ``height`` to the container ``<div>`` which would cover the ``<span>`` elements. However, there may be circumstances when the height of the ``<span>`` elements may vary, and you simply wouldn't know what height to specify. Fortunately, you can apply the ``overflow: hidden;`` property and value pairing to your container to ensure that the ``<span>`` elements are appropriately cleared. For more information on how this trick works, have a look at `this QuirksMode.org online article <http://www.quirksmode.org/css/clearing.html>`_. Your end result should then look like the illustration at the bottom of Figure :num:`fig-css-positioning-float2`.

.. note:: For further reading on floats, check out the `W3Schools tutorial <http://www.w3schools.com/css/css_float.asp>`_, or perform a `web search <https://www.google.co.uk/search?q=css+float>`_. You can also play around with an `online version of our float example on JSFiddle <http://jsfiddle.net/5DXWc/1/>`_.

A more advanced means of positioning elements within a page is to make use of the CSS ``position`` property. By default, elements are positioned on a page *statically*, meaning that such elements are positioned according to the normal flow of the webpage. By applying the ``position`` property, you can change the type of positioning your browser uses to place the element on your webpage. There are `several types of positioning you can use <http://www.w3schools.com/css/css_positioning.asp>`_, but we'll focus quickly on *relative* and *absolute* positioning here.

Imagine we have a ``<div>`` element on a blank page. We then apply the following CSS to the webpage - and if you remember your CSS selectors, you will see that the style below is mapped to the ``<div>`` element we create.

.. code-block:: css
	
	div {
	    width: 100px;
	    height: 100px;
	    background: #3366FF;
	}

The rendered result of this simple page is a blue box - 100 pixels square - located at the top of the webpage. This can be seen as blue box 1 in Figure :num:`fig-css-positioning-relative`, or online at `this JSFiddle <http://jsfiddle.net/735Ht/>`_. If we were then to apply the ``position: relative;`` property and value pairing to our style, the ``<div>`` element on our webpage will then be *positioned relatively* - or in other words, the element is *positioned relative to the position it would otherwise be sitting at.* We could then apply some additional CSS property and value pairings to our ``div`` style to move the element from its original position. For example, we can alter the style to now look like the following CSS style.

.. code-block:: css
	
	div {
	    width: 100px;
	    height: 100px;
	    background: #3366FF;
	    position: relative;
	    left: 200px;
	    top: 80px;
	}

Try and think what this means in English: *position the element relatively, pushed along 200 pixels from the left, and pushed from the top by 80 pixels.* We can also apply ``bottom`` and ``right`` properties, which push from the bottom and right respectively. The end result can be seen as box 2 in Figure :num:`fig-css-positioning-relative`, or online at `this updated JSFiddle <http://jsfiddle.net/735Ht/2/>`_.

.. _fig-css-positioning-relative:

.. figure:: ../images/css-positioning-relative.pdf
	:figclass: align-center
	
	A mockup demonstrating how relative positioning works. Box 1 is our original box, statically positioned. With relative positioning applied, we move the box 200 pixels to the right (pushing from the left), and 80 pixels down (pushing from the top).

In contrast to relative positioning, *absolute positioning* places an element *relative to its first parent element that has a position other than static.* This can seem a little bit confusing, so let's work through this step-by step. Once again, imagine we have a ``<div>`` element on a blank page. We apply a similar style to the relative positioning example above - but this time we choose a nice orange colour to differentiate between the two examples.

.. code-block:: css
	
	div {
	    width: 100px;
	    height: 100px;
	    background: #FF6600;
	}

You can see this example as box 1 in Figure :num:`fig-css-positioning-absolute1`, or online at `this JSFiddle <http://jsfiddle.net/HyZwN/>`_. We then apply ``position: absolute;`` with the following ``left`` and ``top`` properties.

.. code-block:: css
	
	div {
	    width: 100px;
	    height: 100px;
	    background: #FF6600;
	    left: 200px;
	    top: 0;
	}

Our result can be seen as box 2 in Figure :num:`fig-css-positioning-absolute1`, or online at `this updated JSFiddle <http://jsfiddle.net/HyZwN/1/>`_. Note how the orange box is now at the very top of the browser's viewport - this is due to the ``top`` property being set to ``0``. *In other words, the element appears in relation to the top-left corner of the browser's viewport, at co-ordinates (0, 0).*

.. _fig-css-positioning-absolute1:

.. figure:: ../images/css-positioning-absolute1.pdf
	:figclass: align-center
	
	A mockup demonstrating absolute positioning. Box 1 is positioned within the webpage statically, while box 2 is positioned absolutely, 200 pixels to the right (pushed from the ``left``) and flush with the top of its parent container, ``<body>``.

Easy, right? We can go a step further and even position an element absolutely *within* a container. Imagine another blank page. We then add the following HTML markup

.. code-block:: html
	
	<div class="container">
	    <div class="nested"></div>
	</div>

This creates a container of class ``nested`` which is nested within a further container, ``container``. We then apply the following CSS styles to the webpage.

.. code-block:: css
	
	.container {
	    width: 300px;
	    height: 200px;
	    background: #C0C0C0;
	}
	
	.nested {
	    width: 100px;
	    height: 50px;
	    background: #FF6600;
	}

The result is shown in the left illustration in Figure :num:`fig-css-positioning-absolute2`, and is available online at `this JSFiddle <http://jsfiddle.net/K9suE/>`_. We can then position the inner ``<div>`` absolutely within our container by setting the container's ``position`` property to ``relative``. This changes the position from static to relative. We can then position our nested element absolutely, and apply some measurements.

.. code-block:: css
	
	.container {
	    width: 300px;
	    height: 200px;
	    background: #C0C0C0;
	    position: relative;
	}
	
	.nested {
	    width: 100px;
	    height: 50px;
	    background: #FF600;
	    position: absolute;
	    bottom: 5px;
	    left: 5px;
	}

The end result is shown to the right of Figure :num:`fig-css-positioning-absolute2`, and can be seen online with `this JSFiddle <http://jsfiddle.net/K9suE/1/>`_. We have moved our nested element to sit at the bottom of the container with a 5 pixel cushion from the edges. This wouldn't be possible if we didn't change the ``position`` property of the container. Remember, absolute positioning places an element *relative to its first parent element that has a position other than static.*

.. _fig-css-positioning-absolute2:

.. figure:: ../images/css-positioning-absolute2.pdf
	:figclass: align-center
	
	A mockup demonstrating absolute positioning within a container, where its ``position`` property is set to a value other than ``static``. The left illustration shows the two elements without positioning properties applied, while the second shows the effect of applying absolute positioning to the nested element, and applying the value of ``5px`` to both ``bottom`` and ``left`` respectively.

Now that we've covered the four main concepts, let's summarise everything for you in five bullet points.

- By default, elements on a webpage are positioned *statically*.
- *CSS floats* can be used to position elements to the left or right of its parent container.
- You can position elements *relative* to where they would otherwise be with the property ``position: relative;``.
- Elements can also be *positioned absolutely* in relation to the first parent element with a ``position`` value other than ``static``.
- You can adjust the positioning of relatively and absolutely positioned elements via the use of the ``top``, ``bottom``, ``left`` and ``right`` properties, `using any valid unit of measurement <http://www.w3schools.com/cssref/css_units.asp>`_.

We'll be making use of absolute and relative positioning techniques when we come to styling our categories list for the Rango homepage in section :num:`css-tutorial-lists`. Positioning elements is an incredibly important part of web development. While this section only scratches the surface on what is possible, there are countless tutorials and guides online that you can check out. Check out `this webpage <http://designshack.net/articles/css/the-lowdown-on-absolute-vs-relative-positioning/>`_, `this webpage <http://coding.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/>`_ and `this online tutorial <http://www.barelyfitz.com/screencast/html-training/css/positioning/>`_ for starters!

.. _css-tutorial-box:
Padding, Margins and the Box Model
..................................
Throughout the CSS tutorial so far, we've repeatedly mentioned - and made use of - *padding* and *margins.* We've deliberately waited until now to discuss what these properties are because they are another important aspect you need to understand when styling your webpages. As such, discussing them is worthy of their own subsection. However, to explain what padding and margins are, we first need to introduce you to the *CSS box model.*

Each element that you create on a webpage can be considered as a box. The `CSS box model <http://www.w3.org/TR/CSS2/box.html>`_ is defined by the W3C as a formal means of describing the elements or boxes that you create, and how they are rendered in your web browser's viewport. Each element or box consists of *four separate areas*, all of which are illustrated in Figure :num:`fig-css-box-model`. The areas - listed from inside to outside - are the *content area*, the *padding area*, the *border area* and the *margin area*.

.. _fig-css-box-model:

.. figure:: ../images/css-box-model.pdf
	:figclass: align-center
	
	An illustration demonstrating the CSS box model, complete with key showing the four areas of the model.

For each element, you can create a margin, apply some padding or a border with the respective properties ``margin``, ``padding`` and ``border``. Margins clear a transparent area around the border of your element, meaning margins are incredibly useful for creating a gap between elements. In contrast, padding creates a gap between the content of an element and its border. This therefore gives the impression that the element appears wider. If you supply a background colour for an element, the background colour is extended with the element's padding. Finally, borders are what you might expect them to be - they provide a border around your element's content and padding.

As a brief example, consider Figure :num:`fig-css-box-example`. Here, we define an element and apply the CSS style shown to the left of the Figure. The browser renders the element that appears on the right. Even though we specify a width of 100 pixels across, the resultant width is 126 pixels. Similarly, the height of the element is 86 pixels - even though we specify the total height to be only 80 pixels. This is because we also set a padding of 10 pixels, and a border of 3 pixels. As they both apply around all four sides of our element, we must add each value twice to our width and to our height. As can be seen on the `W3Schools website <http://www.w3schools.com/css/css_boxmodel.asp>`_, you can use formulae to work out the widths and heights of your elements by taking into consideration padding and borders.

.. _fig-css-box-example:

.. figure:: ../images/css-box-example.pdf
	:figclass: align-center
	
	CSS style and the corresponding box that is rendered in the browser's viewport. Are the widths and heights of the element what you would expect them to be?

In contrast, margins are not included in the width or height of an element. To demonstrate this, look at Figure :num:`fig-css-box-example2`. Here, three elements all use the same style defined on the left, meaning all three have applied to them a *left margin* of 10 pixels. Even though we apply this margin, the width of each element still appears rendered as 40 pixels. To the left of each element, a small transparent 10 pixel gap is present. This is the margin - and without it, the elements would be sitting right next to each other, giving the impression of only one orange, larger element.

.. _fig-css-box-example2:

.. figure:: ../images/css-box-example2.pdf
	:figclass: align-center
	
	A modified CSS style that is applied to the three orange blocks to the right. A margin is applied to the left of each element. Notice that the width of each element stays the same as defined in the style.

.. note:: You can define different sizes for each side of your element's padding, borders or margins. Check out the ``margin`` property definition on the `W3Schools website <http://www.w3schools.com/cssref/pr_margin.asp>`_ for more information and examples. You can also use the ``padding`` properties for setting padding in the same way. The ``border`` property has different options you can set - `check it out here <http://www.w3schools.com/css/css_border.asp>`_.

.. warning:: When messing around with borders and padding, take great care with widths and heights. It's so easy to forget that padding and borders are added onto the height and width of your elements - and can screw up the layout of elements in close proximity.

.. _css-tutorial-lists:
Stylising Lists
...............
Lists are everywhere. Whether you're reading a list of learning outcomes for a course or a reading a list of times for the train, you know what a list looks like and appreciate its simplicity. As we know from our list of categories on Rango's homepage, HTML provides us with the ability to create lists, too. Using lists - `according to Brainstorm and Raves <http://brainstormsandraves.com/articles/semantics/structure/>`_ - promotes good HTML document structure, allowing text-based browsers, screen readers and other browsers that do not support CSS to render your page in a sensible manner. To demonstrate their point, look at Figure :num:`fig-css-lists-which`. What would you prefer: the page on the left, or the page on the right?

.. _fig-css-lists-which:

.. figure:: ../images/css-lists-which.png
	:figclass: align-center
	
	Two screenshots of Google Chrome displaying the same content. On the left, we use a HTML list. On the right, the links to each hyperlink are placed next to each other without using lists. Which seems more intuitive?

There are three boxes in Rango's homepage which should use some form of list. While we've already got our list of categories sorted, our hyperlinks in the navigation bar - both for user-related and Rango-related links - are not yet in list form, yet should be! We're going to demonstrate how to convert the markup to list form, and how to style these lists to fit in with the page layout.

We'll once again be modifying Rango's ``base.html`` template, and adding new styles to the ``base.css.`` stylesheet. Within ``base.html``, we need to add an `unordered list <http://www.w3schools.com/tags/tag_ul.asp>`_ for both our Rango-related links and user-related links. Find the two relevant ``<span>`` containers and modify them such that they look like the markup snippet below.

.. code-block:: html
	
	<!-- Rango-related links -->
	<span id="header-container-related">
	    <ul class="navbar-list">
	        <li><a href="/rango/add_category/">Add a New Category</a></li>
	        {% if user.is_authenticated %}
	        <li><a href="/rango/restricted/">Restricted Page</a></li>
	        {% endif %}
	    </ul>
	</span>
	
	<!-- User-related links -->
	<span id="header-container-user">
	    <ul class="navbar-list">
	        {% if user.is_authenticated %}
	        <li>Hello, {{ user.username }}!</li>
	        <li><a href="/rango/logout/">Logout</a></li>
	        {% else %}
	        <li><a href="/rango/register/">Register</a></li>
	        <li><a href="/rango/login/">Login</a></li>
	        {% endif %}
	    </ul>
	</span>

Hopefully you'll agree the changes you have to make are relatively straightforward. Essentially, all you need to do is wrap each link within *list element* tags (``<li> </li>``), and in turn wrap your list elements within unordered list tags (``<ul> </ul>``). We also combine the Django template commands within our list. Depending on whether a user is logged in or not, different list items will be sent back to their browser. We also apply a class to our unordered lists, ``navbar-list``. We'll be making use of this class very shortly.

.. note:: Not all of the list items we use are hyperlinks. One of the user-related list items simply prints the username of the logged in individual. In this instance, there is a lack of a ``<a>`` tag around the text. This isn't a typo: it's deliberate!

With these changes applied, we can begin to style our links. If you view Rango's homepage in this present state, you will most likely observe the links in the navigation bar are messed up. To fix this, we need to apply some styling to our lists to change the presentation of our lists. Let's do this now by adding the following styles to our ``base.css`` stylesheet.

.. code-block:: css
	
	.navbar-list {
	    margin: 0;
	    padding: 0;
	    list-style-type: none;
	}
	
	.navbar-list li {
	    display: inline;
	    margin-left: 10px;
	}

For our explanation, look at the first style. Note that the selector matches to our unordered list elements thanks to the class attribute ``navbar-list``. This was applied to each list, and thus removes the need to apply the same properties under different styles. *A HTML element can have both a unique identifier and class(es) applied to it, too!*

As the style ``.navbar-list`` matches our ``<ul>`` elements, the default margin and padding that is applied to the list is removed by setting the ``margin`` and ``padding`` properties to a value of ``0``. We also change the ``list-style-type`` to ``none``, thus removing the bullet point. There's actually quite a few types of bullet you can use. It's worth reading up on the ``list-style-type`` `property on W3Schools <http://www.w3schools.com/cssref/pr_list-style-type.asp>`_ to see just how many values you can choose from!

Our second style applies to each ``<li>`` element contained within an element matched to ``.navbar-list`` - or, in other words, our unordered list elements. We switch the ``display`` type from the default ``block`` to ``inline`` (see Section :num:`css-tutorial-layout` for a discussion on block-level and inline elements), and add some ``margin`` to the left of each list element to space them out. Your lists should now be positioned correctly, just like they were before. We'll sort out the colouring of the links in Section :num:`css-tutorial-linkstyling`.

In order for our template to match the wireframe shown back at the start of the book, we'll also need to adjust the styling for our category list, too. As our markup for this block already uses an unordered list of hyperlinks, all we need to do is write some CSS to make everything look pretty! In Rango's ``base.css`` stylesheet, let's add the following three styles. We'll explain what each style does afterwards.

.. code-block:: css
	
	#category-container ul {
	    padding: 0;
	    margin: 0;
	    list-style-type: none;
	    background: #C0C0C0;
	    overflow: hidden;
	}
	
	#category-container ul li {
	    float: left;
	    position: relative;
	    background: #3399FF;
	    width: 310px;
	    height: 150px;
	    margin-bottom: 15px;
	    margin-right: 15px;
	}
	
	#category-container ul li:nth-child(3n) {
	    margin-right: 0;
	}

Our first style ``#category-container ul`` matches to the unordered list within our ``category-container`` ``<div>`` element. For the unordered list, we remove the padding and margin that is applied by default to the unordered list container, and also remove the bullet point styling using ``list-style-type: none;``. For sanity's sake, we also set a light-grey background to see what's going on - we'll be removing this when we are sure everything is working as expected. The ``overflow: hidden;`` property is applied to ensure the ``<ul>`` container's height is set correctly. We need this as we'll be floating our list elements. Check out Section :num:`css-tutorial-positioning` for more information on why we need ``overflow: hidden;``, or have a look at `this webpage <http://www.quirksmode.org/css/clearing.html>`_.

Our second style maps to each list element (``<li>``) within our category list container. Within this style, we apply quite a few properties, so it's worth going through each one-by-one in list form to help you understand the reasoning behind each.

- First, we ``float`` each list element to the ``left``. This produces the effect of squashing each element to the left of the ``<ul>`` container as much as possible. As the full width of the container is reached, further elements are pushed onto a newline automatically. Check out Figure :num:`fig-css-lists-cats-float` for a pictorial example.
- We then set the ``position`` property to ``relative``. While this doesn't change the positioning of the ``<li>`` element itself (we don't set one or more of ``top``, ``bottom``, ``left`` or ``right``), it'll be incredibly useful for us when it comes to styling the contained hyperlinks shortly.
- We apply a blue background colour so we can see where our list element appears on the page.
- We then apply a ``width`` and ``height`` to each list element. The ``width`` isn't picked out of thin air - we calculate it based on the available room we have on-screen. Check out Figure :num:`fig-css-lists-cats-float` to see how we came to the value of 310 pixels. Conversely, the ``height`` is randomly picked as it provides good proportions to the ``width``.
- We finally apply margins to each list element, allowing us to space them out from one another. We apply a margin at the bottom of each list element of 15 pixels to provide spacing between multiple rows of elements. The right-hand margin is applied - also of 15 pixels - to space each list element out horizontally.

Our final style uses a fancy `CSS3 psuedo-selector <http://reference.sitepoint.com/css/pseudoclass-nthchild>`_ to select every *third* ``<li>`` element within our ``category-container``. For every third element, we remove the right-hand margin that would be otherwise applied to the element? Have a look at Figure :num:`fig-css-lists-cats-float` to figure out why we wish to achieve this.

.. _fig-css-lists-cats-float:

.. figure:: ../images/css-lists-cats-float.pdf
	:figclass: align-center
	
	Pictorial representation of the category list styled. Take note of the widths of the container and each element. The 310 pixel width is wide enough to fit in a 15 pixel margin to the right of each element except every third element. Think about it: we don't need a margin at the end of each line!

We're so close to finishing! One last aspect which we need to address is the positioning of the textual link within each category box. If you cast your mind back to our wireframes, you'll recall that the text appears at the bottom left. We can do this by adding the following style to Rango's ``base.css`` stylesheet.

.. code-block:: css
	
	#category-container ul li a {
	    font-size: 16pt;
	    font-weight: bold;
	    color: #333333;
	    background: #D9D9D9;
	    
	    position: absolute;
	    bottom: 5px;
	    left: 5px;
	    padding: 5px;
	}

You've probably noticed that our selectors are getting ever more complex - this time, we select each hyperlink (``<a>`` tag) within each list element, within our unordered list...within our ``category-container`` ``<div>``. Phew!

With the CSS above, we've added a blank line to separate out the properties applied. At the top, we apply trivial presentational properties. We increase the font size to 16 point and make the font bold. Additionally, we apply a dark grey for the font colour, and a light grey background.

The second half of our style's properties is where things get interesting if you get excited by this stuff. We ``position`` the link ``absolute``ly, which then allows us to position the element 5 pixels from the ``bottom`` and ``left`` of the `next containing element which is not positioned statically <http://css-tricks.com/absolute-positioning-inside-relative-positioning/>`_. Since we set the ``position`` of each containing ``<li>`` element to ``relative``, the container we latch onto is the ``<li>`` element. Confused?

All being well, the result of this application of CSS style should yield a result similar to that shown in the screenshot in Figure :num:`fig-css-lists-cats-end`. The number of categories which you have present may vary - we added two more from our original three to demonstrate the list working both horizontally and vertically.

.. _fig-css-lists-cats-end:

.. figure:: ../images/css-lists-cats-end.png
	:figclass: align-center
	
	A screenshot of Rango's redeveloped homepage with our category list now nicely styled.

Let's finally show you how to replace the blue background colour with an image suitable for a category. To implement this feature fully, you'll need to add an additional field to Rango's ``Category`` model to pull the image URL from. Assume we have an image of a laptop for category ``laptops``. The markup the list element for such a category would look like the following markup snippet.

.. code-block:: html
	
	<li><a href="/rango/laptops">laptops</a></li>

If our laptop image is placed within our ``static`` media directory in ``categories/laptop.jpg``, we can then apply the following `inline CSS <http://www.w3schools.com/css/css_howto.asp>`_ to our markup, producing the following result.

.. code-block:: html
	
	<li style="background: url('/static/categories/laptop.jpg') no-repeat;">
	    <a href="/rango/laptops">laptops</a>
	</li>

.. note:: Why use inline CSS here? We told you to earlier to avoid inline styling as much as possible. However, adding CSS directly to the markup here is advantageous as you can easily pull out the path to your category's image and place it in your CSS property value. If you kept the CSS in a separate stylesheet, you'd need to define a style for each category which simply isn't feasible. How could the stylesheet know how many categories your database has?

Refreshing Rango's homepage in your browser should produce a result similar to that shown in Figure :num:`fig-css-lists-cats-end`, with the background image replacing the plain blue background. If you do see this, give yourself another pat on the back. Learning this stuff isn't easy, and is a source of great frustration to many. However, if you have worked your way through the tutorial step-by-step, you should now have a better understanding of how HTML, CSS and the relevant styles all piece together.

.. note:: Don't forget to remove the ``background`` property in your ``#category-container ul`` style to rid yourself of the grey categories list background!

.. _css-tutorial-linkstyling:
Styling Hyperlinks
..................
Our final gripe with Rango's template is the colour in which the links in our navigation bar appear. The most recent screenshot in Figure :num:`fig-css-lists-cats-end` still shows the black navigation bar with dark purple or blue links on them, which don't contrast very well with the black.

We'll only need one file for this, and that's Rango's stylesheet, ``base.css``. Open the file and add the following two styles, which we explain in detail below.

.. code-block:: css
	
	#header-container a {
	    color: #00BFFF;
	    text-decoration: none;
	}
	
	#header-container a:hover {
	    color: #FFFFFF;
	    text-decoration: underline;
	}

The first style maps to all hyperlinks (or anchors, hence the ``<a>``) within the ``header-container`` element. We set the colour to a light blue, and remove the underlining which is applied to links by default. We then use a further `pseudo selector <http://css-tricks.com/pseudo-class-selectors/>`_, ``:hover``, to be called whenever a user hovers over a hyperlink within ``header-container``. When this happens, the font colour is changed to bright white, and underlining is applied to the link's text. Check our Figure :num:`fig-css-lists-hover` for an example of the effect in action. Job done, template created!

.. _fig-css-lists-hover:

.. figure:: ../images/css-links-hover.pdf
	:figclass: align-center
	
	Cropped screenshots of our modified navigation bar hyperlinks. Now they're much more readable - and they even change colour when you hover over them. How exciting!

.. _css-bootstrap-label:

Working with Twitter Bootstrap
------------------------------
Over the past few years, web development has become a much easier job than it was previously. As browsers have slowly adopted W3C standards and implemented them *correctly* (see `this Wikipedia article <http://en.wikipedia.org/wiki/Internet_Explorer_box_model_bug>`_ about Internet Explorer), we've seen an explosion in ready-made toolkits that provide developers with much of the CSS scaffolding for you.

One of the most notable success stories in this particular area is the `Twitter Bootstrap <http://getbootstrap.com/>`_ project. After only six months of being released, it had become the most popular project on GitHub, and many developers have adopted the Bootstrap project to help with the development of their websites.

.. note:: You may be wondering why we didn't tell you about this earlier. Our approach is well-founded: in order to be able to use these toolkits, you *must* have a good understanding of the concepts to be able to use them! By teaching you the basics of CSS, you can now develop websites using the Twitter Bootstrap toolkit.

Exercises
---------

* Since the Free CSS templates follow the same format it is pretty easy to vary the style. Download another Free CSS template, for example, illustrative, and move the folder into the static/css folder. Now, create a new base template called, base-illustrative.html. Use the index.html provided in the illustrative download as a guide to creating base-illustrative.html for your application. 







