---
layout: post
title:  "Tower of Honai and the real power of abstraction"
author: "discreetso (M.Huzaifa)"
date:   2026-02-26 09:08:00 +0500
categories: Classes recursion abstraction tower Honai OOP 
---

The Tower of Honai and the real power of abstraction

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