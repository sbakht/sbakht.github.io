---
layout: post
title: "majority element"
date: 2016-03-01 17:06:07
description: leetcode algorithms - easy
---

<pre>
Question:
Given an array of size n, find the majority element. The majority element
 is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always 
exist in the array.
</pre>

#### Approach
The simpliest way to do this one is to loop through the array and keep a hash of the occurences of each value. When incrementing an occurence we can check if it has occured more then half the length of the array. If so, we know its the majority and just return it. Otherwise, continue the loop.

#### Solution
{% highlight javascript %}
var majorityElement = function(nums) {
    if(nums.length == 1) {
        return nums[0];
    }
    var timesToBeMajority = Math.ceil(nums.length / 2);
    var duplicates = [];
    
    for(var i = 0; i < nums.length; i++) {
        if(duplicates[nums[i]]) {
            if(duplicates[nums[i]] + 1 >= timesToBeMajority) {
                return nums[i];
            }
            duplicates[nums[i]] += 1;
        }else{
            duplicates[nums[i]] = 1;
        }
    }
    
};
{% endhighlight %}
