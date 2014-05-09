---
layout: default
title: tree
---

~~~

This VDM++ model contains basic classes for defining 
#******************************************************
~~~
###avl.vdmpp

{% raw %}
~~~
class AVLTree is subclass of Tree
  functions
  tree_isAVLTree : tree -> bool
end AVLTree
~~~{% endraw %}

###bst.vdmpp

{% raw %}
~~~
class BinarySearchTree is subclass of Tree

  functions
    public
  operations
    BinarySearchTree_inv : () ==> bool
    public
       while not curr_node.isEmpty() do
end BinarySearchTree
  values
  v = 1
end BalancedBST
~~~{% endraw %}

###queue.vdmpp

{% raw %}
~~~
class Queue
  instance variables
  operations
    public
    public
    public
end Queue
~~~{% endraw %}

###tree.vdmpp

{% raw %}
~~~

class Tree
  types
    public
    public
  instance variables


  operations
    protected
    protected

    protected
    protected
    protected
    protected
    public
    public
          to_visit.Enqueue(gettree());
          while (not to_visit.isEmpty()) do
    public
    public inorder : () ==> seq of int

end Tree

~~~{% endraw %}

###usetree.vdmpp

{% raw %}
~~~
class UseTree
instance variables
  t1 : BinarySearchTree := new BinarySearchTree();
traces
  insertion_BST : 
end UseTree
~~~{% endraw %}
