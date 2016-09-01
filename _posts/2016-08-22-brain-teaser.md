---
title: "Brainteaser questions"
description: ""
category: datascience
tags: []
---



### Table of contents

* TOC
{:toc}


# How to detect a loop in a linked list?

## Motivation
A singly linked list is a common data structure familiar to all computer scientists. A singly linked list is made of nodes where each node has a pointer to the next node (or null to end the list). A singly linked list is often used as a stack (or last in first out queue (LIFO)) because adding a new first element, removing the existing first element, and examining the first element are very fast O(1) operations.

When working with singly linked list, you are typically given a link to the first node. Common operations on a singly linked list are iterating through all the nodes, adding to the list, or deleting from the list. Algorithms for these operations generally require a well formed linked list. That is a linked list without loops or cycles in it.


If a linked list has a cycle:

![{{base}}/images/other/linked_list.jpg]({{base}}/images/other/linked_list.jpg)

[image source](http://i.stack.imgur.com/irw1S.jpg)

The malformed linked list has no end (no node ever has a null next_node pointer)
The malformed linked list contains two links to some node
Iterating through the malformed linked list will yield all nodes in the loop multiple times
A malformed linked list with a loop causes iteration over the list to fail because the iteration will never reach the end of the list. Therefore, it is desirable to be able to detect that a linked list is malformed before trying an iteration. This article is a discussion of various algorithms to detect a loop in a singly linked list.

([source](http://blog.ostermiller.org/find-loop-singly-linked-list),[source](http://stackoverflow.com/questions/2663115/how-to-detect-a-loop-in-a-linked-list))


## Solution

You can make use of Floyd's cycle-finding algorithm, also know as tortoise and hare algorithm.

The idea is to have two references to the list and move them at different speeds. Move one forward by 1 node and the other by 2 nodes.

If the linked list has a loop they will definitely meet.
Else either of the two references(or their next) will become null.
Java function implementing the algorithm:

```Java

boolean hasLoop(Node first) {

    if(first == null) // list does not exist..so no loop either.
        return false;

    Node slow, fast; // create two references.

    slow = fast = first; // make both refer to the start of the list.

    while(true) {

        slow = slow.next;          // 1 hop.

        if(fast.next != null)
            fast = fast.next.next; // 2 hops.
        else
            return false;          // next node null => no loop.

        if(slow == null || fast == null) // if either hits null..no loop.
            return false;

        if(slow == fast) // if the two ever meet...we must have a loop.
            return true;
    }
}
```

# String Programming Interview Questions

String is the primary and probably most common thing you come across on any programming language and so is with any programming interview. There is almost always a question on String whether its related to length or replace but I have always find one or two String programming questions on interviews.


## Write code to check a String is palindrome or not?
Palindrome are those String whose reverse is equal to original.This can be done by using either StringBuffer reverse() method or by technique demonstrated in the solution here.


## Write a method which will remove any given character from a String?
hint : you can remove a given character from String by converting it into character array and then using substring() method for removing them from output string.


## Print all permutation of String both iterative and Recursive way?


## Write a function to find out longest palindrome in a given string?


## How to find first non repeated character of a given String?


## How to count occurrence of a given character in a String?


## How to check if two String are Anagram?


## How to convert numeric String to int in Java?


# Some more String related Questions which mostly appear in Java programming interviews: 

## What is difference between String, StringBuilder and StringBuffer in Java? (answer)
Main difference is that String is immutable but both StringBuilder and StringBuffer are mutable. Also StringBuilder is not synchronized like StringBuffer and that's why faster and should be used for temporary String manipulation.


## Why String is final in Java? (answer)
String is final because of same reason it is immutable. Couple of reasons which I think make sense is implementation of String pool, Security, and Performance. Java designers knows that String will be used heavily in every single Java program, so they optimized it from the start.

## How to Split String in Java? (answer)
Java API provides several convenient methods to split string based upon any delimiter e.g. comma, semi colon or colon. You can even use regular expression to split a big string into several smaller strings.

## Why Char array is preferred over String for storing password? (answer)



# Programming questions on Array

Array is one of the topics where most of programming questions is asked. There are many and many programming questions on Array and here I have included only some of them which is not very difficult to solve but some of array programming question can be extremely challenging, so well prepare this topic.

## In an array 1-100 numbers are stored, one number is missing how do you find it?


## In an array 1-100 exactly one number is duplicate how do you find it?


## In an array 1-100 multiple numbers are duplicates, how do you find it? 
One trick in this programming questions is by using HashMap or Hashtable , we can store number as key and its occurrence as value, if number is already present in Hashtable then increment its value or insert value as 1 and later on print all those numbers whose values are more than one.


## Given two arrays, 1,2,3,4,5 and 2,3,1,0,5 find which number is not present in the second array.
Here is a quick tip to solve this programming question: put the elements of the second array in the Hashtable and for every element of the first array, check whether it’s present in the hash or not, O/P all those elements from the first array that are not present in the hash table


## How do you find second highest number in an integer array?


## How to find all pairs in array of integers whose sum is equal to given number?


## How to remove duplicate elements from array in Java?


## How to find largest and smallest number in array?


## How to find top two maximum number in array?


# LinkedList Programming Interview Questions

## How do you find middle element of a linked list in single pass?
To answer this programming question I would say you start with simple solution on which you traverse the LinkedList until you find the tail of linked list where it points to null to find the length of linked list and then reiterating till middle. After this answer interviewer will ask you find the middle element in single pass and there you can explain that by doing space-time trade-off you can use two pointers one incrementing one step at a time and other incrementing two step a time, so when first pointer reaches end of linked second pointer will point to the middle element.



## How do you find 3rd element from last in single pass?
This programming question is similar to above and can be solved by using 2 pointers, start second pointer when first pointer reaches third place.


## How do you find if there is any loop in singly linked list? How do you find the start of the loop?
This programming question can also be solved using 2 pointers and if you increase one pointer one step at a time and other as two steps at a time they will meet in some point if there is a loop.


## How do you reverse a singly linked list?


## Difference between linked list and array data structure?

# Binary Tree Programming Interview Questions

Binary tree or simply tree is one of favorite topic for most of interviewer and pose real challenge if you struggle with recursion. Programming questions on tree can become increasingly difficult when you think iterative but sometime can be very easy if you come with recursive solution.


## How do you find depth of binary tree?


## Write code to print InOrder traversal of a tree?


## Print out all leaf node of a binary tree?


## Write a method in Java to check if a tree is a binary search tree or not?


## How to check if a tree is balanced or not in Java?



# Programming Questions on Searching and Sorting

I have only included two programming questions related to searching and sorting but there are more can be finding on Google. Purpose of these programming questions is to see whether programmer is familiar with essential search and sort mechanism or not.


## Write a program to sort numbers in place using quick sort?


## Write a program to implement binary search algorithm in Java or C++?


## How do you sort Java object using Comparator?
This is another Java specific programming questions and you can check how to sort Object using Comparator and Comparable for answer. 

## Write code to implement Insertion Sort in Java?


## Write code to implement Bubble Sort in Java?


# Programming Questions on Numbers

Most of the programming questions are based on numbers and these are the ones which most of us did on college level and mind you they still has value I have seen programmers with experience of 3 years struggle with these programming questions and doesn't solve it some time and take a lot of time which simply shows that they are not in programming in there day to day work.


## Write code to check whether a no is power of two or not?


## Write a program to check whether a number is palindrome or not?
Check out this post which shows how to reverse number in Java and can be used to find if its palindrome or not.


## Write code to check whether an integer is Armstrong number or not? 
Here is a Java program to find Armstrong number, you can use same logic to write code in any other programming language like C and C++.


## Write a program to find all prime number up to a given numbers? 
Here is another Java program to find prime numbers and print them. By using logic demonstrated in this program; you can write similar program in C and C++.


## Write function to compute Nth Fibonacci number? Both iterative and recursive?
Check this Java program to print Fibonacci Series using recursion and iteration. 


## How to check if a number is binary?
For this question, you need to write a function which will accept an integer and return true if it contains only 0 and 1 e.g. if input is 123 then your function will return false, for 101 it should return true.

##  How to reverse an integer in Java?


## How to count number of set bits in given integer?


## How to find sum of digits of a number using recursion?


## How to swap two numbers without using temp variable?


## How to find largest of three integers in Java?


## Write a program to find prime factors of integer?


## How to add two integer without using arithmetic operator?


# General Programming Interview Questions

In this category of programming questions I have put questions which are not fit into any data structure but presents a real life problem and you need to provide solution. These programming questions are sometime based on problems faced by developer itself. I have not included many Software design related programming question which I have shared on Top 20 software design questions and answers; you can also check that. 



## Write a program to find out if two rectangles R1 and R2 are overlapping?


## You need to write a function to climb n steps you can climb either 1 step at a time or 2 steps a time, write a function to return number of ways to climb a ladder with n step.


## Write code for Generate Random No in a range from min to max?


## Write program for word-wrap which should work on any screen size?


## Design an algorithm to find the frequency of occurrence of a word in an article?


## Write a program to implement blocking queue in Java?


## Write a program for producer-consumer problem?
This article solves producer consumer problem using BlockingQueue in Java. You can refer it to answer this question.


Read more: http://javarevisited.blogspot.com/2011/06/top-programming-interview-questions.html#ixzz4I9v9UcCC

