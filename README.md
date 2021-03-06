Frontend standards
========================

## Overview

This document details the guidelines and standards adhered to by the Creative Technology department at TMW, and all web applications built should take these into consideration.  It is an evolving document and should be reviewed as and when required to keep up with changes in technology and best practice.

These guidelines have been compiled looking at various previously written guidelines - credit goes to [Isobar](http://na.isobar.com/standards) and [CSS Wizardry](http://cssguidelin.es/) both of which have been used as foundations to build upon for this document, and in some sections been directly quoted.

## Contents

1. [General Guidelines](#section-intro)
  1. [Indentation](#section-intro-indentation)
  2. [Readability vs Compression](#section-intro-readability)
2. [Browser Support](#section-browsersupport)
3. [Base Templates and frameworks](#section-frameworks)
4. [Markup](#section-markup)
	1. [HTML5](#section-markup-html5)
	2. [General Markup Guidelines](#section-markup-general)
	3. [Quoting Attributes](#section-markup-attributes)
	4. [Character Encoding](#section-markup-encoding)
	5. [Accessibility](#section-markup-accessibility)
5. [CSS](#section-css)
	1. [General CSS Principles](#section-css-general)
	2. [Syntax and formatting](#section-css-formatting)
	3. [Indenting](#section-css-indenting)
	4. [OOCSS](#section-css-ocss)
	5. [Typography](#section-css-typography)
	6. [Reset vs Normalisation](#section-css-reset)
	7. [Comments](#section-css-comments)
	8. [Specificity, IDs and classes](#section-css-specificity)
	9. [Conditional Stylesheets](#section-css-conditionalstylesheets)
	10. [!important](#section-css-important)
	11. [Magic Numbers and absolutes](#section-css-magicnumbers)
	12. [Images](#section-css-images)
	13. [Debugging](#section-css-debugging)
	14. [Preprocessors](#section-css-preprocessors)
	15. [Responsive Design](#section-css-rwd)
	16. [Tools](#section-css-tools)
6. [Sass](#section-sass)
	1. [General Sass Principles](#section-sass-general)
	2. [Nesting](#section-sass-nesting)
	3. [@extend](#section-sass-extend)
	4. [Mobile First](#section-sass-mobilefirst)
7. [JavaScript](#section-js)
	1. [General JavaScript Principles](#section-js-general)
	2. [Formatting and code sensibility](#section-js-formatting)
	3. [Libraries](#section-js-libraries)
	4. [Plugins](#section-js-plugins)
	5. [Dependency Management](#section-js-dependencies)
	6. [jQuery Best Practices](#section-js-jquery)
	7. [Debugging](#section-js-debugging)
	8. [Resources](#section-js-resources)
8. [Accessibility](#section-accessibility)
9. [Performance and Optimisation](#section-performance)
	1. [Assets](#section-performance-assets)
	2. [Tools](#section-performance-tools)


***

<a name="section-intro"></a> General Guidelines
===========================================

- All frontend code should display clear separation of presentation, content, and behaviour.
- Markup should be well formed, semantically correct and generally valid.
- JavaScript should [progressively enhance](https://www.gov.uk/service-manual/making-software/progressive-enhancement.html) the experience
	- Use feature detection rather than browser sniffing (edge cases such as performance are acceptable)
- Gracefully degrade functionality when not present (e.g GPS, box-shadow, forms etc).


<a name="section-intro-indentation"></a> Indentation
------------------------------------------------

For all languages, indent your code with tabs.  The default tab size should be set as 2.

<a name="section-intro-readability"></a> Readability vs Compression
-------------------------------------------------------------

We encourage readability over file-size when it comes to maintaining existing files. Plenty of white-space is encouraged, along with ASCII art, where appropriate. There is no need for any developer to purposefully compress HTML or CSS, nor obfuscate JavaScript.

We will use server-side or build processes to automatically minify and gzip all static client-side files, such as CSS and JavaScript.

***

<a name="section-browsersupport"></a> Browser Support
========================================

- Internet Explorer 9+
- Firefox
- Google Chrome
- Safari
- Opera

We test in the latest version of Firefox, Chrome and Safari due to them using incremental auto-updates.

***

<a name="section-frameworks"></a> Base Templates and frameworks
======================================================

We use [Kickoff](http://trykickoff.com), a lightweight frontend framework we maintain for creating scalable, responsive sites.

When building static templates, we use [Statix](http://tmwagency.github.io/statix/), which integrates Kickoff with Assemble to make templating faster and more maintainable.

Both Kickoff and Statix are actively maintained by the Creative Tech team at TMW; for more information about their features, getting started and demos, see the [Kickoff documentation site](http://tmwagency.github.io/kickoff/).

***

<a name="section-markup"></a> Markup
===============================

<a name="section-markup-html5"></a> HTML5
---------------------------------------

The HTML5 Doctype and HTML5 features will be used on projects when appropriate.

To ensure HTML5 markup compatibility with older browsers, use either:

- [Modernizr](http://www.modernizr.com/) - consider bloat, use the build generator to decrease its size
- [HTML5shiv](http://code.google.com/p/html5shiv/) - no feature detection, simply ensures markup compatibility

We will test our markup against the [W3C validator](http://validator.w3.org/), to ensure that the markup is well formed. 100% valid code is not a goal, but validation certainly helps to write more maintainable sites as well as debugging code. TMW does not guarantee markup is 100% valid, but instead assures the cross-browser experience is consistent.


<a name="section-markup-general"></a> General Markup Guidelines
---------------------------------------------------------

The following are general guidelines for structuring your HTML markup. Authors are reminded to always use markup which represents the semantics of the content in the document being created.

- Use `<p>` elements for paragraph delimiters as opposed to multiple `<br />` tags.
- Items in list form should always be housed in a `<ul>`, `<ol>`, or `<dl>`, never a set of `<div>`s or `<p>`s.
- Place an HTML comment around DIV tags that contain a larger amount of markup to indicate the element you're closing. It will help when there is a lot of nesting and indentation. For example:

		<!-- Start of .contentWrap -->
		<div class="contentWrap">

			//some markup goes here

		</div> <!-- End of .contentWrap -->


- Make use of `<thead>`, `<tbody>`, and `<th>` tags (and `Scope` attribute) when appropriate.
- Make use of `<dl>` (definition lists) and `<blockquote>`, when appropriate.
- Use `<label>` fields to label each form field.  The `for` attribute should associate itself with the input field, so users can click the labels and obtain focus.
- Do not use the `size` attribute on your input fields. The `size` attribute is relative to the font-size of the text inside the input. Instead use CSS width.
- Always use title-case for headers and titles. Do not use all caps or all lowercase titles in markup, instead apply the CSS property `text-transform: uppercase/lowercase`.
- Use microformats and/or Microdata where appropriate, specifically `hCard` and `adr`.

...and the single most important rule...

- Tables **shouldn't ever** be used for page layout – only for tabular data.

<a name="section-markup-attributes"></a> Quoting Attributes
----------------------------------------------------

While the HTML5 specification defines quotes around attributes as optional for consistency with attributes that accept whitespace, all attributes should be quoted.

	<a href="mylink.html" title="My Link Title" data-attribute="32">This is my Link</a>


<a name="section-markup-encoding"></a> Character Encoding
-----------------------------------------------------

All markup should be delivered as UTF-8, as it's the most friendly for internationalization. It should be designated in both the HTTP header and the head of the document.

Set the character set using `<meta>` tags:

	<meta charset="utf-8">


<a name="section-markup-accessibility"></a> Accessibility
-------------------------------------------------

Consider ARIA integration for high accessibility sites.

For our full guidelines on Accessibility, refer to the [Accessibility Guidelines](#section-accessibility) section of this document.

***

<a name="section-css"></a> CSS
============================

<a name="section-css-general"></a> General CSS Principles
----------------------------------------------------

- Every time you write inline styles in your markup, a frontend developer somewhere dies - whether it's in a style tag or directly in the markup. Don't do it.
- Add CSS through external files, minimizing the number of files, if possible. CSS should always be included in the `<head>` of the document.
- Use the `<link>` tag to include, never `@import`.
- Ensure markup and style stays separate (some style classes are allowed, e.g imageReplace etc).  Only use style only markup if you absolutely have to (e.g extra wrapping elements); consider `:before` and `:after` CSS pseudo-elements if styles are not 100% necessary.


<a name="section-css-formatting"></a> Syntax and formatting
-------------------------------------------------------

- Use multi-line CSS declarations. This helps with version control (diff-ing single line CSS can be a nightmare). Group CSS declarations by type - keeping font related styling together, layout styling together etc - and ordered by relevance, not alphabetized.
- All CSS rules should have a space after the selector colon and a trailing semi-colon.
- Selectors should be specified using a simplified version of BEM:

		/* Descriptors use camel-casing if more than one word: e.g. twoWords */
		.skipToContent {
		    ...
		}

		/* ========= */

		/* Child elements use single hyphens: - */
		.form-controlGroup {
		    ...
		}

		/* ========= */

		/* Modifier element use a double hyphen: -- */
		.btn.btn--primary {
		    ...
		}

		/* ========= */

		/* Element state: .is- */
		.is-active {
		    ...
		}

		/* ========= */

		/* Sass variables are dash-case */
		a {
		    color: $color-primary;
		}

- Use shorthand when specifying multiple values.  Remember longhand can be shorter for single values.
- Multi-attribute selectors should go on separate lines.
- Don't over qualify class or ID selectors.  Leads to specificity issues further down the line.

		// Bad
		div.content {}

		// Good
		.content {}
- 0 requires no units

		// Good
		.bar,
		.foo[href="bar"] {
			position: absolute;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;

			padding: 10px 0 0 0;
			margin: 10px 0;

			background: red;
			border-radius: 10px;
			-moz-border-radius: 10px;
		}


<a name="section-css-indenting"></a> Indenting
--------------------------------------------

For each level of markup nesting, indent your CSS to match.  For example:

		nav {}
			nav li {}
				nav li a {}

		.content {}
			.content p {}


<a name="section-css-ocss"></a> OOCSS
-------------------------------------

When building components, or modules, try and keep a DRY, OO frame of mind.

Instead of building dozens of unique components, try and spot repeated design patterns and abstract them; build these skeletons as base 'objects' and then peg classes onto these to extend their styling for more unique circumstances.

If you have to build a new component split it into structure and skin; build the structure of the component using very generic classes so that we can reuse that construct and then use more specific classes to skin it up and add design treatments.

Read:
- [The Nav Abstraction](http://csswizardry.com/2011/09/the-nav-abstraction/)


<a name="section-css-typography"></a> Typography
---------------------------------------------


@font-face should be used for font replacement where possible - ensuring that the font can be safely used in .ttf format on the web in agreement with its licensing agreement.  Where this is an issue, look to use tools such as [TypeKit](https://typekit.com/) or [Fontdeck](http://fontdeck.com/)

To generate @font-face files, the [Font Squirrel font-face generator](http://www.fontsquirrel.com/fontface/generator) should be used.

JavaScript replacement techniques should be avoided where possible, as they are painful, time-consuming and usually inaccurate.  Flash replacement techniques (such as Sifr) should never be used.

Always define [supporting font-size classes](http://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css/), in conjunction with headers to avoid restyling header sizes.


<a name="section-css-reset"></a> Reset vs Normalisation
---------------------------------------------------

There is no set preference to using a reset CSS file or using a normalisation technique, as long as consistency is applied throughout projects.

If a reset is preferred, the [Eric Meyer reloaded reset](http://html5doctor.com/html-5-reset-stylesheet/) should be used.

For normalisation, the excellent [normalise.css](http://necolas.github.com/normalize.css/) should be included.

[Kickoff](http://tmwagency.github.io/kickoff/), which is used as a base for all of TMW‘s projects, chooses to implement normalisation by default, rather than a CSS reset.


<a name="section-css-comments"></a> Comments
---------------------------------------------

Comment as much as you can as often as you can. Where it might be useful, include a commented out piece of markup which can help put the current CSS into context.

CSS will be minified before it hits live servers, so don't worry about excessive commenting bloating code - the benefits far outweigh any file-size worries.

This is especially true for responsive layouts where percentage width/margin's have been worked out.  Always comment in the ratio so that the resulting % values mean something to the next developer viewing your CSS.  A random 6dp percentage will mean nothing to anyone else looking at your code.

e.g.

		width: 34.042553% /* 320 / 940 */


<a name="section-css-specificity"></a> Specificity, IDs and classes
----------------------------------------------------------

CSS is designed to cascade, so make sure you understand [cascading and selector specificity](http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html).  It will enable you to write very terse and effective code.

Use of IDs and classes effect specificity massively.  Only use IDs where deemed necessary, especially on larger builds.  Classes are much more modular and portable.  If you want to use an ID solely as a JavaScript hook, consider using the ID alongside a class for CSS styling.

Name classes and IDs by the nature of **what it is** rather than what it looks like. A class of blueBox-left may seem relevant at the time, but should its colour or position change, it will become meaningless.  Naming in conjunction with a more OOCSS approach should eliminate this ambiguity.

**Read:** [Shoot to kill – CSS Selector Intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)


<a name="section-css-conditionalstylesheets"></a> Conditional Stylesheets
------------------------------------------------------------------

Stylesheets specific for Internet Explorer can, by and large, be totally avoided. The only time an IE stylesheet may be required is to circumvent blatant lack of support (e.g. media queries, PNG fixes).

As a general rule, all layout and box-model rules can and will work without an IE stylesheet if you refactor and rework your CSS. This means we never want to see `<!--[if IE 7]> element{ margin-left:-9px; } < ![endif]-->` or other such CSS that is clearly using arbitrary styling to just 'make stuff work'; it will hinder the maintainability of our CSS.

When building mobile first responsive websites, it is necessary to generate a separate stylesheet for old versions of IE to ensure they aren't left with the mobile version of your website because they cannot read media queries.  This can be done using SASS and is covered in the [SASS – IE Stylesheet](#section-sass-mobilefirst) section of this documentation.

If IE specific styling is required, look to utilise Paul Irish's [body/html class conditional for IE* targeting](http://paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/).


<a name="section-css-important"></a> !important
---------------------------------------------

It is okay to use `!important` on helper classes only. To add `!important` pre-emptively is fine, e.g. .error { color:red!important }, as you know you will always want this rule to take precedence.

Using `!important` reactively, e.g. to get yourself out of nasty specificity situations, is not advised. Rework your CSS and try to combat these issues by refactoring your selectors. Keeping selectors short and avoiding IDs will help you out here massively.


<a name="section-css-magicnumbers"></a> Magic numbers and absolutes
-----------------------------------------------------------------

A magic number is a number which is used because ‘it just works’. These are bad because they rarely work for any real reason and are not usually very futureproof or flexible/forgiving. They tend to fix symptoms and not problems.

For example, using .dropdown-nav li:hover ul { top: 37px; } to move a dropdown to the bottom of the nav on hover is bad, as 37px is a magic number. 37px only works here because in this particular scenario the .dropdown-nav happens to be 37px tall.

Instead you should use .dropdown-nav li:hover ul { top: 100%; } which means no matter how tall the .dropdown-nav gets, the dropdown will always sit 100% from the top.

Every time you hard code a number think twice; if you can avoid it by using keywords or ‘aliases’ (i.e. top: 100% to mean ‘all the way from the top’) or—even better—no measurements at all then you probably should.

Every hard-coded measurement you set is a commitment you might not necessarily want to keep.


<a name="section-css-images"></a> Images
---------------------------------------

Image names should use dashes and be named so that their use is clear i.e. icon-facebook-blue.png

It is hard to advise on a one size fits all solution for images currently.  Instead there are a number of methods that should be considered and chosen from when approaching images in CSS.

CSS sprites can be very useful for combining the number of images on your site into a single HTTP request. Sprites work in every browser, although care should be taken when including large sprites on mobile devices as memory limits can be reached when large image files are used.  [Sprite Cow](http://www.spritecow.com/) is a great tool for generating the CSS required for positioning, as is [SpriteMe](http://spriteme.org/) for generating a sprite out of the images used on your site.

Alternatively, converting your images to data URI's and including them in the CSS avoids HTTP requests entirely.  This is however at the expense of older browser support, [namely Internet Explorer 7 and earlier](http://caniuse.com/datauri).

At TMW, we currently use a combination of [GruntIcon](https://github.com/filamentgroup/grunticon), and data-uris, but this is reviewed on a project-by-project basis.


<a name="section-css-debugging"></a> Debugging
----------------------------------------------

If you run into a CSS problem, take code away before you start adding more in a bid to fix it. The problem will exist in the CSS that is already written, more CSS isn't necessarily the right answer!

It can be tempting to put overflow:hidden; on something to hide the effects of a layout quirk, but overflow was probably never the problem; fix the problem, not its symptoms.


<a name="section-css-preprocessors"></a> Preprocessors
---------------------------------------------------

Use of a preprocessor should be used on a per project basis where it is deemed necessary.

Where a preprocessor is used, we shall use [Sass](http://sass-lang.com/).  Kickoff, the TMW base framework, contains a set of Sass base files that should be used.

Be sure to know the ins-and-outs of excellent vanilla CSS and where a preprocessor can aid that, not hinder or undo it. Learn the downsides of preprocessors inside-out and then fuse the best aspects of the two with the bad bits of neither.

For more specific guidelines on using Sass, read the [Sass section of these guidelines](#section-sass).


<a name="section-css-rwd"></a> Responsive Design
----------------------------------------------

All work is considered in a responsive, mobile first, way unless the project dictates otherwise.

Responsive design isn't just a way of developing, it is a way of thinking that needs to flow through the entire site development process from content, UX, design and development.

It is recommended to read Ethan Marcotte's excellent book, [Responsive Web Design](http://www.abookapart.com/products/responsive-web-design) as well as the related [A List Apart article on the subject](http://alistapart.com/article/responsive-web-design/).

It is out of the scope of this document to go through the specifics of developing responsively, but some suggested techniques that we use during development are talked about in [Sass – Mobile First](#section-sass-mobilefirst).


<a name="section-css-tools"></a> Tools
------------------------------------

- [Procssor](http://procssor.com/) - formats untidy CSS into indented loveliness

***

<a name="section-sass"></a> Sass
======================================

<a name="section-sass-general"></a> General Sass Principles
------------------------------------------------------

- Be sure to know the ins-and-outs of excellent vanilla CSS and where a preprocessor can aid that, not hinder or undo it. Learn the downsides of preprocessors inside-out and then fuse the best aspects of the two with the bad bits of neither.
- One of the most powerful features of using a preprocessor is simply being able to separate your CSS into a number of different files that are pulled in and combined at compile time.  This makes it easier to make your code more maintainable and better structured than having all of your code in one file.


<a name="section-sass-nesting"></a> Nesting
-----------------------------------------

When nesting selectors, try not to nest more than 3 levels deep.  If you find yourself writing deeply nested selectors, it is usually a sign that you should rethink how you have structured your markup or class declarations.

Nest only when it would actually be necessary in vanilla CSS, e.g.

		.header {}
		.header .site-nav {}
		.header .site-nav li {}
		.header .site-nav li a {}

Would be wholly unnecessary in normal CSS, so the following would be bad Sass:

		.header {
			.site-nav {
				li {
					a {}
				}
			}
		}

If you were to write this in Sass, it would look more like:

		.header {}
		.site-nav {
			li {}
			a {}
		}

<a name="section-sass-extend"></a> @extend
------------------------------------------

Use caution when using the @extend operator.  It can give unexpected results in the compiled CSS when used too liberally and can usually be avoided by using classes to extend styling in a more modular fashion.

For example, rather than writing the following:

		.section-centered {
			display: block;
			margin: 0 auto;
		}

		.masthead {
			@extends .section-centered;
		}

Simply add the class to the masthead markup instead:

		<div class="masthead section-centered">
			…
		</div>

Doing this will help to keep your styling modular and more reusable.

There are of course times that using @extend can be very useful, but don't use it as a defacto when sensible use of vanilla CSS would be just as simple.


<a name="section-sass-mobilefirst"></a> Mobile first
-----------------------------------------------

In the majority of cases, sites should be built mobile first, specifiying the mobile styles as your base CSS and adding media queries to progressively enhance the experience for larger width devices and screens.

The problem with doing this is that Internet Explorer version 8 and earlier doesn't support media queries and so ignore them and render just the mobile styles.  There is a way of solving this problem using JavaScript, but our preferred solution is to solve the problem using Sass.

[Jake Archibald wrote about this solution](http://jakearchibald.github.io/sass-ie/) which uses Sass to generate two stylesheets – a fixed width stylesheet, which is conditionally loaded for IE8 and below, and a separate stylesheet for all other browsers.  This solution is also built into Kickoff, TMW's frontend framework.

***

<a name="section-js"></a> Javascript
===================================

<a name="section-js-general"></a> General JavaScript Principles
------------------------------------------------------

- 99% of JavaScript should be included in external JavaScript files and included at the END of the BODY tag.  One exception to this rule is [Modernizr](http://modernizr.com/) which should be included at the end of the `<head>`.
- Feature detect, don't browser detect.  [Modernizr](http://modernizr.com/) is a great resource for doing this.
- Name variables and functions logically and in camelCase.  Sensible names that are long are preferred to short names that make no sense.
- Try to write functions to follow the principle that they should do one thing and do it well.  If you can see that a function is becoming more complex, abstract it out into multiple functions – it will become more readable, reusable and will make more sense to someone unfamiliar to the code.
- Prefix jQuery collection variables with the dollar (`$`) character e.g `$headerChildren`
- Class declarations should start with a capital letter.
- Constants or configuration variables should be at the start of a class and written in CAPS.
- Build using the object literal pattern e.g.

		var SiteSetup = {
			init: function () {
				this.$sections = $('#container section');
				this.$additionalTextNodes = $('section a > span');
				this.createMarkup();
			},
			createMarkup: function(){
				var $additionalTextNodes = this.$sections.remove();
				&additionalTextNodes.css({
					position: 'absolute',
					top: this.style.left - $sections[0].style.width / 2
				});
			}
		}
		SiteSetup.init();

- Structure and formatting should follow the example below:

		$(function(){

			var SiteSetup = {
				ANIMATION_SPEED: 100,

				init : function () {
					//fire off all other classes
					if (LightBox.$lightbox.length > 0) {
						LightBox.init();
					}
				}
			},
			LightBox = {
				$lightbox: $('.lightbox'),

				init : function () {},
				open : function () {},
				close : function () {}
			};

			SiteSetup.init();
		});

- Documentation should follow [NaturalDocs](http://www.naturaldocs.org/documenting.html) structure.  As with all code, document as frequently as you can - the more detail the better.  At the very least, document each function you create.

**Read: **
[The Essentials of Writing High Quality JavaScript](http://net.tutsplus.com/tutorials/javascript-ajax/the-essentials-of-writing-high-quality-javascript/)


<a name="section-js-formatting"></a> Formatting and code sensibility
-------------------------------------------------------------

- Separate operators/comparators with spacing

		// Good
		if (foo && foo.bar && typeof foo.bar === 'object') {
			foo.bar.call();
		}

		// Terrible
		if(foo&&foo.bar&&typeof foo.bar==='object'){
			foo.bar.call();
		}

- Use braces for logic evaluations.  If evaluation execution is simple, keep non-braced logic on a single line e.g:

		// Good
		if (i < 10) return true;

		// Good
		if(foo && foo.bar && foo.bar > 10) {
			foo.baz = foo.bar - 100 * 2.7 + 'rad'
		}

		// Bad
		if(foo && foo.bar && foo.bar > 10)
			foo.baz = foo.bar - 100 * 2.7 + 'rad'

		// Bad
		if(i < 10)
			return true;

		// Bad
		if(i < 10)
		{
			return true;
		}

- Remap this to self when passing context
- Always use `===` as a comparator (unless you really need flexible evaluations e.g comparison to null)
- Always add a second radix param to parseInt() to prevent accidental octal issues
- Never bother comparing variables to `true`/`false`
- For large loops, either cache the length variable to prevent re-evaluation or use a reverse while loop
- Don't create functions in loops - its slow (and stupid)
- When creating functions with many parameters, pass in an object rather than listing numerous parameters.
	- use `$.extend` if you are using jQuery to extend a passed in object while providing defaults
- If possible, avoid using bitwise operations unless they really help. If used, document them with comments

		// inverting bits to ease comparison to -1
		if (~foo.bar.indexOf('leetness')){
			alert('w00t!')
		}



<a name="section-js-libraries"></a> Libraries
-----------------------------------------

When considering how we use JavaScript on a project, no two projects are usually the same in how it uses libraries, although the style and inclusion of the libraries is kept as consistent as possible.

Many of our projects are developed using a mix of native JavaScript and [jQuery](http://jquery.com/), although the use of jQuery or simply a native solution is considered at the start of each project.

Kickoff, the TMW frontend framework, includes jQuery as part of it's default build, but this can be easily removed, especially if using the Yeoman generator for Kickoff, which will ask if you would like to include it as part of your project setup.


<a name="section-js-plugins"></a> Plugins
---------------------------------------

We maintain a number of JavaScript classes and plugins we have built and extended across a number of projects.  These can be found on [our github repo](https://github.com/tmwagency/js-classes-and-plugins), the readme of which details our actively maintained projects.

We also maintain an active wiki detailing a number of JavaScript and jQuery plugins we use for common use cases such as form validation, carousels and lightboxes.  Any additions to this must first be added to the experimental list and then approved by at least 2 Members of the team.


<a name="section-js-dependencies"></a> Dependency Management
------------------------------------------------------------

Dependency management and build processing in JavaScript is an area that has progressed rapidly over the last 12-18 months.  Our preferred method of handling dependencies in JavaScript is to use [Browserify](browserify.org), which uses a CommonJS syntax to manage your dependencies.

Although it is encouraged to use browserify on future projects, it is down to the lead developer on each project to choose the solution that best fits their needs.


<a name="section-js-jquery"></a> jQuery Best Practices
-------------------------------------------------

- Always cache DOM selection if you plan to re-use data
- Use efficient query selectors. Write for many browsers, don't assume document.querySelector()
- Avoid using $.each for repeated or performance critical functionality. Instead use a `for` or reverse `while` loop (especially for large objects)
- Use `on()` and `off()` handlers for events.  Everything else is now deprecated (live, delegate, bind)
- When using simple html5 attribute data, simply use `$selected.attr('data-foo')` unless working with complex data types (where you can use `$selected.data()`)
- Try to understand the underlying JavaScript functionality of jQuery methods.  This will help you write much more efficient selectors (watch Paul Irish's talk - [10 Things I Learned from the jQuery Source](http://paulirish.com/2010/10-things-i-learned-from-the-jquery-source/))


<a name="section-js-debugging"></a> Debugging
--------------------------------------------

Learn how to use your browser tools properly as it will save you hours in debugging.

If you're using `alert()` you're doing it wrong.  Use `console.log()`, or [Paul Irish's lightweight wrapper](http://paulirish.com/2009/log-a-lightweight-wrapper-for-consolelog/)


<a name="section-js-resources"></a> Resources
-------------------------------------------

### Forms
- Uniform

### Responsive Carousels
- Flexslider

### Responsive Images
- Adaptive Image

### Mobile touch
- SwiftClick

This list will eventually go on a separate wiki detailing more specific plugin information.

***

<a name="section-accessibility"></a> Accessibility
================================

Markup and code should be written in a way that is inherently accessibile, irrespective of the project being worked on.

When marking up content, ARIA roles are the preferred method of designating the role of sections in our markup when its use may be ambiguous.

For accessibility testing, consider using one of the following:
- [Wave Accessibility tester](http://wave.webaim.org/)


***

<a name="section-performance"></a> Performance and Optimisation
============================================

Performance should be treated as a [constraint on your project](http://timkadlec.com/2013/01/setting-a-performance-budget/).  It is no use making the most beautiful site on the web if noone can be bothered to wait for it to download.

<a name="section-performance-assets"></a> Assets
----------------------------------------------

It isn’t just down to the size of your files, but the number of them.  Each additional request on mobile [increases the latency of your website](https://www.igvita.com/2012/07/19/latency-the-new-web-performance-bottleneck/).

CSS and JavaScript should be concatenated and minified on production servers to minimse their footprint on your website.

Images are a complex subject, especially in the realm of Responsive Design, and is one that is constantly changing.  We recommend checking out [PictureFill](http://scottjehl.github.io/picturefill/) for handling responsive images, as well as reading [Eric Portis' excellent article on the subject](http://alistapart.com/article/responsive-images-in-practice).

For image optimisation, we use:

- [Pngyu](http://nukesaq88.github.io/Pngyu/) – For PNGs
- [JPEGMini](http://www.jpegmini.com/) – For JPEGs


<a name="section-performance-tools"></a> Tools
--------------------------------------------

We recommend running your web pages through one of the following tools to get feedback on the loading and optimsation of your site:

- [Google PageSpeed](https://developers.google.com/speed/pagespeed/)
- [WebPage Test](http://www.webpagetest.org/)
