---
layout: post
title: 7 Angular Directives For Beginners To Know
---


Since this post is for Angular beginners, let me clarify one thing about directives up front. When referring to directives in a javascript file, you should do it in camel case, and when using a directive in an html file you should use all lower-case and separate words with dashes.

For example, if you use `ngSrc` in an html file you should write it like this `ng-src`.

Okay, the other thing to know is that Angular comes with a lot of helpful directives baked right in, but there are also lots of 3rd party directives that you can quickly bring in to your own code, sort of like an : libarary. I'll just include one of these third-party directives at the end as an example, the rest will all be included in Angular.

##1. ngModel

This one probably came up for you already in whatever course, book, or blog introduced you to Angular. That's because it is an easy way to demonstrate Angular's two-way data-binding. But in case it didn't, you should learn it now.

The main idea here is that whatever property you define using this directive will store the value of that element on the scope using that property.

This can be demonstrated without a JavaScript file at all. Here's a simple example using HTML:

<script src="https://gist.github.com/GMeyr/a9e50718702549118ad8.js"></script>

As you type into the input field, ngModel would print the text to the screen above it. The data is also available on the scope to your JavaScript files under the variable name $scope.myInput.

##2. ngRepeat

When you have a list of items that are stored on your scope,  you don't always know how many there will be, or it might change over time, so you can't display them using `<li>` HTML tags like you normally would. 

If you throw an ngRepeat tag in a HTML element (like a `li`), it will automatically create the right number of items to fit your data.

Here's an example of using ngRepeat a `<tbody>` tag to repeat rows in a table:

<script src="https://gist.github.com/GMeyr/33765a6687a77d3937a2.js"></script>

<script src="https://gist.github.com/GMeyr/9f69a6ae7739f98a656c.js"></script>

This will print the following on the screen:

Curly
Moe
Larry

##3. ngShow

This tags are very useful for displaying and removing things on the DOM based on some condition. Point ngHide to a boolean value on the $scope, or a function call or expression that evaluates to a boolean value.

If that value is true, then the element will be shown on the DOM. If it is false, the element will be hidden. (This is different from ngIf, which actually removes and destroys the element and it's scope, instead of simply hiding it.)

Here an example that uses ngShow to implement a help button. If users had trouble with the answer to this math problem. They could click the 'Help!' button and a bit of text would appear below with a hint.

<script src="https://gist.github.com/GMeyr/a54d4b38be4fcf218d1c.js"></script>

<script src="https://gist.github.com/GMeyr/324c55f2e1b7febc80ef.js"></script>

If you had a button that changed the value of $scope.helpMessage back to false, then the help message would be hidden again.

You can also use the directive ngHide if you want to show/hide elements using the opposite boolean values.


