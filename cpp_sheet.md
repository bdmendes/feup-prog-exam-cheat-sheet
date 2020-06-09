```
This C++ sheet cheat is adapted from https://github.com/mortennobel/cpp-cheatsheet.
All statements assume using namespace std.
As of C++20 standard.
PROG 19/20, FEUP
Scenic Time
```


## Special Keywords

Reserved keywords (may not be used in other contexts):

```cpp
alignas
alignof
and
and_eq
asm
atomic_cancel
atomic_commit
atomic_noexcept
auto
bitand
bitor
bool
break
case
catch
char
char8_t
char16_t
char32_t
class
compl
concept
const
consteval
constexpr
constinit
const_cast
continue
co_await
co_return
co_yield
decltype
default
delete
do
double
dynamic_cast
else
enum
explicit
export
extern
false
float
for
friend
goto
if
inline
int
long
mutable
namespace
new
noexcept
not
not_eq
nullptr
operator
or
or_eq
private
protected
public
reflexpr
register
reinterpret_cast
requires
return
short
signed
sizeof
static
static_assert
static_cast
struct
switch
synchronized
template
this
thread_local
throw
true
try
typedef
typeid
typename
union
unsigned
using
virtual
void
volatile
wchar_t
while
xor
xor_eq
```

May be used in function names or objects when not in their special context:

```
override
final
import
module
transaction_safe
transaction_safe_dynamic
```


## Preprocessor

```cpp
#include  <stdio.h>         // Insert standard header file
#include "myfile.h"         // Insert file in current directory
#define X some text         // Replace X with some text
#define F(a,b) a+b          // Replace F(1,2) with 1+2
#undef X                    // Remove definition

#if defined(X)              // Conditional compilation (#ifdef X)
#else                       // Optional (#ifndef X or #if !defined(X))
#endif                      // Required after #if, #ifdef
```


## Literals

```cpp
255, 0377, 0xff             // Integers (decimal, octal, hex)
2147483647L, 0x7fffffffl    // Long (32-bit) integers
123.0, 1.23e2               // double (real) numbers
'a', '\141', '\x61'         // Character (literal, octal, hex)
'\n', '\\', '\'', '\"', '\0'// Newline, backslash, single quote, double quote, null terminator
"string"                    // Same as {'h','e','l','l','o','\0'};
true, false                 // bool constants 1 and 0
nullptr                     // Pointer type with the address of 0
```


## Declarations

```cpp
int x;                      // Declare x to be an integer (value undefined)
int x=255;                  // Declare and initialize x to 255
short s;                    // Usually 16 or 32 bit integer (int may be either)
char c='a';                 // Usually 8 bit character
unsigned char u=255;        // Signed is implicit, use unsigned to expand positive range
float f; double d;          // Single or double precision real (always signed)
bool b=true;                // true or false, may also use int (1 or 0)
int a, b, c;                // Multiple declarations

int a[10];                  // Array of 10 ints (a[0] through a[9])
int a[]={0,1,2};            // Initialized array (or a[3]={0,1,2}; )
int a[][2]={{1,2},{4,5}};   // Array of array of ints (only first dimension can be deduced!)
char s[]="hello";           // String (6 elements including '\0'); same as char* s = "hello"
std::string s = "Hello";    // same as std::string s("Hello"); calls default constructor

int *p,*a;                  // p and a are pointers to ints (* before a is necessary!)
char* s="hello";            // s points to first element of array
void* p=nullptr;            // Address of untyped memory (nullptr is 0)
int& r=x;                   // r is a reference to (alias of) int x
int* r=x;                   // r is memory location of x
                            // Dereference later to get object: int myInt = *r;

enum weekend {SAT,SUN,MON}; // weekend is a type wrapping global integer values: SAT=0, SUN=1, MON=2
enum weekend {SAT=14,SUN=3};// Explicit representation as int
enum weekend day = SAT;     // day is a variable of type weekend (e.g may be 14 but not 10)

typedef String char*;       // String s; means char* s;

const int c=3;              // Constants must be initialized, cannot assign to (read-only)
constexpr int = d;          // Same but d must be known at compile time (e.g. d cannot be a parameter)

int8_t,uint8_t,int16_t,
uint16_t,int32_t,uint32_t,
int64_t,uint64_t            // Fixed length standard types

auto it = m.begin();        // Auto deduces type of variable (in this case an iterator)
```
Always read right to left:

```cpp
const int* p=a;             // p is a pointer to a constant int (might point elsewhere)
int* const p=a;             // p is a constant pointer to an int (a will change if as *p)
const int* const p=a;       // Both p and its contents are constant
const int& cr=x;            // cr is a reference (alias) of int that is constant
```


## Storage Classes

```cpp
int x;                      // Declare x in the stack. It's automatically popped at end of scope
static int x;               // Global lifetime even if local scope; cannot be used outside with extern
extern int x;               // Compiler is able to access x declared in other translation units
```


## Statements

```cpp
int x;x=y;                  // Declarations and assignements are statements
;                           // Empty statement

{                           
    int x;                  // x is not accessible outside its scope
}

if (x) a;                   // if x is true (not 0), evaluate a
else if (y) b;              // if not x and y (optional, may be repeated)
else c;                     // if not x and not y (optional)

while (cond) a;             // Repeat while cond is true (if cond is int -> cond!=0)

for (initial; cond; inc) a; // Equivalent to: x; while(y) {a; z;}

for (t elem : container) a; // Range-based for loop - do a; for each COPY of element in container

do a; while (x);            // Equivalent to: a; while(x) a;

switch (x) {                // x must be integer known at compile time
    case X1: a;             // if x == X1, do a; b; c; (everyting is executed until break)
    case X2: b;             // if x == X2, do b; c; (use break if c; is not desired)
    default: c;             // Same as if (true)
}

break;                      // Jump out of while, do, or for loop, or switch
continue;                   // Jump to bottom of while, do, or for loop
return x;                   // Return x from function to caller
```


## Exception handling

```cpp
#include <stdexcept> // to access STL exception classes

try {
  doSomething(); // this may throw an exception
  
  throw invalid_argument("received negative value");
                 // you may throw an object yourself (in this case an exception)
}

catch (exception t) { // if t was thrown, catch it (do not crash program)
  fixSomething();
  cout << t.what() << endl; // print error message describing exception
  throw; // throw t again if you want the program to crash
}

catch (...) { doSomething(); }    // if a throws something else, jump here
```


## Functions

```cpp
int f(int x, int y);     // f is a function taking 2 ints BY COPY and returning int BY COPY
Player& f(Player &x);    // f is a function taking 1 Player BY REFERENCE and returning it BY REFERENCE
                         // make sure that the return object does not get popped out of stack/scope!

int f(int x);            // overload of f (change parameters, return type alone is not enough)
void f();                // f is a procedure taking no arguments
void f(int a=0);         // Default parameters always come after non-default ones
f();                     // Default return type is int (bad practice to hide this info)
inline f() {statement;}  // Optimize for speed when defined in this translation unit
f() { statements; }      // Function definition (must be global)
T operator-(T x);        // allows T a; T b = -a;
T operator++(int);       // postfix ++ or -- (parameter ignored)
extern "C" {void f();}   // f() was compiled in C
```


## Lambda functions

[] is the list of acessible variables from the outer scope. Pass & to allow acess to all.

```cpp
int plusTwo= [](int a){
    return a+2;
};

int a = 3;
int b = plusTwo(a); // b = 5;
```


## Main function

```cpp
int main()  { statements... }     // main is the starting point of any program
int main(int argc, char* argv[]) { statements... }
        //argc -> number of arguments when running the program (default 1 - program name)
        //argv -> command strings (char**)
```


## Expressions

```cpp
T::X                        // Name X defined in class T
N::X                        // Name X defined in namespace N
::X                         // Global name X

t.x                         // Member x of struct or class t
p-> x                       // Member x of struct or class pointed to by p
a[i]                        // i'th element of array a
f(x,y)                      // Call to function f with arguments x and y
T(x,y)                      // Object of class T initialized with x and y
typeid(x)                   // Returns referebce to object of type of x (access name with .name())

dynamic_cast<T>(x)          // Converts x to a T, checked at run time
                            // May convert child class to parent, with slicing data problems
                            // Doing the reverse isn't possible: nullptr or exception
                            
static_cast<T>(x)           // Converts x to a T, for simple data types
                            // Alerts when possible truncation issues (which C-style casts do not do)
                            // Does not work with classe types
                            
reinterpret_cast<T>(x)      // Interpret bits of x as a T
const_cast<T>(x)            // Casts away const

sizeof(x)                   // Number of bytes used to represent object x
sizeof(T)                   // Number of bytes to represent type T
x++                         // Add 1 to x, evaluates to original x (postfix)
x--                         // Subtract 1 from x, evaluates to original x (postfix)
++x                         // Add 1 to x, evaluates to new value (prefix)
--x                         // Subtract 1 from x, evaluates to new value (prefix)
~x                          // Bitwise complement of x
!x                          // true if x is 0, else false (1 or 0 in C)
&x                          // Address of x
*p                          // Contents of address p (*&x equals x)
(T) x                       // Convert x to T (obsolete, use .._cast<T>(x))

x * y                       // Multiply
x / y                       // Divide (return same type of operands - 3/2 is 1)
x % y                       // Modulo (result has sign of x)

x + y                       // Add, or \&x[y]
x - y                       // Subtract, or number of elements from *x to *y
x << y                      // x shifted y bits to left (x * pow(2, y))
x >> y                      // x shifted y bits to right (x / pow(2, y))

x < y                       // Less than
x <= y                      // Less than or equal to
x > y                       // Greater than
x >= y                      // Greater than or equal to

x & y                       // Bitwise and (3 & 6 is 2)
x ^ y                       // Bitwise exclusive or (3 ^ 6 is 5)
x | y                       // Bitwise or (3 | 6 is 7)
x && y                      // x and then y (evaluates y only if x)
x || y                      // x or else y (evaluates y only if !x)
x = y                       // Assign y to x, returns new value of x
x += y                      // x = x + y, also -= *= /= <<= >>= &= |= ^=

x ? y : z                   // y if x, else z
throw x                     // Throw exception, aborts if not caught
```


## Unions

Memory location of all members is the same; only one may be used at given time.

```cpp
union Numbers
{
    int x;
    double d;
};
```


## Classes

Define the class in a header file:

```cpp
#pragma once                // Header files use this directive to avoid conflicting symbols

class T {                   // A new type
private:                    // Section accessible only to T's member functions
protected:                  // Also accessible to classes derived from T
public:                     // Accessible to all
    int x;                  // Member data
    void f();               // Member function
    void g() {return;}      // Inline member function
    void h() const;         // Does not modify any data members
    int operator+(int y);   // t+y means t.operator+(y)
    int operator-();        // -t means t.operator-()

    T(): x(1) {}            // Constructor with initialization list (avoid allocating x twice!)
    T(const T& t): x(t.x) {}// Copy constructor
    
    T& operator=(const T& t)
    {x=t.x; return *this; } // Assignment operator
    
    ~T();                   // Destructor (automatic cleanup routine)
    explicit T(int a);      // Allow T t=T(3) but not T t=3
    T(float x): T((int)x) {}// Delegate constructor to T(int)

    int operator int() const
    {return x;}             // Allows int(t)
    
    int operator()(int a) const
    {return x+a;}           // One can now do T obj; int sumObj = obj(a);
                            // Functors are useful to pass to STL algorithms since they hold state

    friend void i();        // i() has private access (friendship is given by T, not claimed by i())
    friend class U;         // Members of class U have private access
    static int y;           // Data shared by all T objects
    static void l();        // Shared code. May access y but not x
};
```

Then define member functions and use the class in implementation files:

```cpp
#include "T.h"              // Use this directive to access the class definitions

void T::f() {               // Code for member function f of class T
    this->x = x;}           // this is address of self (means x=x;)
    
int T::y = 2;               // Initialization of static member (required)
T::l();                     // Call to static member
T t;                        // Create object t implicit call constructor, same as T t = T();
t.f();                      // Call method f on object t
```


## Class inheritance and polymorfism

Mind the acccess between base and child class members:

```
INHERITANCE                      BASE CLASS
                      public     protected     private

public                public     protected     -
protected             protected  protected     -
private               private    private       - 
```

Create a child class according to your needs:

```cpp
struct T {                  // Equivalent to: class T { public:
  T();                      // Class constructor 
  virtual void i();         // May be overridden at run time by derived class
  virtual void g(int x)=0;  // Must be overridden (pure virtual)
};

class U: public T {         // Derived class U inherits all members of base T
  public:
  U(): T();                 // Base class constructors are not inherited; use delegation like this
  void g(int x) override;   // Explicitly override method g
  void g(int x);            // Same as above but compiler does not check if g is virtual in T
  int y;                    // Specific of U, will get sliced away if U is interpreted as a T
};  
```

Mind possible data slicing problems:

```cpp
class FeupPerson {};
class Student : public FeupPerson {};
FeupPerson p;
Student s;

p = s; // possible but data is sliced away - slicing problem (s=p is illegal)

std::vector<FeupPerson> p(3); // polymorfic since FeupPerson might be a Student as well

p[1] = Student(); // possible but data is sliced away yet again
                  // use virtual methods to fix this issue
```


## Templates - overload for all types

```cpp
template <class T> T
f(T t);

template <class T>
class X {
  X(T t); };                // A constructor
  
template <class T>
X<T>::X(T t) {}

X<int> x(3);                // An object of type "X of int"

template <class T, class U=T, int n=0>     // Template with default parameters
```


## Namespaces - avoid naming conflicts

```cpp
namespace N {class T {};}   // Hide name T
N::T t;                     // Use name T in namespace N
using namespace N;          // Make T visible without N::
```


## Dynamic memory allocation (manual allocations)

C Style:

```cpp
// allocate 1D array
int* intArray = (int*) malloc(nElems*sizeof(int));

// deallocate 1D array
free(intArray); //free takes a void*, but implicit conversion is made
```

C++ Style:

```cpp
// allocate 2D array
int** intMatrix = new int*[nLines];
for (int i=0; i < nLines;++i) intMatrix[i] = new int[nCols];

// deallocate 2D array
for (int i=0; i < nLines;++i) delete[] intMatrix[i];
delete[] intMatrix;
```


## `math.h`, `cmath` - floating point math

```cpp
#include <cmath>            // Include cmath (std namespace)
sin(x); cos(x); tan(x);     // Trig functions, x (double) is in radians
asin(x); acos(x); atan(x);  // Inverses
atan2(y, x);                // atan(y/x)
sinh(x); cosh(x); tanh(x);  // Hyperbolic sin, cos, tan functions
exp(x); log(x); log10(x);   // e to the x, log base e, log base 10
pow(x, y); sqrt(x);         // x to the y, square root
ceil(x); floor(x);          // Round up or down (as a double)
fabs(x); fmod(x, y);        // Absolute value, x mod y
```


## `assert.h`, `cassert` - debugging aid

```cpp
#include <cassert>        // Include iostream (std namespace)
assert(e);                // if e is false, print message and abort
#define NDEBUG            // (before #include <assert.h>), turn off assert
```


## `iostream.h`, `iostream` (replaces `stdio.h`; inherits from ios)

```cpp
#include <iostream>         // Include iostream (std namespace)
cin >> x >> y;              // Read words x and y from stdin (set fail flags if types mismatch)
                            // With strings, extract operator stops at whitespaces (consuming them)
                            // final '\n' (enter) is not consumed, use cin.ignore() later

cout << "x=" << 3 << endl;  // Write line to stdout (endl is same as cout << '\n' << flush)
cerr << x << y << flush;    // Write to stderr and flush
c = cin.get();              // c = getchar();
cin.get(c);                 // Read char, store in c, consume it
cin.peek(c);                // Read char, store in c, do not consume it (still asks if buffer is empty)
cin.getline(s, n, '\n');    // Read line into char s[n] to '\n' (default)

if (cin)                    // Good state (not EOF and not fail)
cin.clear();                // Set error flags to 0 (use cin.ignore() later)
cin.ignore(nChars,Delim);   // Ignore nChars characters or until delimiter found

                            // To read/write any type T (pass by reference is mandatory):
istream& operator>>(istream& i, T& x) {i >> ...; x=...; return i;}
ostream& operator<<(ostream& o, const T& x) {return o << ...;}
```


## `fstream.h`, `fstream` (file I/O works like `cin`, `cout`)

```cpp
#include <fstream>          // Include filestream (std namespace)

ifstream f1("filename");    // Open text file for reading
if (f1)                     // Test if open and input available
    f1 >> x;                // Read object from file 
f1.get(c);                  // Read char or line
while (f1.getline(str, n)) outputStream << str;        // Read file line by line, output to stream

ofstream f2("filename");    // Open file for writing
if (f2) f2 << x;            // Write to file
```

For random access files be aware of stream pointers:

```cpp

fstream handle("filename",ios::binary); // open in binary mode to access char by char

handle.tellg(); // returns pointer to current location
handle.seekg(place); // tries to put current reading position at place

handle.tellp(); // returns pointer to current location
handle.seekp(place); // tries to put current writing position at place

if (handle.fail()) handle.clear(); // if place is out of file bounds, clear error flag
```

## `stringstream` (most methods are inherited from ios; allows input and output)

For specific input/output only purposes, use `istringstream` and `ostringstream` instead.

```cpp
#include <sstream>
stringstream ss("Hello"); // same as stringstream m; m << "Hello";
ss << " World";           // same syntax as cout, cin
ss.str();                 // Return "Hello World"
ss >> a >> b;             // a,b strings bacome "Hello" and "World" (no spaces because of >>)
```

Reaching the end of ss extraction causes eof. To reuse to output:

```cpp
ss.str("");               // Different from ss.str(); this clears current contents
ss.clear();               // Clear error flags
ss << "Now I say hi"      // Reusable again
```


## `string` - variable sized character array

```cpp
#include <string>         // Include string (std namespace)
string s1, s2="hello";    // Create strings
string repeated('c',4):   // Same as string("cccc");
s1.size();                // Number of characters ('\n' is not counted)
s1 += " world";           // Concatenation
s1 == "hello world"       // Comparison, also <, >, !=, etc.
s1[0];                    // 'h'; use s1.at(0) to be able to handle out of bounds exceptions
s1.substr(m, n);          // Substring of size n starting at s1[m]
s1.substr(m);             // Substring from s1[m] until end of s1
s1.c_str();               // Convert to const char*, restricted lifetime
s1 = to_string(12.05);    // Converts number to string
getline(cin, s);          // Read line ending in '\n'
s1.find("hello");         // Pointer to first char of found substring, if not found string::npos
```


## `vector` - dynamic array (rapid insertions/deletions on back; direct access)
```cpp
#include <vector>         // Include vector (std namespace)
vector<int> a(10);        // a[0]..a[9] are int (default size is 0)
vector<int> b{1,2,3};     // Create vector with values 1,2,3
a.size();                 // Number of elements (10)
a.push_back(3);           // Increase size to 11, a[10]=3
e.emplace_back(3)         // Push back an object of type T constructed with parameter 3
a.back()=4;               // a[10]=4;
a.pop_back();             // Decrease size by 1
a.front();                // a[0];
a[20]=1;                  // Segmenation fault
a.at(20)=1;               // Like a[20] but throws out_of_range()

a.erase(a.begin()+3);     // Remove a[3], shifts elements towards back

a.erase(std::remove_if(a.begin(), a.end(), isOdd), a.end());
                          // Erase-remove idiom (faster than erasing one-by-one in a for loop)
                          // Remove_if points to the element after all non-removed elements
                          // isOdd is the comp function, should return bool and receive two objects

a.insert(a.begin()+2,12)  // Make a[2] 12; shifts remaining to the right (linear complexity)

for (int& p : a)  p=0;  // In C++11 you do not need to use iterators for a quick iteration
for (vector<int>::iterator p=a.begin(); p!=a.end(); ++p)  *p=0;  // C++03 had no range-based for loop

vector<int> b(a.begin(), a.end());  // same as b = a;
vector<T> c(n, x);        // c[0]..c[n-1] init to x
```


## `deque` - stack queue (rapid insertions/deletions on front and back; direct acess)

`deque<T>` is like `vector<T>`, but also supports:

```cpp
#include <deque>          // Include deque (std namespace)
deque a<int>;
a.push_front(x);          // Puts x at a[0], shifts elements toward back
a.pop_front();            // Removes a[0], shifts toward front
```


## `list` - doubly linked list (rapid insertion/deletion everywhere, no direct access to elements)

You cannot access specified index without accessing all on the left/right.
Therefore you can't do l[3] and neither l.begin()+3; only it++ and it--.

```cpp
list<int> l = {1,2,8,9,12,2};
auto it = find(l.begin(),l.end(),9);
l.insert(it,23);
l.remove(8);   // remove all elements == 8; reduce container size
l.remove_if(f) // same as above but use f as comp
l.sort();      // only for lists, use std::sort for vector or deque
```


## `array` - statically sized array (lightweight wrapper around C array)

As with C arrays, size must be known at compile time.

```cpp
array<int,3> houses = {1,2,4};
houses.at(2)                   // Return 4
for (const auto& s: houses) {} // Range-based for loop is supported
houses.size()                  // Return 3
```


## `utility` (to use pair)

```cpp
#include <utility>               // Include utility (std namespace)
pair<string, int> a("hello", 3); // A 2-element struct
a.first;                         // "hello"
a.second;                        // 3
```


## `map` - ordered associative container

If order is not important, use `unordered_map` instead.

```cpp
#include <map>            // Include map (std namespace)
map<string, int> a;       // Map from string to int
a["hello"] = 3;           // Add or replace element a["hello"]
a.erase("hello");         // Erase by key
a.clear();                // Erase all map elements, leaving size at 0
for (auto& p:a) cout << p.first << ": " << p.second;  // Prints "hello: 3"
a.size();                 // 1
a.empty()                 // Same as !a.size()
```


## `set` - store unique elements ordered

For insertion to work, the operator < must be defined between two objects of used type.
Elements are considered duplicates (therefore not added) when !(a < b) && !(b < a).

```cpp
#include <set>            // Include set (std namespace)
set<int> s;               // Set of integers
s.insert(123);            // Add element to set

if (s.find(123) != s.end()) // find is set specific (use std::find for other containers)
s.erase(123);  // no need to use iterators here (for vectors you did)

cout << s.size();         // Number of elements in set
```


## `unordered_set` - store unique elements without specific order

Same as above, but out of order, thus faster.
Instead of defining the < operator you must define ==.


## `algorithm` - collection of 60 algorithms on sequences with iterators

```cpp
#include <algorithm>                   // Include algorithm (std namespace)

min(x, y); max(x, y);                  // Smaller/larger of x, y (any type defining <)
swap(x, y);                            // Exchange values of variables x and y
sort(a, a+n);                          // Sort array a[0]..a[n-1] by <
sort(a.begin(), a.end());              // Sort vector or deque
sort(a.begin(), a.end(), f);           // Sort array or deque using f as comp (change order if f)
                                       // f should be like bool f(T a, T b){return a<b;}

reverse(a.begin(), a.end());           // Reverse vector or deque

find(a.begin(),a.end(),value);         // Return pointer to first value if found, else a.end()
binary_search(a.begin(),a.end(),value);// Same as above but container must be sorted

count(a.begin(),a.end(),value);        // Return number of occurrences of value in container a
search(a.begin(),a.end(),sequence.begin(),sequence.end(); // Iterator to first ocurrence of sequence

remove(a.begin(),a.end(),value);       // Place non-removed elements at the beggining
                                       // Capacity isn't changed
                                       // Returns pointer to after last non-removed element
```


## `chrono` - time related library

```cpp
#include <chrono>
using namespace std::chrono;

auto from = high_resolution_clock::now();

// ... do some work    

auto to = high_resolution_clock::now();
using ms = duration<float, milliseconds::period>;
cout << duration_cast<ms>(to - from).count() << "ms";
```


## C style random integers

```cpp
#include <chrono>
using namespace std::chrono;

auto seed =               // Get time since 1 Jan 1970
  system_clock::now().time_since_epoch().count();

srand(seed);              // Initialize random generator (only once in entire program)
rand() % b + a;           // Return integer in range [a,b+a[
```
