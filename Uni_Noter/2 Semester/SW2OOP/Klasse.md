### Main
`````c++
#include "Person.h"

int main() {

    Person p("Anton", 22);
    p.printInfo();
}
`````

### H file
`````c++

class Person {
private:
    
public:
    Person();  // konstruktør
};
#endif
`````

### cpp File
`````c++
#include "Person.h"
Person::Person(std::string n, int a) {
    navn = n;
    alder = a;
}

void Person::setNavn(std::string n) {
`````
