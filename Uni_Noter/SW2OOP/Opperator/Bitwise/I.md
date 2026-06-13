

Deklaration 
`````c++
friend MyClass operator|(MyClass lhs, const MyClass& rhs);
`````

Implementering 
`````c++
MyClass operator|(MyClass lhs, const MyClass& rhs) {
    lhs |= rhs;
    return lhs;
}
`````

Main 
`````c++
MyClass c = a | b;
`````
