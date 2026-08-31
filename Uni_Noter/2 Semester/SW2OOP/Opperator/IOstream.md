
##   <<

Deklaration 
`````c++
friend std::ostream& operator<<(std::ostream& os, const MyClass& obj);
`````

Implementering 
`````c++
std::ostream& operator<<(std::ostream& os, const MyClass& obj) {
    os << obj._val;
    return os;
}
`````

Main 
`````c++
std::cout << a << std::endl;
`````
