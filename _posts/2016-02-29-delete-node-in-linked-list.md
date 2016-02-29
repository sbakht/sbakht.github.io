---
layout: post
title: "delete node in a linked list"
date: 2016-02-29 08:51:30
description: leetcode algorithms - easy
---

<pre>
Write a function to delete a node (except the tail) in a singly linked list, 
given only access to that node.

Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node
 with value 3, the linked list should become 1 -> 2 -> 4 after calling your 
 function.
</pre>

#### Approach
The usual technique to deleting a node in a linked list is to skip over the node we are skipping by `previousNode.next = previousNode.next.next`. This allows us to skip over
the node that needs to be removed, effectively deleting it. In garbage collected languages, the node would then be deleted since it no longer has any references.

We can't use this technique because we don't have access to the previous node. We only have access to the node that needs to be deleted. This means we can't remove the actual node from the linked list. Our only other option is to replace the value of the node.

All we have to do is set the nodes' value to the next nodes' value, then skip over that next node since we essentially duplicated it.

<pre>
Let's remove 3 from 1 -> 2 -> 3 -> 4
1. Replace the 3 with the next node value
1 -> 2 -> 4 -> 4
2. Skip over the next value
1 -> 2-> 4 -> null
</pre>

This methods will work for removing any node that isn't the tail since the question ignores the tail. This method won't work for the tail since we have to set the deleting node value to the next value, but there is no next node if we are deleting the tail.

#### Solution
{% highlight javascript %}
var deleteNode = function(node) {
    node.val = node.next.val;
    node.next = node.next.next;
};
{% endhighlight %}
