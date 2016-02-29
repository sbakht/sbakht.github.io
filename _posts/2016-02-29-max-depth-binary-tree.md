---
layout: post
title: "maximum depth of binary tree"
date: 2016-02-29 00:20:12
description: leetcode algorithms - easy
---

<pre>
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path 
from the root node down to the farthest leaf node.
</pre>

#### Recursive Approach
I'm not too good at recursion myself, so my explanation won't be very good. So we can do recursion when a problem is made up of the same sub problems. This works really
well in binary trees since each tree is comprised of smaller trees. 

Therefore the depth of any tree, is the depth its child tree + 1. Our base case would return 0 when the node is null since you can't increment by 1 since there is no node.
Since we are trying to find the max depth, we should only increment the max of the left and right subtree.

#### Solution
{% highlight javascript %}
var maxDepth = function(root) {
    if(root === null) {
        return 0;
    }
    var left = maxDepth(root.left);
    var right = maxDepth(root.right);
    return 1 + Math.max(left,right);
};
{% endhighlight %}
