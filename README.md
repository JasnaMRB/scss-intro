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