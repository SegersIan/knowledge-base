# Bubble Sort

* Algorithm
  * Set pointers to first two cells
  * Compare, swap if second cell's value is smaller than the first cells' value
  * Move the pointers one cell to the right and repeat process till end of array.
  * At end of going through the array, remember to ignore next passthrough the last item as we're positive it's the highest value
  * Now we start with the pointers to first two cells, and repeast the process, only we stop earlier as we know on each passthrough the last items are ordered.

* After every passthrough we can safely asume the last item is the highest item is at the end.
* On second passthrough we can asume the last two items don't need to be checked any more, and so forth.

* Efficiency O(N2) (quadratic)
