Begge klasser lever hver for sig. men den ene klasse
kender til den anden ved pointere

![[Pasted image 20260613231716.png]]

Deklaration 
`````c++
class Car {
public:
    void drive();
};

class Driver {
public:
    Driver(Car* car);
    void go();
private:
    Car* _car; // pointer — ejer ikke
};
`````

Implementering 
`````c++
Driver::Driver(Car* car) : _car(car) {}

void Driver::go() {
    _car->drive();
}
`````

Main 
`````c++
Car car;
Driver driver(&car);
driver.go(); // Car lever uden Driver
`````
