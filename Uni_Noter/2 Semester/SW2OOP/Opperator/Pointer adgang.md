
##    +  -  +=  -=

Deklaration 
`````c++
class Inner {
public:
    void hello() { /* ... */ }
};
class MyClass {
public:
    MyClass(Inner* p);
    Inner* operator->() const;
private:
    Inner* _ptr;
};
`````

Implementering 
`````c++
Inner* MyClass::operator->() const {
    return _ptr;
}
`````

Main 
`````c++
Inner obj;
MyClass wrapper(&obj);
wrapper->hello(); // kalder Inner::hello()
`````
