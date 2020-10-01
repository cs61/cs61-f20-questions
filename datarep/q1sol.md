Data representation question
============================

Common memory leak/error Bingo! Mark the statements on your Bingo card that do not cause any memory leaks, errors, or undefined behavior.

___B_____I_____N_____G_____O___
|     |     |     |     |     |
|  1  |  2  |  3  |  4  |  5  |
|_____|_____|_____|_____|_____|
|     |     |     |     |     |
|  6  |  7  |  8  |  9  | 10  |
|_____|_____|_____|_____|_____|
|     |     |     |     |     |
|  11 |  12 |  13 | 14  |  15 |
|_____|_____|_____|_____|_____|
|     |     |     |     |     |
|  16 |  17 |  18 |  19 |  20 |
|_____|_____|_____|_____|_____|
|     |     |     |     |     |
|  21 |  22 |  23 |  24 |  25 |
|_____|_____|_____|_____|_____|



X 1. Overwrites end of destination
char* myPtr = (char*) malloc(10);
strcpy(myPtr, "CS61 rocks!!!");


X 2. Write beyond the allocated memory
int* myIntPtr = malloc(4);
myIntPtr += sizeof(long);

*myIntPtr = 10;


+ 3. Valid free with more space allotted than needed
char* myPtr = (char*) malloc(10);
strcpy(myPtr, "COVID-19");
free(myPtr);


X 4.Double free, so invalid free
char* myPtr = (char*) malloc(15)
free(myPtr);
free(myPtr_;


X 5. Memory leak due to lack of free
int main () {
	int* myIntPtr = (int*) malloc(16);
	return;
}


+ 6. Valid free with just adequate space allotted
char* myPtr = (char*) malloc(12); 
strcpy(myPtr, "CS61 rocks!");
free(myPtr);


X 7. Attempts to dereference end of struct memory
void function () {
	struct my_struct {
		int a;
		char b;
		long c;
	}

	my_struct* new_struct = malloc(sizeof(my_struct));
	char* structPtr = (char*) new_struct;
	structPtr += sizeof(my_struct);
	*structPtr;
}


+ 8. Valid free
void* myPtr = (void*) malloc(10);
free(myPtr);


X 9. Does not delete the array of data
char* myBuffer = new char[10];
delete myBuffer;


X 10. This initializes the value of the pointer not the number of array ints
int* myptr = new int(61);
*myptr[60};


X 11. Malloc should use free and not delete
void* myPtr = (void*) malloc(10);
delete myPtr;


+ 12. Valid new/delete pairing 
char* myPtr = new T;
delete myPtr;


+13. Valid free
free(NULL);


X 14. Unitialized variable
int* myIntPtr = (int*) malloc(24);
int i1 = myIntPtr[1];
int i2 = myIntPtr[2];

void function() {
	int sum = i1 + i2;
}


+ 15. Valid free
void* myPtr = (void*) malloc(10);
free(myPtr);


X 16. Allocation of less memory than needed to store int
int* myIntPtr = (int*) malloc(3);
*myIntPtr = 61;


X 17. Mixing new and free, so invalid free
void function() {
	struct my_struct {
		int a;
	}
	
	my_struct* new_struct = new my_struct[5];
	free(new_struct);
}


+ 18. Valid even though it's unused (too similar to Compiler hijinks in the lecture notes?)
int main() {
	char* filename = malloc(40);
	int line = 10;
	
	while (line < 15) {
		printf("%s", "line number: ", line);
		++line;
	}
	
	free(filename);
}


X 19. Invalid hexdump of memory beyond end (too close to datarep2?)
int main() {
	long i = 61;
	
	hexdump(&i, sizeof(i)+1);
}


X 20. Invalid hexdump of memory beyond end (too close to datarep2?)
int main() {
	int i = 61;
	
	hexdump(&i, sizeof(long));
}


X 21. One-off error
char* myCharPtr = (char*) malloc(10);
myChar[10] = 's';
char i1 = myChar[10];

X 22. 


+ 23. Valid
int* myIntPtr = (int*) malloc(24);
int i1 = myIntPtr[1];
int i2 = myIntPtr[2];

void function()
{
	int sum = i1 + i2;
	free(myIntPtr);
}


X 24. Off by one access
int* myIntPtr = (int*) malloc[60];
float sum = 0;

for (int i = 0; i < 16; ++i) {
  sum += myIntPtr[i];
}


X 25. Uninitialized and one-off
char* myCharPtr = (char*) malloc(10);
char i1 = myChar[10];


//Resources
https://www.cprogramming.com/tutorial/memory_debugging_parallel_inspector.html
CS61 DataRep lecture notes + code
