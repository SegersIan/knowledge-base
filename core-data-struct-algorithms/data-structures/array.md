# Array

* An array has often a fixed size.
* Each element in the array has a fixed size, there accessing is constant `O(1)` as we can take the offset memory location and jump straight to the requested item do `offset memory location + (requested index * element memory size)`
* An array is always continious, meaning, if we delete an item, we have to shift all elements after the removed element one memory block. So we have a nice continous array again without empty memory locations. This means adding an element at the beginning of an array means we have to move all elements in the array one memory location further. For this reason adding and deleting can be O(N) in the worst case.
* Searching requires us in the worst case scenario to check every element of the arraym, therefore O(N) for searching.

![big-0-2](../assets/big-o-2.png)