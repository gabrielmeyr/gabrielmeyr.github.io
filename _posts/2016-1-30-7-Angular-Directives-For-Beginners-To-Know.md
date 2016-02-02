---
layout: post
title: 7 Angular Directives For Beginners To Know
---


Since this post is for Angular beginners, let me clarify one thing about directives up front. When referring to directives in a javascript file, you should do it in camel case, and when using a directive in an html file you should use all lower-case and separate words with dashes.

For example, if you use `ngSrc` in an html file you should write it like this `ng-src`.

Okay, the other thing to know is that Angular comes with a lot of helpful directives baked right in, but there are also lots of 3rd party directives that you can quickly bring in to your own code, sort of like an : libarary. All of these examples will be normal Angular directives baked right  into the framework, though.

##1. ngModel

This one probably came up for you already in whatever course, book, or blog introduced you to Angular. That's because it is an easy way to demonstrate Angular's two-way data-binding. But in case it didn't, you should learn it now.

The main idea here is that whatever property you define using this directive will store the value of that element on the scope using that property.

This can be demonstrated without a JavaScript file at all. Here's a simple example using HTML:

<script src="https://gist.github.com/GMeyr/a9e50718702549118ad8.js"></script>

As you type into the input field, ngModel would print the text to the screen above it. The data is also available on the scope to your JavaScript files under the variable name $scope.myInput.

##2. ngRepeat

When you have a list of items that are stored on your scope,  you don't always know how many there will be, or it might change over time, so you can't display them using `<li>` HTML tags like you normally would. 

If you throw an ngRepeat tag in a HTML element (like a `li`), it will automatically create the right number of items to fit your data.

The value of the ngRepeat attribute is similar to the way a for loop is used on objects. To loop through the array stored on the $scope as 'stooges', I tell ngRepeat to loop through each 'name in stooges'. I could say 'person in stooges' or 'stooge in stooges' because the first word is just the name we are going to use as the iterating variable.

Then within the repeated HTML we refer to the current item in the list by the name of our iterating variable, which in this case, is 'name'.

Here's an example of using ngRepeat a `<tbody>` tag to repeat rows in a table:

<script src="https://gist.github.com/GMeyr/33765a6687a77d3937a2.js"></script>

<script src="https://gist.github.com/GMeyr/9f69a6ae7739f98a656c.js"></script>

This will print the following on the screen:

Curly
Moe
Larry

If you have objects stored in an array instead of strings, you can access the properties on each object using dot notation. You can see an example of this when you get down to #5.


##3. ngShow

This tags are very useful for displaying and removing things on the DOM based on some condition. Point ngHide to a boolean value on the $scope, or a function call or expression that evaluates to a boolean value.

If that value is true, then the element will be shown on the DOM. If it is false, the element will be hidden. (This is different from ngIf, which actually removes and destroys the element and it's scope, instead of simply hiding it.)

Here an example that uses ngShow to implement a help button. If users had trouble with the answer to this math problem. They could click the 'Help!' button and a bit of text would appear below with a hint.

<script src="https://gist.github.com/GMeyr/a54d4b38be4fcf218d1c.js"></script>

<script src="https://gist.github.com/GMeyr/324c55f2e1b7febc80ef.js"></script>

If you had a button that changed the value of $scope.helpMessage back to false, then the help message would be hidden again.

You can also use the directive ngHide if you want to show/hide elements using the opposite boolean values.

##4. ngSubmit

ngSubmit is pretty simple, but also pretty handy. Normally submitting an HTML form triggers a POST request with the input data. ngSubmit prevents that default action and instead calls a function to do whatever you want with the input data.

<script src="https://gist.github.com/GMeyr/c10ded67c1ff0b7d1688.js"></script>

<script src="https://gist.github.com/GMeyr/ddec397969c02c5b8a9c.js"></script>

If I typed in 'koala' in the input field there and clicked submit, an alert would pop up saying 'Your favorite animal is a koala' and no POST request would be triggered.

If you want this kind of power when someone click a button that doesn't involve  a form, use the ngClick directive instead.

##5. ngClass

ngClass allows you to use an expression to determine what class (or classes) will be assigned to an element. We're going to look at how to use an expression that returns a string to provide a class. You can use this directive to assign class using arrays and objects ([see the documentation here](https://docs.angularjs.org/api/ng/directive/ngClass)). We're going to keep it simple for now, though.

Say I want to display the names of puppies and kittens in a list. I don't want to label them as puppy or kitten though, I just want the names of puppies to be in blue and the names of kittens to be in red.

To do this, I'll create two classes in my stylesheet, puppy and kitten, and use ngClass to automatically assign the right class to each list item.

Notice that this example also uses ngRepeat, which we went over earlier.

<script src="https://gist.github.com/GMeyr/19e088d7f4d7c242c570.js"></script>

<script src="https://gist.github.com/GMeyr/fea056da453cda4dd41e.js"></script>

<script src="https://gist.github.com/GMeyr/6d8567e201a843d1548b.js"></script>



