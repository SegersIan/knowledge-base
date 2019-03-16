# Quick Sort

* Recursive algorithm

* We use partitioning, which means to take a random value form the array, this will be called the `pivot`. So we take this pivot and make sure every number that is less than the pivot ens up on the left, and every number larger ends up on the right of the pivot.

* So first to partition the list:
  * The left pointer continiously moves one cell to the right until it reaches a value that is greater than or equal to the pivot and then stops.
  * Then the right pointer continiously moves one cell to the left until it reaches a value that is less than or equal to the pivot and then stops.
  * We swap the values that the left and right pointers are pointing to.
  * We continue this process until the pointers are pointing to the very same value or the left pointer has moved to the right of the right pointer.
  * Finally, we swap the pivot with the value that the left pointer is currently pointing to.

Now we now that all the values on the left of the pivot or smaller and all the values of the pivot larger.

* The Algorithm
  * Do the partition, having the pivot in its proper place
  * Treat the subarrays to the left and right of the pivot as their own arrays, and recursively repeat the previous step and this step. That means that we'll partition each subarray, and end ip with even smaller subarrays to the left and the right of each subarrays pivot. We then partition those subarrays and so forth.
  * When we have a subarray that has zero or one elements, that is our base case and we do nothing.

Efficiency is O(N log N)