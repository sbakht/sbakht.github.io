---
layout: post
title: "excel sheet column number"
date: 2016-03-01 15:32:16
description: leetcode algorithms - easy
---

<pre>
Question:
Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding 
column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
</pre>

#### Approach
A good way to go about this is to write out some examples. There are already some examples, but we should write out some for 3 char length like `AAA`. Then we can try to see if there is some algorithm to calculate them. Once we come up with an algorithm, writing the code should be a lot easier.

<pre>
A : 1
B : 2
Z : 26
AA :27 - > 1 + 1*26
AB :28 - > 2 + 1*26
BA :53 - > 1 + 2*26
BB :54 - > 2 + 2*26
ZA :677 -> 1 + 26*26
ZZ :702 -> 26 + 26*26
AAA : 703 -> 1 + 27*26 - > 1 + 1*26 + 1*26*26
</pre>

It took me a while to realize that you just have to use `26^x` to get the values. Using the above data we can derive a function to calculate the number for any cell location. We start at the least significant char and multiply its int value by `26^x` where `x = the ith position in the char starting from the right`.

We can loop through the string going backwards just adding to the sum and incrementing the power on each loop. We create a string to store the alphabet so we can convert single characters to their int value.

#### Solution
{% highlight javascript %}
var titleToNumber = function(s) {
    var alphabet = "|ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    var sum = 0;
    var power = 0;
    for(var i = s.length - 1; i >= 0; i--) {
        sum += alphabet.indexOf(s[i]) * Math.pow(26,power);
        power++;
    }
    return sum;
};
{% endhighlight %}
