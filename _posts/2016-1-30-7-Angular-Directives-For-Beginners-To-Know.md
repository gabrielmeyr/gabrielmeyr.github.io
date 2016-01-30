---
layout: post
title: 7 AngularJS Directives For Beginners To Know
---

Since this post is for Angular beginners, let me clarify one thing about directives up front. When referring to directives in a javascript file, you should do it in camel case, and when using a directive in an html file you should use all lower-case and separate words with dashes.

For example, if you use `ngSrc` in an html file you should write it like this `ng-src`.

Okay, the other thing to know is that Angular comes with a lot of helpful directives baked right in, but there are also lots of 3rd party directives that you can quickly bring in to your own code, sort of like an : libarary. I'll just include one of these third-party directives at the end as an example, the rest will all be included in Angular.

##1. ngModel

This one probably came up for you already in whatever course, book, or blog introduced you to Angular. That's because it is an easy way to demonstrate Angular's two-way data-binding. But in case it didn't, you should learn it now.

The main idea here is that whatever property you define using this directive will store the value of that element on the scope using that property.

You can see an example of how to use it [in the Angular docs](https://docs.angularjs.org/api/ng/directive/ngModel).

##2. ng-repeat

When you have a list of items that are stored on your scope,  you don't always know how many there will be, or it might change over time, so you can't display them using `<li>` HTML tags like you normally would. 

If you throw an ngRepeat tag in a HTML element (like a `li`)

