# Insertion Sort

* Algorithm
  * In the first passthrough, we temporarily remove the value at index 1 and store in a temporary variable. This will leave a gap at that index, since it contains no value. In subsequent passthroughs we remove the values at the subsequent indexes.
  * We then begin a shifting phase, where we take each value to the left of the gap, and compare it to the value in the temporary variable. If the valie to the left of the gap is greater than the temporary variable, we shift it to the right, AS we shift values to the right, inherently, the gap moves leftwares. As soon as we encounter a value that is lower than the temporarily removed value, or we reach the left of the array, this shifting phase is over.
  * We hten insert the temporary removed value in the current gap.
  * We repeat steps 1 through 3 untill the array is fully sorted.

A beter analogy is:
* You have a pack of cards, layed out from left to right, beside each other.
* You start with the card on index one and push it up in an empty row above.
* Now we have a gap in the row of cards.
* Move each card on the left of the gap in the gap, as long the cards are bigger than the card you pushed above.
* Then move the card that was pushed a row above into the empty gap.
* Now start the same over but from index 2 till all cards are fully sorted.