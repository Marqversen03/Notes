
##    +  -  +=  -=

Deklaration 
`````c++
int& operator[](int i);
const int& operator[](int i) const;
`````

Implementering 
`````c++
int& MyClass::operator[](int i) {
    return _data[i];//read and write
}
const int& MyClass::operator[](int i) const {
    return _data[i];
}//read only
`````

Main 
`````c++
a[0] = 5;          // non-const
int x = a[0];     // const
`````
