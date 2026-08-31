## Initinereing
### Den klassiske initinereing
`````c++
int a = 1;
double b = 3.14;
char c = 'A';
`````

Problemet opstår i "Implicit type conversion"

````` c++
int a = 3.7; // bliver til 3
int a //bliver et mærkelig tal
`````

### Direct initialization

````` cpp
int a(1);
double b(3.14);
std::string s("hej");
`````

### Uniform initialization

````` c++
int a{1};
double b{3.14};
std::string s{"hej"};
`````

Denne er mere sikker fordi:
````` c++
int a = 3.7; // rapportere fejl
`````

denne har også default initialization

````` c++
int a{} // =0
bool c{} // false
`````

### Array 

````` c++
int arr[3] = {1,2,3};
int arr[]{1,2,3};
int arr[3]{}; // alle = 0
`````
### Pointer 

````` c++
int* p = nullptr;
int* p{nullptr};
`````

### Refference 

````` c++
int x = 5;
int& ref{x} //ref er variablen
`````

### Pointer 

````` c++
const int a{5};

constexpr int b{5}; // brug den i array size []
`````
 dette gør a og b altid vil være lig 5. forskellen er at const expr
 betyder at b er kendt til 5 før programmet starter. og dervel gør programmet mere stabil og fast as fuck.
