---
layout: post
title: "valid anagram"
date: 2016-02-29 19:04:56
image: '/assets/img/'
description: leetcode algorithms - easy
---

<pre>
Problem:
Given two strings s and t, write a function to determine if t is an anagram
 of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your
 solution to such case?
</pre>

#### Approach
We would first want to check if their lengths are the same and `return false` if they aren't. Then we loop through the first string and create a hash with values being the char element at each index. This way can store how many of each char there are by incrementing the value in the hash when we come across the same char.

Then we can loop through the 2nd string, subtracting from the hash key values when we come across a char that was in the first string. We `return false` if `hash[key] < 0` meaning there are more of the same char in the 2nd string then the first string. We also return false if a char doesn't appear in the hash. 

If it goes the loop succesfully, then we know they are anagrams and can `return true`. All the values in the hash would be `0`.

#### Solution
{% highlight javascript %}
var isAnagram = function(s, t) {
    var hash = {};
    if(s.length !== t.length) {
        return false;
    }
    
    for(var i = 0; i < s.length; i++) {
        hash[s[i]] = (hash[s[i]] || 0) + 1;
    }
    for(var i = 0; i < t.length; i++) {
        if(hash[t[i]]) {
            hash[t[i]] -= 1;
        }else{
            return false;
        }
    }
    return true;
};
{% endhighlight %}
