# SCSS Intro

This is a repo for my SCSS intro course I am taking from Udemy.
https://www.udemy.com/sasscourse/learn/v4/t/lecture/4455760?start=0

I just want to track my commits and learning progress here.

# Environment Setup

1. Install [Sublime Text](https://www.sublimetext.com)
2. install [Package Control](https://packagecontrol.io) for Sublime Text
3. Install Sass via Package Control
4. Install SCSS via Package Control
5. Install Sass Build via Package Build***
6. Install [Emmet](http://emmet.io) via Package Control for code completion
7. Install Ruby via Terminal
8. Install Sass via Terminal
9. Set your Build System as Sass: Tools -> Build System -> Sass

*** Alternatively, follow the Sass website's instructions by running this snippet in Terminal in your project's directory:

    sass --watch style.scss:style.css --style compact --no-cache

replacing 'style.scss' and 'style.css' with whatever file names you want to use. Anyway, you save a step in that you don't need to hit Cmd/Ctrl + B to rebuild your CSS files when you change your SCSS files.

# Test out your environment setup

Create a `style.scss` file with the following simple syntax, using a nested `p` element only usable in SCSS, not CSS:

    body {
	background-color: #eee;
	color: #800;

        p {
            color: #008;
        }
    }
    
If running `sass --watch`, watch sass process this automatically into a valid CSS file!

If building from Sublime Text, press Ctrl/Cmd + B!

## Change Build System to put CSS files in CSS folder

1. Go to Tools -> Build System -> New Build System...
2. Paste this in:

	{

	  "cmd": ["sass", "--update", "$file:${file_path}/../css/${file_base_name}.css", "--stop-on-error", "--no-cache"],

	  "osx":
	  {
	      "path": "/usr/local/bin:$PATH"
	  },

	  "windows":
	  {
	      "shell": "true"
	  }

	}

3. Save as `Build to CSS Directory.sublime-build`
4. Select Tools -> Build System -> Build to CSS Directory
5. Create `css` and `scss` directories
6. Move test `style.scss` file to `scss` folder
7. Press Cmd + B

Voila!

## Build CSS files on Save

1. Go to Package Control -> Install Package -> SublimeBuildOnSave
2. To ignore partials, go to Preferences -> Package Settings -> SublimeBuildOnSave -> User settings
3. Add this:
		{
		    "filename_filter": "(/|\\\\|^)(?!_)(\\w+)\\.(css|js|sass|less|scss)$",
		    "build_on_save": 1
		}

# Building Partials

1. Name a new `.scss` file with prepender underscore '_'. This tells preprocessor not to make a CSS file out of this. 
2. Add your variables to the file!

# Code Conventions

- Use variables especially for values that are used more than once.
- Also just for readability and easy maintenance.
- variable names are all lower-case, separating words within a var by a dash (e.g., `$hello-world`)
- Use Partials to separate variables by category and from the rest of your styles.
- Use Mixins for blocks of reusable styles.

# Functions

## Built-in

- rgb(x,y,x) = red, green, blue
- hsl(x,y,z) = hue saturation, light
- darken(x,y) = color, % to darken
- lighten(x,y) = color, % to lighten
- transparentize(x, y,) = color, 0-1 (like 0% to 100%)
- opacify(x, y) = color, 0-1 (like 0% to 100%)

## Custom

Put in a `partials` file, e.g., `_functions.scss`.
- [Strip Unit](https://css-tricks.com/snippets/sass/strip-unit-function/)

# Directives

## `@extend` vs `@mixin` + `@include`

Under the hood, `@include` from `@mixin` copies style properties to specified selectors. This means you have the same amount of selectors but lots of duplicated properties.

On the other hand, `@extend` copies selectors to be added to specified selector definitions. This means you potentially have duplicate selectors but not duplicated properties.

So objectively, you will typically have a bigger CSS file in the end with `@mixin`s compared to `@extend`. 

However, if you [gzip](https://varvy.com/pagespeed/enable-compression.html) your CSS (which you always should), it's been found that performance is still better with `@mixin` because gzip automatically strips out duplicated properties. This is why many people actually exclusively use `@mixin` and avoid using `@extend` completely.

belly: [mixins vs. extends](https://tech.bellycard.com/blog/sass-mixins-vs-extends-the-data/)

## `@extend` quirks

	.cta-button {
		
		// This won't work; can't use multiple selectors
		// @extend .hello .world;
	}

	@media screen {
		.foo {
			color: red;
		}
		.super-cta-button {
			// This won't work because .cta-button is defined outside media query
			//@extend .cta-button;

			// This WILL work
			@extend .foo;
			font-size: em(20px);
		}
	}


## `@if`, `@else if`, and `@else`

	$contrast: hello; // results in @else
	// $contrast: high -- results in #000
	// $contrast: low -- results in #999

	body {
	  font-family: $text-font;
	  @include large-screens {
	    font-size: em(18px);
	  }
	  @if $contrast == high {
	  	color: #000;
	  } @else if $contrast == low {
	  	color: #999;
	  } @else {
	  	color: $text-color;
	  }

	}

This kind of stuff is great to use for multiple themes of a stylesheet, e.g., "Light", "Dark", "Default", "ClientX", "ClientY", "Ocean".

## Loops

### `@for`

	// from 1 to 6 is exclusive 6
	@for $i from 1 through 6 {
		.col-#{$i} {
			width: $i * 2em;
		}
	}

Generates this CSS:

	.col-1 {
	  width: 2em; }

	.col-2 {
	  width: 4em; }

	.col-3 {
	  width: 6em; }

	.col-4 {
	  width: 8em; }

	.col-5 {
	  width: 10em; }

	.col-6 {
	  width: 12em; }

### `@each`

	
	@each $speaker in $speakers {
		.#{$speaker}-profile {
			background-image: url('/img/#{$speaker}.png');
		}
	}

Generates this CSS:

	.bob-banker-profile {
	  background-image: url("/img/bob-banker.png"); }

	.patty-plume-profile {
	  background-image: url("/img/patty-plume.png"); }

	.sandra-smith-profile {
	  background-image: url("/img/sandra-smith.png"); }

#### With a Map

	$font-sizes: (tiny: 8px, small: 11px, medium: 13px, large: 18px);

	@each $name, $size in $font-sizes {
		.#{$name} {
			font-size: $size;
		}
	}

Generates this CSS:

	.tiny {
	  font-size: 8px; }

	.small {
	  font-size: 11px; }

	.medium {
	  font-size: 13px; }

	.large {
	  font-size: 18px; }

# Popular Sass Frameworks/Toolkits

- [Susy](http://susy.oddbird.net/) toolkits - flexible, highly customizable, lets you create your own grids
- [Breakpoint](http://breakpoint-sass.com/) tool - helps you identify and handle breakpoints in responsive design
- [Compass](http://compass-style.org/) - framework