---
layout: post
title:  "Class templates (generics)"
author: "discreetso (M.Huzaifa)"
date:   2026-02-25 10:58:00 +0500
categories: Classes class templates generics OOP 
---

**Class templates** is one of the widely used and important concept in the mordern programming. In Java and most of the other languages, it is called **generics**. In python, there are no templates because it itself detects datatypes.

```c
/* class template of LIFO to make it usable for other data types */
#include <iostream>
#include <string>
using namespace std;

template <class T>
class List {
  struct node {
    T val;
    node *next;
  };

  node *head, *last;
  void delete_after_node(node *current);

public:
  List();
  void push(T val);
  T pop();
  void print_list();
};

template <class T>
List<T>::List() {
  head = last = NULL;
}

template <class T>
void List<T>::push(T val) {
  node *temp = new node;
  temp->val = val;
  temp->next = NULL;

  if(last == NULL) {      //need this when list is empty
    head = temp;
    last = temp;
  } else {                //for all other cases
    last->next = temp;
    last = last->next;
  }
}

template <class T>
T List<T>::pop() {
  T val;
  if(head->next == NULL) {
    val = last->val;    //saving val for later use
    delete head;        //deleting head

    head = NULL;        //nothing left in list now
    last = NULL;
  } else {              //for all other cases
    val = last->val;    //saving val for later use
    node *current = head;

    while(current->next != last) {
      current = current->next;
    }

    //node current is just before last, so delete last
    delete_after_node(current);
    last = current;
  }
  return val;         //now return the value we send later
}

template <class T>
void List<T>::delete_after_node(node *current) {
  node *temp = current->next;
  current->next = current->next->next;
  delete temp;
}

template <class T>
void List<T>::print_list() {
  node *current = head;

  cout << "[ ";
  while (current != NULL) {
    cout << current->val << " ";
    current = current->next;
  }
  cout << "]" << endl;
}

int main() {
  List<int> l;
  l.push(5);
  l.push(15);
  l.push(21);
  l.pop();
  l.print_list();
}
```