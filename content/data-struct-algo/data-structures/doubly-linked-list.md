# Doubly Linked List

* Part of the node based structures group

* Items in a doubly linked list means, each element of the list exists out of three parts. The first part contains a pointer to the previous item of the list, the second part contains the value and the third part contains the pointer to the next item. If there is no next or previous item, the pointers to these locations will contain a nil.

* The memory doesn't have to find one continous block of memory.

* Inserting will be always O(N) as we have to walk through the entire list to find the final item and then update that item's pointer to the next item.

* Reading and Searching is O(N) as we might have to walk through to the entire list to get to the right memory location.

* Deleting will be O(N) in case at the middle of the list.

* The list keeps track of the first and last item

This is a perfect data structure to create a queue as you have O(1) for inserting at the end and deleting at the beginning.

![big-0-2](../assets/big-o-2.png)