En friend til en klasse må bruge den andens klasses public private og protected. altså alt

Deklaration 
`````c++
class MyClass {
public:
    MyClass(int v);
    friend class Printer; // friend klasse
private:
    int _val;
};

class Printer {
public:
    void print(const MyClass& obj);
};
`````

Implementering 
`````c++
MyClass::MyClass(int v) : _val(v) {}

void Printer::print(const MyClass& obj) {
    // kan se _val direkte — pga. friend
    std::cout << obj._val;
}
`````

Main 
`````c++
MyClass m(42);
Printer p;
p.print(m); // udskriver 42
`````
