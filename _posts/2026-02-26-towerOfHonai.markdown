---
layout: post
title:  "Tower of Honai and the real power of abstraction"
author: "discreetso (M.Huzaifa)"
date:   2026-02-26 09:08:00 +0500
categories: Classes recursion abstraction tower Honai OOP 
---

The **Tower of Honai** and the real power of abstraction


```c
#include <iostream>
using namespace std;

void print_move(int disk, char from_rod, char to_rod){
	cout << "Move disk " << disk << " from " << from_rod << " to rod " << to_rod << endl;
}

void move_disk(int n, char from_rod, char to_rod, char aux_rod) {
	if(n == 1) {
		// just the smallest disk. Can be moved anywhere
		print_move(n, from_rod, to_rod);
		return;
	}
	
	// move all-minus-largest from FROM to AUX (using to as extra)
	move_disk(n-1, from_rod, aux_rod, to_rod);
	
	//move largest disk
	print_move(n, from_rod, to_rod);
	
	// move all-minus-largest from AUX (where we left them) to TO (using FROM as extra)
	move_disk(n-1, aux_rod, to_rod, from_rod);
}

int main() {
	int n = 5;
	move_disk(n, 'A', 'B', 'C');		// A, B AND C are the three rods
	return 0;
}
```

Algorithm is extremely simple, don't think about it if ywe think about it, then we will confuse ourself.  
 Move whatever on top to AUX, move the largest disk from FROM to TO and move whatever we put on AUX to this guy TO.   
 So the idea is we break the very large problem into two pieces.  
 When we have a larger problem and we break it down into smaller problems, one of which we can do easily and the other which is exactly the same problem but slightly smaller than the previous one. This is called recursion.  
  **Recursion** essentially means doing the same thing over and over again. 
**Recursion** is essentially solving the same problem using the same code again.  
**Technical definition** is when we call the funcition or whenever we call ourself again we have to break it down just a little bit.  
 So there are **two things to consider in recursion**:  
  first we have to identify the pattern that, what is the pattern? what is being repeated?  
   And then secondly, we have to recognize what can I cut off a little bit once we have those two things then you have recursion ready.   
**Recursion** is not a difficult thing, it is essentially a different way of looking at things.  
If we understand the problem that how we structured it then we can even predict that how long it is going to take.   
Once we formalize the problem properly now we can predict how long it's going to take and that is the **Analysis of Algorithms** course.   
How do we figure out **how much time** this thing will take?   
So one way to do this, we actually run it and see how long it takes. Another way is that we formalize the problem properly and then analyze it that how much time this thing takes and we have tricks, techniques, tools, theorems and formulas for that and we can actually formalize the problem on paper and decides how long it's going to take, and even we can come up with guarantees.   
Take the nuclear reactor example that we have a mathematical guarantee that if it's temperature goes from here to there, I am going to get like 0.00000002 seconds, I am going to get a warning that it is going to explode anything slower than that, going to be catastrophic.  
So where these guarantees come from? That come from "Analysis of Algorithm" course.   
In recursion, first we have the initial call then the recursive call and that recursive call then can stop or it can generate another recursive call and this whole process of calling the same function again and again using with slightly different parameters is called **recursion**.   
so the algorithm is recursive, the process is recursion and the calls are recursive calls or recursive invocations of the same function.
