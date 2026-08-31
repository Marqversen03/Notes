
Deklaration 
`````c++
class MyClass {
public:
    MyClass(int v);
    explicit operator int() const;   // til int
    explicit operator bool() const;  // til bool
private:
    int _val;
};
`````

Implementering 
`````c++
MyClass::operator int() const {
    return _val;
}
MyClass::operator bool() const {
    return _val != 0;
}
`````

Main 
`````c++
MyClass a(7);
int x = static_cast<int>(a);  // x == 7
if (a) { /* bool — truthy hvis _val != 0 */ }
MyClass b(0);
if (!b) { /* b er falsy */ }
`````
