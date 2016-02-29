---
layout: post
title: "move zeros"
date: 2016-02-29 14:32:47
description: leetcode algorithms - easy
---

<pre>
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, `nums` should be [1, 3, 12, 0, 0].

Note:
    1. You must do this **in-place** without making a copy of the array.
    2. Minimize the total number of operations.
</pre>

#### Approach
Since this has to be done in **in-place** our only choice is to rotate the values. We can use 2 pointers `i` and `j` where `i < j`. Pretty much we are trying to find the first `0`, then reverse it with the next instance of a `non 0`. We just repeat this, finding the subsequent `0` and reversing with the next `non 0` until one of our pointers is greater then `nums.length`. At that point all the `0's` would be at the end of the array.

Lets show an example for `nums = [0,1,0,3,12]`.
<pre>
i = 0, j = 1
[0, 1, 0, 3, 12] //nums[i] is 0 and nums[j] != 0 so we reverse them and increment i

i = 1, j = 1
[1, 0, 0, 3, 12] //now we increment j until nums[j] != 0

i = i, j = 3
[1, 0, 0, 3, 12] //now we reverse and increment i

i = 2, j = 3
[1, 3, 0, 0, 12] //increment j until nums[j] != 0

i = 2, j = 4
[1, 3, 0, 0, 12] //reverse and increment i

i = 3, j = 4
[1, 3, 12, 0, 0] //increment j until nums[j] != 0

//j = 5 > nums.length so we break
</pre>

Now we just have to translate this to code. One thing to notice is that when `nums[i] != 0` we increment both `i` and `j` so `i <= j` is always true.

#### Solution
{% highlight javascript %}
var moveZeroes = function(nums) {
    var i = 0, j = 1;
    while(j < nums.length) {
        if(nums[i] === 0) {
            if(nums[j] !== 0) {
                nums[i] = nums[j];
                nums[j] = 0;
                i++;
            }else{
                j++;
            }
        }else{
            i++;
            j++;
        }
    }
};
{% endhighlight %}
