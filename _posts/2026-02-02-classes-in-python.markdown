---
layout: post
title:  "Classes in Python"
date:   2026-02-02 10:57:00 +0500
categories: Classes Python OOP 
---
**Huzaifa (learned from Prof. Nauman)**
Many real-world problems can be modeled through classes. Any "object" in the world belongs to a class.
# Modeling Real-World Problems with Classes

Every class has some properties and functions.

## Example of a Class (for understanding)
```python
class Animal():
    leg = False  # member/class variables
    name = ""
    
    def sound(self):  # function
        return "*silence*"
    def move(self):
        return True
```

### Explanation:
- A class is a concept of abstraction. The class written above is just a description of an "Animal".
- We cannot interact directly with this class because it is only a blueprint.
- To interact, we create an instance (or object) of the class.
- Properties like `leg` and `name` are attributes or information about the object.
- Methods like `sound()` and `move()` are functions associated with the class, called methods.
- A class defines behavior but does not perform actions itself.

### Creating an Instance:
```python
a = Animal()
```
- This creates an instance or object of the class `Animal` and assigns it to variable `a`.
- To interact with this instance:
```python
a.legs()
default output: False
```
- When calling `(a.)`, Python looks into the instance for the attribute or method.
```python
type(a)
default output: <class '__main__.Animal'>
```
```python
a.sound
output: "*silence*"
```

## Key Points About `self`
- `self` is a conventionally used first parameter in instance methods within a class.
- It refers to the specific instance of the class — essentially, the object itself.

## Additional Examples:
Recall string methods like join() and split():
```python
s = "a-b-c"
s.split("-")  # returns ['a', 'b', 'c']
default output: ['a', 'b', 'c']
delimiter = ", "
joint_str = ", ".join(['a', 'b', 'c'])  # returns "a, b, c"
default output: "a, b, c"
demonstrates that both join() and split() are methods in the str class.
'text'.split() splits strings,
'text'.join() joins list elements into a string.
```

## Inheritance: Defining Subclasses of Animal (e.g., Dog & Cat)
```python
class Dog(Animal):  # Dog inherits from Animal
    def sound(self):
        return "Bark!"
default output:
d = Dog()
d.sound()
default output: "Bark!"
definition:
d is an instance of Dog which overrides the sound method from Animal.
ewline 
and similarly for Cat:
def class Cat(Animal):
def sound(self):	return "Meow"
c = Cat()
c.sound()
default output: "Meow!" 
note:
the subclass inherits properties/methods from its parent unless overridden.
'that means d.move() will work because move() is inherited from Animal.'}"}] } }'}**>**
