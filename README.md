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
