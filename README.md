<p align="center">
  <img src="https://uikitty.net/wp-content/uploads/2020/09/bootstrap-5-gulp-sasss.png" width="700" alt="Bootstrap 5 with Gulp boilerplate">
</p>

<h3 align="center">Bootstrap 5 starter boilerplate with Gulp</h3>

## Environment for developing web projects on Bootstrap 5 + Gulp + SASS 
A ready-made environment for developing the frontend component of sites and admin interfaces on Bootstrap 5.


## Environment requirements
To create an environment, you must have the following tools installed:
- Node.js
- Git
- Gulp

If you do not have these tools, you need to install them.

## Installing project dependencies
To install project dependencies, enter the commands at the command line:
- `npm install`
- `bower install` (only for version 1.0.0)

## How to use the environment
Normal mode: Enter `gulp` on the command line.
Custom build: Enter the required task at the command line. For example, to build CSS, you must enter the command `css: build`. A list of all available tasks can be viewed in the gulpfile.js file.

___

## More Details

### Tool List
The environment for developing a frontend project (site) is built on the basis of the following tools:

- Node.js (the environment in which the environment will run);
- npm (the package manager included with Node.js; will be used to download Gulp, plugins and frontend packages);
- Popover, Bootstrap 5 (packages that will be used to build css and js parts of the site);
- Gulp and its plugins (will be used to build the project and perform other web tasks).
 
### Gulp project file structure
The project file structure can be organized in different ways. This may depend both on the preferences of a particular developer and on the project for which it is being created.

In this article, we will adhere to the following structure:

The file structure of a Bootstrap 5 project built with Gulp

The "assets" folder and the "gulpfile.js", "package.json" files are located in the root of the project. The gulpfile.js file will contain the tasks for the Gulp project builder.

The first version of the project also used the ".bowerrc" and "bower.json" files. The file "bower.json" is the configuration file for the Bower manager, based on which the frontend packages required for loading were determined. In this project, it was used to load Bootstrap, jQuery and Popper.

There are two folders in the "assets" folder: "src" (for source files) and "build" (for finished files; the Gulp builder will put them in this folder). The "src" folder contains the "fonts" (for fonts), "img" (for source images), "js" (for js-files), "style" (for styles) and "template" (for HTML fragments) directories and the file "index.html".

In the first version of the project, the "src" folder also contained the "bower_components" directory. It was intended for components loaded with Bower. It is not in the current version.

There are two files in the "js" directory: "main.js" and "my.js". The file "my.js" is used to write your scripts, and "main.js" is used to define a list of files, the contents of which will need to be included in the final js file. The final is the file that should be output (in the "build" directory).

The "style" directory is reserved for styles. This directory contains three files: "main.scss" (contains a list of files, the contents of which must be included in the resulting stylesheet), "my.scss" (used to write custom styles) and "variables.scss" (contains SCSS variables, with which we will change the styles of Bootstrap 5, as well as use it to create our variables).

The "index.html" file is the main page of the project being created. Besides "index.html" other html pages can be placed in this directory.

The "template" directory is intended for placing fragments of HTML pages into it. For example, in this directory you can create files "head.html" and "footer.html", and import their contents (using the syntax // = path_to_file) into several pages at once. This will make it easier to create and edit html pages, because separate parts of the pages will already be in separate files.

### Import Bootstrap 5 sources to the project and configuring them

There are different ways to connect the Bootstrap 5 framework to a project, as well as options for working with it.

The most flexible option is to use source codes. In this case, you can not only very easily change the default Bootstrap styles, but also connect to the project only those classes and components that will be used in it.

Bootstrap 5 CSS source codes are written in SCSS language and presented through a large number of small files.

List of SCSS files (located in the "node_modules / bootstrap / scss /" directory): "functions.scss", "variables.scss", "mixins.scss", "variables.scss", "print.scss", "reboot. scss "," type.scss "," images.scss "," code.scss "," grid.scss "," tables.scss "," forms.scss "," buttons.scss "," transitions.scss " , "dropdown.scss", etc.

Each such file either performs a certain service task, or is responsible for styling a certain function of the framework or component. SCSS files have short and meaningful names. Using only them, you can quite accurately understand the purpose of each of them.

Customizing or changing the default Bootstrap 5 styles is done by overriding the values of the SCSS variables. All SCSS variables are collected in one place for convenience (in the "variables.scss" file). But, it is desirable to override their values, of course, not in this file, but in your own (for example, having the same name "variables.scss", but located in "assets / style / variables.scss").

For example, changing the color of the success and danger themes is done by changing the values of the $ green and $ red variables:

```
// Override the default values of Bootstrap 5 variables
$ red: #cc2eaa;
$ green: #2ecc71;
```

Please note that after copying Bootstrap 5 variables into your CSS file ("assets/style/variables.scss"), you need to uncheck them !default.

The SCSS file "assets / style / main.scss" specifies which Bootstrap 5 SCSS source files should and should not be compiled into CSS. In other words, it is the contents of this file that we will define the set of styles that, after compilation, will be connected to the web page.

In addition, the files "assets / style / variables.scss" (for redefining Bootstrap variables) and "assets / style / my.scss" (for creating custom styles) are also connected to this file.

Content of the file "main.scss" (example):

```
// Overriding Bootstrap 5 default variable values and defining your own
@import "variables";

// Connect the SCSS sources of Bootstrap 5
@import "../../../node_modules/bootstrap/scss/_functions";
@import "../../../node_modules/bootstrap/scss/_variables";
@import "../../../node_modules/bootstrap/scss/_mixins";
@import "../../../node_modules/bootstrap/scss/_root";
@import "../../../node_modules/bootstrap/scss/_reboot";
@import "../../../node_modules/bootstrap/scss/_type";
@import "../../../node_modules/bootstrap/scss/_images";
@import "../../../node_modules/bootstrap/scss/_code";
```
In addition, some of Bootstrap 5's components require JavaScript to work.

List of Bootstrap 5 js files (located in the "node_modules/bootstrap/js/dist/" directory): "util.js", "alert.js", "button.js", "carousel.js", "collapse.js "," dropdown.js "," modal.js "," tooltip.js "," popover.js "," scrollspy.js "," tab.js ", and" toast.js ".

Determining which Bootstrap 5 js files need to be included in the final project js file and which not is done through "main.js".

Importing the necessary files into the resulting build / main.js is done using the following construction:

`// = path_to_file`

The Gulp plugin "gulp-rigger" will perform this action. How to install and connect it will be described below.

You can also import Popper into this file (required for Dropdown, Tooltip and Popover components) and, if necessary, your own js files.

The content of the file "main.js" (example):

```
// Import Popper
//= ../../../node_modules/popper.js/dist/umd/popper.js

// Import Bootstrap 5 js-files 
//= ../../../node_modules/bootstrap/js/dist/util.js
//= ../../../node_modules/bootstrap/js/dist/alert.js
//= ../../../node_modules/bootstrap/js/dist/button.js
//= ../../../node_modules/bootstrap/js/dist/carousel.js
//= ../../../node_modules/bootstrap/js/dist/collapse.js
```

Thanks a lot [itchef](https://github.com/itchief) for [article](https://itchief.ru/bootstrap/build-project-with-gulp-v4) and boilerplate with gulp and bootstrap 4!
Bootstrap 5 starter boilerplate with Gulp was made due to the pattern [itchief repository](https://github.com/itchief/gulp-project-bootstrap-4). It was modified and updated to the bootstrap 5. 


