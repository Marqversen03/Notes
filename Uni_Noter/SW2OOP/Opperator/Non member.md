

Deklaration 
`````c++
class MyClass {
public:
    MyClass(int v) : _val(v) {}
    MyClass& operator+=(const MyClass& other);
    int val() const { return _val; }
private:
    int _val;
};
// deklareres UDENFOR klassen — ingen friend
MyClass operator+(MyClass lhs, const MyClass& rhs);
`````

Implementering 
`````c++
MyClass operator+(MyClass lhs, const MyClass& rhs) {
    lhs += rhs; // bruger public +=
    return lhs;
}
`````

Main 
`````c++
MyClass a(3), b(4);
MyClass c = a + b; // c._val == 7
`````
