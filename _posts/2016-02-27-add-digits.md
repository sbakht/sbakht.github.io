---
layout: post
title: "add digits"
date: 2016-02-27 23:08:41
description: leetcode algorithms - Easy
---

<pre>
Question:
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

Follow up:
Could you do it without any loop/recursion in O(1) runtime?
</pre>

#### Approach
So to do this we need to be able to access each digit of a number. This can be done using the `modulus` operator. Lets take the example of 138.

`138 % 10 = 8` which is the last digit. To access the 3, we can then divide by 10 and use `Math.floor()` to get rid of decimals. Then we just repeat the `n % 10` until `n = 0`.
<pre>
138 % 10 = 8
138 / 10 = 13.8 // Math.floor(13.8) = 13
13  % 10 = 3
13 / 10 = 1.3 // Math.floor(1.3) = 1
1 % 10 = 1
1 / 10 = .1 // Math.floor(.1) = 0
</pre>
While doing this we keep a running sum of each `modulus`.  There are situations where the resulting sum has the same amount of digits as the original number, such as with 99. 

`9 + 9 = 18` which is still 2 digits long. In this case we can't just use a single while loop to run while n > 0. We have a to create a temp variable to hold the sum then set `n = sum` when `sum > 9`.

#### Solution
{% highlight javascript %}
var addDigits = function(num) {
    var temp;
    while(num > 9) {
        temp = num;
        num = 0;
        while(temp > 0) {
            num += temp % 10;
            temp = Math.floor(temp / 10);
        }
    }  
    return num;
};
{% endhighlight %}

#### Alternate Solution
We can simply the solution by knowing a trick with adding digits.
<pre>
addDigits(9) - > 9
addDigits(18) -> 9
addDigits(27) - > 9
addDigits(36) -> 9
</pre>

We can see a pattern that all multiples of 9 will have a result of 9. This means the answer is simply `n % 9` when n isn't a multiple of 9.

Take this for example:
<pre>
addDigits(17) - > 8
17 is one less than a multiple of 9, making the result 9 - 1 = 8

addDigits(19) - > 1
1 + 9 = 10
1 + 0 = 1
Being 1 greater then a multiple of 9 wraps it around back to 1
</pre>

{% highlight javascript %}
var addDigits = function(num) {
    if(num === 0) {
        return 0;
    }
    return num % 9 || 9;
};
{% endhighlight %}
