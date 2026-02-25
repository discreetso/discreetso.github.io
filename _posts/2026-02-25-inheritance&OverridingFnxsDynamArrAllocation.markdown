---
layout: post
title:  "Inheritance & Overriding functions, Dynamic Array allocation"
author: "discreetso (M.Huzaifa)"
date:   2026-02-25 10:45:00 +0500
categories: Classes Inheritance Overring functions OOP Dynamic array allocation 
---
Inheritance establishes an is-a relationship between a parent and a child. For example, a **Triangle**  is-a **Shape**. 

**Shape**  
 the parent, also called a superclass, parent class, base class.  
 **Triangle**  
 the child, also called a subclass or derived class.

```c
#include <iostream>
#include <string>
using namespace std;

class Point {
public:
  int x;
  int y;
  void print_points();
};

void Point::print_points() {
  cout << "(" << x << " , " << y << ")" << endl;
}

/* xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx */

class Shape {
public:
  int num_points;
  Point *points;
  Shape();
  void set_points(Point *p);
  float get_area();
  void show_shape();
};

Shape::Shape() {
  cout << "In shape constructor ..." << endl;
  points = NULL;      //initialize
  num_points = 0;
  //do nothing. Can't decide what "shape" is ...
}

void Shape::set_points(Point *p) {
  points = p;
}

float Shape::get_area() {
  //again, can't do anything
  return -1.0;
}

void Shape::show_shape() {
  Point *temp;
  temp = points;
  for(int i = 0; i < num_points; i += 1) {
    temp->print_points();
    temp++;
  }
}

/* xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx */

//let's inherit this Shape class
class Triangle: public Shape {
public:
  Triangle();
  float get_area();       //"overriding the function"
};

Triangle::Triangle() {
  cout << "In Triangle constructor ..." << endl;
  num_points = 3;
}

float Triangle::get_area() {
  int x0, y0, x1, y1, x2, y2;
  Point *t = points;
  x0 = t->x;    y0 = t->y;    t++;
  x1 = t->x;    y1 = t->y;    t++;
  x2 = t->x;    y2 = t->y;

  //formaula for computing area...don't have to understand
  return abs(x0 * (y1 - y2) + x1 * (y2 - y0) + x2 * (y0 - y1) / 2);
}

void create_shape() {
  Triangle *t;
  t = new Triangle;

  Point p1, p2, p3;
  p1.x = p1.y = 0;
  p2.x = p2.y = 10;
  p3.x = p3.y = 25;

  // dynamic array aloocation
  Point *points_of_triangle = new Point[3];    
  points_of_triangle[0] = p1;
  points_of_triangle[1] = p2;
  points_of_triangle[2] = p3;

  t->set_points(points_of_triangle);
  t->show_shape();
  cout << "Area of Triangle: " << t->get_area() << endl;
}

int main() {
  create_shape();

  return 0;
}
```