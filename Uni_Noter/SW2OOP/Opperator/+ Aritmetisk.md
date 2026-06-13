
Deklaration 
`````c++
MyClass& operator+=(const MyClass& other);
`````

Implementering 
`````c++
MyClass& MyClass::operator+=(const MyClass& other) {
    _val += other._val;
    return *this;
}
`````

Main 
`````c++
a += b;
`````
