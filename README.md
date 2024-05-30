<h1 align="center">
    C++ Advanced
 </h1>
 <h5 align="center">
   Author: Anshaj Kumar
 </h5>
 
 
 ### Contents  
 
| No. | Topics |
| --- | --------- |
|    | **Core C++** |
|1   | [Special Notes](#special-notes-) |
|2   | [Strings in C++](#strings-in-c) |




##### *Refer [GFG tutorials](https://www.geeksforgeeks.org/software-design-patterns) for more*



 ###    Special Notes :  
 
 1. If we do not define *main()* function in any cpp file compiler will compile the file but linker will give missing **entry point error**.
 2. *Refrences should we initialised with a value/refrence at time of deceleration*  
 Reference is not a variable and we have to declare it at time of initialisation and 
	 can't be modified furthur i.e. assigned to reference of other variable if we try to do this 
  	it will simply copy the value.
    ```C++
		int a = 5;
		int b = 6;
		// int& ref ;  X wrong (ref should we initialised wiyh a value/refrence at time of deceleration)
		int& ref = a;
		ref = b ; ( implies a = 6 , b = 6 ) 
    ```  
   3. `const int* const a=new int`  Here, 1st pointer means you cant change refrence of pointer(i.e memory address it is pointing to) 2nd const means you can't change Value after dereferencing pointer.
   4. If any method is const (declare const after method name like `int GetCount() const { return count; }`) i.e. it is read only and not going to change value of any variable of class.
   5. If a variable is declared as `mutable int a;`, it can be changed from inside of const methods.  
   6. `Object obj = new Object();` initialises Object in Heap while `Object obj;` initialise Object in stack.  
>  *  Allocating in Heap takes longer than allocating in stack.  
>  *  In case of heap , You have to manually free the memory you allocated. (i.e. `delete obj;`)  
>  *  In case of heap , contiguous memory is allocated i.e. we have to find a place from where required amount of memory is present which of course takes time. (There is something called freelist which takes care of free memories/memories addresses.)
	
   7. `new` keyword calls constructor and `delete` keyword calls destructor in case of class.
   

   
**[⬆ Back to Top](#----c-advanced-)** 

# Strings in C++
```C++
#include<iostream>
#include<string>
int main()

```
