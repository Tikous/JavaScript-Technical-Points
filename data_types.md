**What data types does JavaScript have and how do they differ**

JavaScript has eight data types: Undefined, Null, Boolean, Number, String, Object, Symbol, and BigInt.
- Symbol represents a unique and immutable data type created to resolve possible global variable conflicts.
- BigInt is a numeric type of data that can represent integers in any precision format. BigInt can be used to safely store and manipulate large integers, even if the Number is outside the range of safe integers that number can represent.

**These data can be divided into raw data types and reference data types:**

- Stack: raw data type
- Heap: References data types (objects, arrays, and functions)

**The difference between the two types is the storage location:**

- The original data type is a simple data segment directly stored in the stack, which occupies a small space and has a fixed size, and belongs to the frequently used data, so it is stored in the stack;

- An object whose data type is stored in the heap, occupying a large space and having an unfixed size. If stored in the stack, it will affect the performance of the program. The reference data type stores a pointer on the stack that points to the starting address of the entity in the heap. When the interpreter looks for a reference value, it first retrieves its address in the stack and then retrieves the entity from the heap.

**The concepts of heap and stack exist in data structures and operating system memory**

- In the data structure, the access mode of the data in the stack is first in, last out.
- The heap is a priority queue that is sorted by priority, which can be specified by size.

**In operating systems, memory is divided into stack and heap areas:**

- The stack memory is automatically allocated and released by the compiler to store the parameter values of functions and the values of local variables. It operates like a stack in a data structure.
- Heap area memory is usually freed by the developer allocation, and if the developer does not free it, it may be reclaimed by the garbage collection mechanism at the end of the program.