

Deklaration 
`````c++
MyClass& operator++();      // pre
MyClass  operator++(int);  // post
`````

Implementering 
`````c++
MyClass& MyClass::operator++() {
    ++_val;
    return *this;
}

MyClass MyClass::operator++(int) {
    MyClass old = *this;
    ++(*this);
    return old;
}
`````

Main 
`````c++
++a; // pre  — foretrukket
a++; // post — laver kopi
`````
