

Deklaration 
`````c++
class MyClass {
public:
    MyClass(int v) : _val(v) {}
    MyClass& operator+=(const MyClass& other);
private:
    int _val;
};
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
MyClass a(3), b(4);
a += b; // a._val == 7
`````
