---
layout: post
title: Coin Sums Problem -- Simple JavaScript Solution
---
The coin sum problem seems to be something that people in various programming languages try to tackle. The idea is that you have a money system with various coins all worth a different amount. Write a function that will tell you how many combinations of coins are possible that will result in a given total.

The version of the problem I solved in JavaScript involves the money system in Great Britain which has coins with the following value: 1p, 2p, 5p, 10p, 20p, 50p, £1 (100p) and £2 (200p). The 'p' stands for 'pence'.(This scenario is also [problem #31 in Project Euler](https://projecteuler.net/problem=31).)

I am going to describe in detail the "brute force" solution you will see if you google the problem. There is also an elegant (yet hard to follow) solution that I'm not going to address here. Google it if you're curious.

##What Didn't Work
The first thing I thought was that this requires a decision tree, so I thought I'd make a variation of the backtracking algorithm I used to solve the 'N Queens' problem. See [this link](http://www.geeksforgeeks.org/backtracking-set-3-n-queen-problem/) for a good example of that. I spent SO MANY HOURS working out that solution that it would have been great to get some more mileage out of it.

I wanted to add a coin, then check and see if we were at or over the desired total, and if above then remove the coin and try the next coin. And so on through all the possible permutations. But the logic was tough to make work. Beware infinite loops if you try this approach. That's if you get it to run at all.
##A Model To Follow
After working on this for a few hours and still being pretty lost, I blurred my eyes and peeked at [an online solution](http://www.mathblog.dk/project-euler-31-combinations-english-currency-denominations/). That told me I needed to make a bunch of nested for loops representing a test for each kind of currency.

I didn't look refer back to the example solution again though as I tried to apply the idea for myself. Eventually I ironed out all the specifics.

One thing to note here is that instead of starting with a coin sum of zero, in this approach we delete the value of coins from the target number until we reach zero.

First declare your solution variable and lay out nested for loops that subtract the value of each coin, in order of most valuable coin to least. After all the loops, increment your solution count, because your loops have finished contributing coin values that get you from the total down to zero.

Also make sure each for loop has a new var to iterate with so that the loops can work independently within each other instead of messing with each other's place.

```
var coinSums = function(target){
  var solutions = 0;
  for(var a = total; ? ; a-200){
    for(var b = a ; ? ; b-100){
      for(var c = b; ? ; c-50){
        for(var d = c; ? ; d-20){
          for(var e = d; ? ; e-10){
            for(var f = e; ? ; f-5){
              for(var g = f; ? ; g-2){
                for(var h = g; ? ; h-=1){
                  solutions++;
                }
              }
            }
          }
        }
      }
    }
  }
  return solutions;
};
```

See how each for loop takes the starting value of its var from the current value of the iterator immediately preceding it (example: _var b = a_)? That means that if we have already taken 200 from the total and var a is now equal to 1, then var b is starting with that current value of a also and we maintain our progress toward zero.

So if our target is 250, a starts out as being equal to 250. Then after our a loop runs, a is now equal to just 50 and our b loop starts out with b equal to 50.
##Between The Apostrophes
The next question is, what is the condition that should cause each loop to stop. My first thought was that we let loops run while the var was above 0.  If we do that, we find that the function runs, it just finds _too many_ solutions.

```
var coinSums = function(target){
  var solutions = 0;
  for(var a = total; a > 0 ; a-200){
    for(var b = a ; b > 0 ; b-100){
      for(var c = b; c > 0 ; c-50){
        for(var d = c; d > 0 ; d-20){
          for(var e = d; e > 0 ; e-10){
            for(var f = e; f > 0 ; f-5){
              for(var g = f; g > 0 ; g-2){
                for(var h = g; h > 0 ; h-=1){
                  solutions++;
                }
              }
            }
          }
        }
      }
    }
  }
  return solutions;
};
```


That's happening because we are counting it as a solution every time we add a penny, not just when we add the final penny in a combination. So let's wrap our solution iterator in an if statement that checks if our total is down to zero, an indication that we have added the final coin (whether it was a penny or a previous coin).

```
var coinSums = function(target){
  var solutions = 0;
  for(var a = total; a > 0 ; a-200){
    for(var b = a ; b > 0 ; b-100){
      for(var c = b; c > 0 ; c-50){
        for(var d = c; d > 0 ; d-20){
          for(var e = d; e > 0 ; e-10){
            for(var f = e; f > 0 ; f-5){
              for(var g = f; g > 0 ; g-2){
                for(var h = g; h > 0 ; h-=1){
                  if(h === 0){
                    solutions++;
                  }
                }
              }
            }
          }
        }
      }
    }
  }
  return solutions;
};
```

##Wait A Second...
Okay, that makes sense. But now our function is actually not finding <em>any </em>solutions.

This is because we are only iterating when we reach zero, but our for loops aren't allowed to keep going if our running total is zero or lower. Let's change it so that they allow zero values for the iterator.

```
var coinSums = function(total){
  solutions = 0;
  for(var a = total; a > -1; a-=200){
    for(var b = a ; b > -1; b-=100){
      for(var c = b; c > -1; c-=50){
        for(var d = c; d > -1; d-=20){
          for(var e = d; e > -1; e-=10){
            for(var f = e; f > -1; f-=5){
              for(var g = f; g > -1; g-=2){
                for(var h = g; h > -1; h-=1){
                  if(h === 0){
                    solutions++;
                  }
                }
              }
            }
          }
        }
      }
    }
  }
  return solutions;
};
```

And that's -- we're done! Our solution may not be the prettiest out there, but it works. It finds 1 solution if you are trying to make change for 1p, and 25 solutions if you are trying to make change for 17p. Now when do we get to visit Great Britain!

Way to hang in there through this thing. One of these days I'll try to makes sense of and explain the more elegant solution.
##Woo!