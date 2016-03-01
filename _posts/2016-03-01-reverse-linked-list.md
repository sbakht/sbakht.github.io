---
layout: post
title: "reverse linked list"
date: 2016-03-01 17:13:22
description: leetcode algorithms - easy
---

<pre>
Question:
Reverse a singly linked list.
</pre>

#### Approach
A property of a linked list is that you can prepend to the head in `O(1)`. With this we can just prepend to the head each node as we traverse the linked list.

We have to remember to create a temp variable to hold the current value so we don't break the original linked list when setting the value's next to be the new linked list's old head.

#### Solution
{% highlight javascript %}
var reverseList = function(head) {
    if(head === null || head.next === null) {
        return head;
    }
    var curr = head;
    var temp = head;
    var newHead = null;
    while(curr !== null) {
        temp = curr;
        curr = temp.next;
        temp.next = newHead;
        newHead = temp;
    }
    return newHead;
};
{% endhighlight %}
