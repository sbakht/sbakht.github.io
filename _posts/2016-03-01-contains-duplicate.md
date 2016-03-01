---
layout: post
title: "contains duplicate"
date: 2016-03-01 16:53:55
description: leetcode algorithms - easy
---
<pre>
Question:
Given an array of integers, find if the array contains any duplicates. 
Your function should return true if any value appears at least twice in 
the array, and it should return false if every element is distinct.
</pre>

#### Approach
This one is pretty straightforward. Just loop through the array and store the value in a hash. If the value is already in the hash, you `return true`. `return false` if it makes it through the loop

#### Solution
{% highlight javascript %}
var containsDuplicate = function(nums) {
    var duplicates = {};
    for(var i = 0; i < nums.length; i++) {
        if(duplicates[nums[i]]) {
            return true;
        }else{
            duplicates[nums[i]] = 1;
        }
    }
    return false;
};
{% endhighlight %}
