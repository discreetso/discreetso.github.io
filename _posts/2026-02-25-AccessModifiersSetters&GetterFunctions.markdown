---
layout: post
title:  "Access Modifiers, setters and getters"
author: "discreetso (M.Huzaifa)"
date:   2026-02-25 10:47:00 +0500
categories: Classes Access Modifiers setters getters OOP 
---
Whenever we have a member/field of a class, which can have some constraints. We make those members hidden and access it through the methods, which can contain logic called setters and getters.  
A **setter function** is a function that sets the value of a hidden variable for us.  
A **getter function** is a function that gets the value for us.

```c
//Setters and getters functions

#include <iostream>
#include <string>
using namespace std;

class Employee {
  int pay_rate;

public:
  Employee();

  void set_pay_rate(int pay_rate);
  int get_pay_rate();
};

Employee::Employee() {
  pay_rate = 14;
}

void Employee::set_pay_rate(int pay_rate) {
  if(pay_rate > 14) {
    this->pay_rate = pay_rate;
  } else {
    cout << "Pay rate " << pay_rate << " not acceptable, not setting ..." << endl;
  }
}

int Employee::get_pay_rate() {
  return pay_rate;
}

int main() {
  Employee a;
  // a.pay_rate = 15;

  cout << "Constructor initialized value: " << a.get_pay_rate() << endl;

  a.set_pay_rate(15);
  cout << "Pay rate: " << a.get_pay_rate() << endl;
  a.set_pay_rate(13);

}
```

## Access modifiers
To achieve **Encapsulation** or **Data hiding**, we make use of access modifiers. Access modifiers are three:
- **private** means just this class.
- **protected** means this class and it's children.
- **public** means everybody.

```c
//Access modifiers or Access specifiers: public, private and protected

#include <iostream>
#include <string>
using namespace std;

class Employee {
protected:
  int pay_rate;

public:
  Employee();

  void set_pay_rate(int pay_rate);
  int get_pay_rate();
};

Employee::Employee() {
  pay_rate = 14;
}

void Employee::set_pay_rate(int pay_rate) {
  if(pay_rate > 14) {
    this->pay_rate = pay_rate;
  } else {
    cout << "Pay rate " << pay_rate << " not acceptable, not setting ..." << endl;
  }
}

int Employee::get_pay_rate() {
  return pay_rate;
}

//child class FacultyMember
class FacultyMember: public Employee {
public:
  FacultyMember();
  void set_pay_rate(int pay_rate);
};

FacultyMember::FacultyMember() {
  pay_rate = 25;
}

void FacultyMember::set_pay_rate(int pay_rate) {
  if(pay_rate > 25) {
      } else {
    this->pay_rate = pay_rate;
    cout << "Pay rate " << pay_rate << " not acceptable, not setting ..." << endl;
  }
}

int main() {
  // Employee a;
  // // a.pay_rate = 15;
  //
  // cout << "Constructor initialized value: " << a.get_pay_rate() << endl;
  //
  // a.set_pay_rate(15);
  // cout << "Pay rate: " << a.get_pay_rate() << endl;
  // a.set_pay_rate(13);

  FacultyMember fm;

  fm.set_pay_rate(26);
  cout << "Pay rate: " << fm.get_pay_rate() << endl;
  fm.set_pay_rate(23);
}
```