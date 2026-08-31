

Deklaration 
`````c++
class MyClass {
public:
    MyClass(int v) : _val(v) {}
    friend MyClass operator+(MyClass lhs, const MyClass& rhs);
private:
    int _val;
};
`````

Implementering 
`````c++
MyClass operator+(MyClass lhs, const MyClass& rhs) {
    lhs._val += rhs._val; // kan se _val pga. friend
    return lhs;
}
`````

Main 
`````c++
MyClass a(3), b(4);
MyClass c = a + b; // c._val == 7
`````
