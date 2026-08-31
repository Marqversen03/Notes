
Deklaration 
`````c++
MyClass operator+=(const MyClass& other);
`````

Implementering 
`````c++
MyClass MyClass::operator+=(const MyClass& other) {
    return _val += other._val;
}
`````

Main 
`````c++
std::cout << (a += b) << std::endl;
`````
