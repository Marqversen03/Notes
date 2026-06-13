
hvis en klasse har en pointer skal der laves rule of three. eksemple

`````c++
MyClass a;
MyClass b = a
`````

a og b peger det samme sted hen. så vis a slettes crasher programmet. vis du ændre a ændre du også b. 
programmet fixer det her selv med en "Shallow clean" men vi kan godt lide en "deep clean" denne inkludere tre regler

1. Destructor
2. Copy constructor
3. Copy assignment


Deklaration 
`````c++
// Når du har dette i din klasse:
private:
    int* _data;   // <-- rå pointer
    int  _size;

// SKAL du implementere alle tre:
~MyClass();                              // 1. Destruktor
MyClass(const MyClass& other);          // 2. Copy constructor
MyClass& operator=(const MyClass& other); // 3. Copy assignment
`````

Implementering 
`````c++
MyClass::~MyClass() {
    delete[] _data;
}

MyClass::MyClass(const MyClass& other) {
    _size = other._size;
    _data = new int[_size];
    
    for (int i = 0; i < _size; i++) {
        _data[i] = other._data[i];
    }
}

MyClass& MyClass::operator=(const MyClass& other) {
    if (this == &other) return *this;
    delete[] _data;
    _size = other._size;
    _data = new int[_size];
    for (int i = 0; i < _size; i++) {
        _data[i] = other._data[i];
    }
    return *this;
}
`````

Main 
`````c++
MyClass a(5);
MyClass b = a;  // copy constructor
MyClass c(3);
c = a;          // copy assignment
`````
