

Deklaration 
`````c++
MyClass& operator=(const MyClass& other);
`````

Implementering 
`````c++
MyClass& MyClass::operator=(const MyClass& other) {
    if (this == &other) return *this; //safety check
    _val = other._val;
    return *this;
}
`````

Main 
`````c++
a = b;
a = a; // safe
`````
