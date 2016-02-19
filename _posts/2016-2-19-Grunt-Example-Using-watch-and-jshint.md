---
layout: post
title: Grunt Example Using watch and jshint
---
This post will help you create a basic file that lets you run Grunt, and also show you how to make Grunt watch your files and automatically run jshint on when you change them.

The three main sections of a Gruntfile are:

1. configure task settings
2. declare dependencies
3. register tasknames

So run `npm install grunt` in your project's root directory using the terminal, and let's move on to step 1.

## Step 1: Make a Gruntfile

You need a file called Gruntfile.js in your root directory to run Grunt. You can have Grunt walk through the creation of a file with you (kind of like how `npm init` will interactively help you create a package.json file). You would type `grunt init:gruntfile` in your terminal to do that. But we're going to make our own Gruntfile to show you how easy the basics are and keep some clutter out.

You can see an example of the complete file at the end of this post.

So make a new file in your root directory called Gruntfile.js. Start out by putting this code into it:

```
module.exports = function(grunt) {
  grunt.initConfig({});

  grunt.loadNpmTasks();

  grunt.registerTask('default', []);
};
```

Before we do anything with these three function calls, take a look at the structure. Pretty much all Gruntfiles follow this basic skeleton structure:

1. Set the configuration of each task
2. Load the source file for that task
3. Tell Grunt what command should run the task

## Step 2. The Structure

initConfig takes an object literal as a parameter, and each task you want to set up will be a property with its own object literal. Like this:

```
module.exports = function(grunt) {
  grunt.initConfig({
    jshint: {
      files: [
      'Gruntfile.js',
        'src/*.js'
      ],
    }

    watch: { //watch does not need to be registered as a task
      files: [
        '<%= jshint.files %>'
      ],
      tasks: ['jshint']
    }
  });

  grunt.loadNpmTasks();

  grunt.registerTask('default', []);
};
```

The specific settings for the jshint configuration are easy (and there are variations -- check the docs). We just made jshint a property and assigned it an object with its own property called files. As you might have guessed, in here we put references to all the files we want jshint to check.

I'm just going to two files in that array -- the first is a reference to my Gruntfile, and the second is a special syntax that says to Grunt, "Check everything in my src folder that ends in js.

Now we'll add in our configuration for the watch task as another property. The specific settings for 'watch' are easy to see from this example or by reading the docs:

```
module.exports = function(grunt) {
  grunt.initConfig({
    jshint: {
      files: [
      'Gruntfile.js',
        'src/*.js'
      ],
    },
    watch: { //watch does not need to be registered as a task
      files: [
        '<%= jshint.files %>'
      ],
      tasks: ['jshint']
    }
  });

  grunt.loadNpmTasks();

  grunt.registerTask('default', []);
};
```

In the files array of the watch task, we could have specified specific files. But since we already did that when we set up jshint, we can just refer to those files using this template notation `<%= ... =>`. The advantage there is if you want to change the files jshint runs on, you only need to do it in one place, and the watch task will still be up to date.

## Step 2: Dependencies
Whether in the browser or in Node.js, many of us are probably used to declaring our dependencies at the top of a file. I'm not sure why in Grunt it's typical to declare them in the middle of the file, but that's how they do it in the [Grunt documentation](http://gruntjs.com/sample-gruntfile), so we're going to stick with that approach. (The file will still work if you move them to the top, if you're curious.)

We use the `.loadNpmTasks` method to load dependencies. You to do this for most tasks you want to set up in Grunt.

If you're wondering what the name of the package is for a given task, just google the taskname and 'grunt'. Usually the right docs are at the top for major packages.

```
module.exports = function(grunt) {
  grunt.initConfig({
    jshint: {
      files: [
      'Gruntfile.js',
        'src/*.js'
      ],
    },
    watch: { //watch does not need to be registered as a task
      files: [
        '<%= jshint.files %>'
      ],
      tasks: ['jshint']
    }
  });

  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-contrib-watch');

  grunt.registerTask('default', []);
};
```

Now, these files we're depending on don't just appear out of thin air -- be sure to use npm to install them in your root directory. Like `npm install 'grunt-contrib-watch'`.

##Step 3. Register and Run Tasks

Now we tell Grunt what to do for its default task.

`grunt.registerTask('default', ['jshint']);

This means when you type `grunt` into the command line in the root directory for this folder, Grunt will run the 'jshint' task. You can add other tasks you have created to that array also.

If you want, you can also register other things like a 'test' task that would run when you type `grunt test` in the command line. The default task is special because you only need to type `grunt` to run it. For other tasks, the command is `grunt [taskname]`.

You're done with the file! Now let's run it. (Be sure you've closed the `module.exports` function at the end of your file with a `};`).

Go to the command line and type 'grunt' from your root directory of the project. It will run jshint on your files. (If it doesn't, make sure you don't have any typos in your Gruntfile and that you npm installed the dependencies.)

And for something even more exciting, type `grunt watch` in the command line. Now go change something in one of your watched files, save it, and presto! It runs jshint automatically. Pretty cool, especially considering you can have the watch task fun more than just jshint.

## Example of complete Gruntfile
<script src="https://gist.github.com/GMeyr/ba2c6a1afb47e8f188d5.js"></script>


