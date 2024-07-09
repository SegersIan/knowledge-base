# Queue

* A queue the same as an array memory wise, being a continious list in memory.
* A queue however limits us, that we can only delete at the beginning of the array and insert at the end of the array. Therefore, inserts are constant O(1) as we can only insert at the end, but a deletion is always O(N) as we have to move all items in the array one location as we can only delete the first item.
* Reading and searching remain O(N)

Note that we can replace the underlying array structure with linked lists to improve efficiency.

![big-0-2](../assets/big-o-2.png)