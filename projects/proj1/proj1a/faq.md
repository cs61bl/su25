---
# layout: page
# title: "FAQ - Project 1A"
# nav_order: 1
# parent: >-
#   Project 1A: LinkedListDeque
# grand_parent: "Project 1: Deques"
# has_children: false
# has_toc: false
# has_right_toc: true
# description: >-
#   Project 1 FAQ.
# released: true

# layout: page
# title: "FAQ - Project 1A"
# nav_order: 4
# parent: >-
#   Project 1A: LinkedListDeque
# grand_parent: "Project 1: Deques"
# has_children: false
# has_toc: false
# has_right_toc: true
# description: >-
#   Project 1 FAQ.
# released: true

layout: page
title: "FAQ - Project 1A"
nav_order: 4
parent: >-
  Project 1A: LinkedListDeque
grand_parent: "Project 1: Deques"
has_children: false
has_toc: false
has_right_toc: true
description: >-
  Project 1 FAQ.
released: true
---

##### I'm getting a "Required Type is Deque but provided is ..."

There are two possible issues. Make sure you haven't accidentally imported java.util.* (or java.util.LinkedList or
java.util.ArrayList). The other possible issue comes with an issue in your class signature.

##### Intellij is telling me "The method ... of type LinkedListDeque has the same erasure as ... of type Deque but does not override it."

You probably forgot the generic `T` in the implements line of your class signature (i.e. you wrote
`implements Deque` instead of `implements Deque<T>`). If you used something other than `T` for your generic type
parameter, use that instead.

##### Q: How do I make my arrows point to particular fields of a data structure?

In your diagram from lecture it looked like the arrows were able to point to the middle of an array or at specific
fields of a node.

A: Any time I drew an arrow in class that pointed at an object, the pointer was to the ENTIRE object, not a particular
field of an object. In fact it is impossible for a reference to point to the fields of an object in Java.

##### Q: What does OOB stand for?

Out of bounds.

##### Q: My tests pass locally but Gradescope is telling me "NullPointerException: Cannot invoke java.lang.Iterable.iterator() because this.actual is null"

This may be caused by returning null in your `toList` method. Make sure that toList always returns an `ArrayList`, even if the Deque is empty.
