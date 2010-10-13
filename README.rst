Using it
========
This implementation of a red black tree suports any kind of object in it. For this reason, the user must provide two aditional functions.

The first one should have the following signature:

void* function_name(struct stree_node* node);

This function should return the key used in the red black tree. For example, if one is creating a red black tree of integers and the value stored in the tree is the address of each integer, this function should return node->node.

The second function should have the following signature:

uint64_t function_name(void* keyA, void* keyB);

This function should compare the two keys and return:

* 0 if the keys are the same.

* A number less than 0 if the keys are in the right order.

* A number bigger than 0 if the keys are not in the right order.

Note that these functions should be passed to the new_rbtree function. However, if a simple address comparison fits your needs then you should call new_simple_rbtree(), which automatically will create the comparison and key functions for you.

Further explanation will be given in a nearby future.