---
title: "Arrays: Two Pointer"
date: 2022-12-08T06:45:24-06:00
draft: false
tags: ['arrays', 'algorithms', 'software']
---

Today I learned about the two pointer technique for solving interesting array problems. The pointers can move in the same direction, opposite directions or a fixed width:

```sh
# same direction
 2*>      1*>
[ ][ ][ ][ ][ ][ ]...

# opposite directions
# (towards each other)
    1*>     <2*
[ ][ ][ ][ ][ ][ ]...
# (away from each other)
      <1*    2*>
[ ][ ][ ][ ][ ][ ]...

# fixed window 
# (of 4 in this example)
    |1*----2*|
[ ][ ][ ][ ][ ][ ]...
```
The two pointer technique can be used to perform a search with one pointer and an action with a second pointer. It could be used to keep track of history. It could be used for reversing an array. Etc.

The two pointer technique is a useful tool to have in our arrays toolbox.
