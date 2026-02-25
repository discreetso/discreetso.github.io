---
layout: post
title:  "File Handling In C- Character & Binary"
author: "discreetso (M.Huzaifa)"
date:   2026-02-02 10:57:00 +0500
categories: Classes Python OOP 
---
### The Role of Buffers in Stream Flow

When we write `cout << "Hello World!";`, the text appears on the console. Behind that console, there is a software layer called the **terminal**. However, data does not move directly from your code to the screen; it travels through a temporary storage area in the RAM called a **Buffer**.

#### What is a Buffer?

A buffer is a temporary memory location that holds data while it is being moved from one place to another. In this case, the buffer sends data to the terminal piece by piece.

#### Why do we need a Buffer?

The primary reason is the **difference in speed** between the CPU and external hardware.

> **Example:**  
> Suppose you want to transfer data from a computer to a USB drive. A USB drive is much slower than your processor. If the system transferred data directly, the computer would have to "wait" for the USB to finish, slowing down your entire operation.
> 
> Instead, the system places the data into a **buffer** first. Once the data is in the RAM, the system is free to perform other tasks while the buffer handles the slow transfer to the USB in the background.

##### Summary

While we usually don't need to manage the buffer manually, it is essential to understand that it exists between our **input and output**. This understanding helps us visualize the actual flow and stream of data within a computer system.

```c
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

void output_matrix(int a[][3], int rows, int cols) {
  for(int i = 0; i < rows; i += 1) {
    for(int j = 0; j < cols; j += 1) {
      cout << a[i][j] << " ";
    }
    cout << endl;
  }
}

void char_example() {
  //output file stream instance
  ofstream fout;    //ofstream is datatype as int and fout is a variable, we write this by convention
  string filename = "sample.txt";
  string line;

  //when we write .open to open any file it is by default in the write mode
  fout.open(filename);    //try using the absolute path
  fout << "my test line" << endl;   //fout writing out of the program to the file
  fout.close();     //need to remeber this

  //input file stream instance
  ifstream fin;     //fin variable is also by convention
  fin.open(filename);

  while (fin) {
    getline(fin, line);
    cout << line << endl;
  }
  fin.close();
}

void bin_example() {
  int pixels[3][3];

  //assigning values to the array pixels
  for(int i = 0; i < 3; i += 1)
    for(int j = 0; j < 3; j += 1)
      pixels[i][j] = 1 + i*j;

  output_matrix(pixels, 3, 3);

  //writing to a file
  ofstream fout("data.bin", ios::binary);
  for(int i = 0; i < 3; i += 1)
    for(int j = 0; j < 3; j += 1)
      fout.write((char *)&pixels[i][j] , sizeof(int));

  fout.close();   //notice what happens when we miss this

  //read data back in
  cout << "Resetting pixels...." << endl;
  for(int i = 0; i < 3; i += 1)
    for(int j = 0; j < 3; j += 1)
      pixels[i][j] = 0;

  output_matrix(pixels, 3, 3);

  cout << "Reading again..." << endl;
  ifstream fin("data.bin", ios::binary);   //try missing file

  //also try !fin in the condition
  if(fin.fail()) {
    cout << "Failed to read file ... " << endl;
  } else {
    for(int i = 0; i < 3; i += 1)
      for(int j = 0; j < 3; j += 1)
        fin.read((char *)&pixels[i][j], sizeof(int));
  }
  fin.close();

  output_matrix(pixels, 3, 3);
}

int main() {
  cout << "int: " << sizeof(int) << endl;
  cout << "char: " << sizeof(char) << endl;

  char_example();
  bin_example();
  return 0;
}
```