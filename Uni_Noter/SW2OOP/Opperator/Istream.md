
##   >>

Deklaration 
`````c++
friend std::istream& operator>>(std::istream& is, MyClass& obj);
`````

Implementering 
`````c++
std::istream& operator>>(std::istream& is, MyClass& obj) {
    is >> obj._val;
    return is;
}
`````

Main 
`````c++
std::cin >>; a;
`````
