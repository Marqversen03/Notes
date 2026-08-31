### Member
Opperator skal være en del af en funktion når det er en member såsom:
	= [] () ->
valgfri
	-+ *
aldrig
	<<

### Const
`````c++
Myclass Operator+(Myclass& other) const
			Funktionen må ikke ændre this

Myclass Operator+(const Myclass& other) 
			Funktionen må ikke ændre other

const Myclass Operator+(const Myclass& other) 
			Resultatet må ikke ændres

const int& operator[](int i) const;
			Man må ikke sætte en værdi kun læse
			
std::ostream& operator<<(std::ostream& os, const MyClass& obj);
			Objektet kan kun printes ⚠️ ret vigtig ⚠️
`````


`````c++
class MyClass {

private:
    int value;
public:
    MyClass(int v);

    // Member operator
    MyClass operator+(const MyClass& other) const;

    // Unary
    MyClass operator++();      // prefix

    MyClass operator++(int);  // postfix

    // Special operators (SKAL være member)
    int& operator[](int index);
    void operator()();
    int getValue() const;

};
// Non-member
MyClass operator+(const MyClass& a, const MyClass& b);
`````

`````c++
#include "MyClass.h"
// Constructor
MyClass::MyClass(int v) {
    value = v;
}

  

// Member +
MyClass MyClass::operator+(const MyClass& other) const {
    return MyClass(value + other.value);
}
// Prefix ++
MyClass MyClass::operator++() {
   ++value;
   return *this;
}

// Postfix ++
MyClass MyClass::operator++(int) {
    MyClass temp = *this;
    value++;
    return temp;
}

  

// Index []

int& MyClass::operator[](int index) {
    // eksempel (dummy)
    static int dummy = 0;
    return dummy;

}

  

// Function call ()

void MyClass::operator()() {
    std::cout << "Function called! Value = " << value << std::endl;

}

  

// Non-member +

MyClass operator+(const MyClass& a, const MyClass& b) {
    return MyClass(a.getValue() + b.getValue());
}

  

int MyClass::getValue() const {
    return value;

}
`````

`````c++
int main() {

    MyClass a(5), b(10); 
    MyClass c = a + b;
    ++a;
    a++;
    a();  // function operator
    std::cout << c.getValue() << std::endl;
    return 0;

}
`````