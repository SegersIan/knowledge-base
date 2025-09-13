# Hash Table

* Used for fast reading
* Also known as associative arrays
* Use a deterministic hash function
* Under the good a hash stores data in a bunch of cells in a row, similar to an array.
* When a key is provided, this key is hashed, this hash will return a memory location within the row of cells.
* Collisions can happen with the hash function, a classic solutions is "separate chainging". What we do is instead of placing a value in the cell, we puts a reference to an array in it. That array will hold a subarray for each element. So once it founds a hash location with an array, it will do a sequential lookup within that array. e.g. `[[key1, value1],[key2, value2]]`
* Efficiency if a hash table is based on
  * How much data we're storing in the hash table
  * How man cells are available in the hash table
  * Which hash function we're using

* Result is that Search/Insert/Delete is O(1) average and worst 0(N) in case everything ends up in one array referenced in one cell.

![big-0-2](../assets/big-o-2.png)