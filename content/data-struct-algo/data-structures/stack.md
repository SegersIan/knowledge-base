# Stack

* A stack the same as an array memory wise, being a continious list in memory.
* A stack however limits us, that we are only allowed to insert and delete at the end of our array. So we cannot add or remove in the middle or to the beginning of the array, which makes our insertions and deletions fast. As we can always immediatly jump to the end of the array and there are no trailing elements that need to be moved around to respect the continuity of our array. Therefore inserts and deletions are constant O(1). 
* Searching and access remain O(N) as it's still is an continious list of elements in memory.

Note that we can replace the underlying array structure with linked lists to improve efficiency.

![big-0-2](../assets/big-o-2.png)