---
layout: post
title: "Arrays vs. Linked Lists"
date: 2013-04-22 12:27
comments: true
categories: [Flatiron School, Interview Prep, Ruby, Arrays, Linked Lists]
---

Today at Flatiron School we started researching common Computer Science questions we might be asked during interviews. A common topic is the difference between Arrays and Linked Lists. I've used arrays lots of times in coding, but I had no idea what a linked list is. Below is a summary about what the differences between the two and their common use cases.

Both Arrays and Linked Lists are used to store linear data of similar types. Depending on your application or requirement, you may elect to pick one over the other.

<!-- more -->

## Arrays

**What's an Array?**

- Typically arrays are denoted in bracket notation. 

<!-- code example -->
    fav_nums = [10, 27, 12]
    fav_colors = ["yellow", "red", "orange", "green"]

- Array size is allocated when it's declared. 

<!-- code example -->
    fav_nums.size # => returns 3
    fav_colors.size # => returns 4

**Advantages:**

- A common use case for arrays is frequent searching.

<!-- code example -->
    fav_nums[0] # => returns 10
    fav_colors[3] # => returns "green"

**Disadvantages:**

- Array size is often fixed and specified at compile time. If you allocate arrays large in size in anticipation of data needs, you're allocating arrays with wasted space and may potentially crash.
- Inserting new elements or deleting existing elements at the front of an array is potentially expensive because existing elements need to be shifted or unshifted to make room. 
- If you have trouble remembering the difference between shift and unshift... just take out the f and think about what they do. Got that handy tip from stackoverflow!

##Linked Lists

**What's a Linked List?**

- The structure of Linked Lists consist of nodes. Think of nodes like the links in a chain.
- Each node contains 2 fields: a data field (the actual stored value) and reference field (which points to which element is next aka the "link"). 
- The references or pointers in nodes are what connect all of the nodes together.

**Pros:**

- Linked Lists may be sized dynamically. If your application requires dynamically sized lists, you'll want to use a Linked List.
- Use Linked Lists if your application requires frequent insertion or deletion of elements at a specific location.

**Why?**

- Memory is allocated differently for Linked Lists than Arrays. 
- Arrays lump one block of memory for all of its elements. 
- Linked Lists allocate space for each element separately in its own block of memory called a "node" or a "linked list element." 

**What else?**

- It's easier to store data of different sizes in a linked list. An array assumes every element is exactly the same size.
- As you mentioned, it's easier for a linked list to grow organically. An array's size needs to be known ahead of time, or re-created when it needs to grow.
- Shuffling a linked list is just a matter of changing what points to what. Shuffling an array is more complicated and/or takes more memory.
- As long as your iterations all happen in a "foreach" context, you don't lose any performance in iteration.

**Resources:**

- Super detailed explanation of [Linked Lists by the CS department at Stanford](http://cslibrary.stanford.edu/103/LinkedListBasics.pdf)
- Good ole [Wikipedia's Linked List entry](http://en.wikipedia.org/wiki/Linked_list)
- Ruby doesn't have Linked Lists. Hashes are similar to Linked Lists in that they have references (keys) and values, but they're not the same. Here's how someone wrote [a Linked List in Ruby](http://khakimov.com/blog/2012/05/11/back-to-school-linked-list-with-ruby/).
- Listened to [Solange's True EP](http://prettymuchamazing.com/music/stream/solange-true-ep) and the new [Daft Punk "Get Lucky" track](http://www.youtube.com/watch?v=5NV6Rdv1a3I) while writing this blog post