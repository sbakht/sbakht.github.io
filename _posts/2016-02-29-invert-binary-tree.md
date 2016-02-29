---
layout: post
title: "invert binary tree"
date: 2016-02-29 14:11:33
description: leetcode algorithms - easy
---

<pre>
Invert a binary tree.

     4
   /   \
  2     7
 / \   / \
1   3 6   9

to

     4
   /   \
  7     2
 / \   / \
9   6 3   1
</pre>

#### Approach
This problem isn't that bad if you notice that the left and right children of each node are reversed at each level. First the root's children are reversed, then it goes to those children and reverses their children, and so on.

Therefore we can just use a Depth-First Search and rotate the children at each node we encounter. This can be done easily with recursion by reversing on each recursive call, then calling the function again with its children. We return the root at the end and in the base case since we want the top level root to be returned in the end.

#### Solution
{% highlight javascript %}
var invertTree = function(root) {
    if(root === null) {
        return root;
    }
    
    var temp = root.left;
    root.left = root.right;
    root.right = temp;
    
    invertTree(root.left);
    invertTree(root.right);
    return root;
};
{% endhighlight %}


