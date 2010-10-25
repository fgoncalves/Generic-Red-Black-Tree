Introduction
============
This implementation of a red black tree suports any kind of object in it. It is a simple implementation and should compile on all systems.

Although this implementation is generic it requires that the objects stored in it be "malloched" before insertion. The reason for such thing lies in the implementation of destroy_rbtree, which frees the stored nodes.

Compilation
===========
Compilation can be done easily with gcc. One example might be gcc -c rbtree.c

If debug info is required you can recompile with -DDEBUG. Note that some times your program may stop or fail due to this rbtree implementation, if so recompile it with -DDEBUG to get the appropriate error messages.

Using it
========
The user must provide two aditional functions.

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

Function description
====================
tree_root* new_simple_rbtree() ::

	   This function creates and returns a rbtree with pointer comparison. The pointers being compared are the addresses of the stored objects.

tree_root* new_rbtree(void* (*key_function_pointer)(struct stree_node* node),
			   int64_t (*compare_function_pointer)(void* keyA, void* keyB)) ::

	   This function creates and returns a rbtree with key and compare functions defined by the user. The first function will be used to return a key and the second function will be used to compare keys.

void* rb_tree_insert(tree_root* root, void* node) ::

      This function inserts a node in the given rbtree. If exists a node with the same key in the tree as the node being stored, then a pointer to the older node is returned. This is done so the user can deallocate the memory. Otherwise NULL will be returned.

void* rb_tree_delete(tree_root* root, void* key) ::

      This function removes from the tree the node with the given key. The returned value is a pointer to that node.

void* search_rbtree(tree_root root, void* key) ::
      
      Duh... search the tree and return the pointer to the founded value. If no node is found then NULL is returned.

void destroy_rbtree(tree_root* root) ::
     
     This function deletes the tree AND the stored values.

tree_iterator* new_tree_iterator(tree_root* root) ::

     Allocate a new iterator to the values stored in the tree.

uint8_t tree_iterator_has_next(tree_iterator* it) ::

	Check if there are values still to be iterated.

void* tree_iterator_next(tree_iterator* it) ::

      Return the next value in the iteration. There is no guarantee about the order of the returned values.

void destroy_iterator(tree_iterator* it) ::

     Destroy the given iterator.
