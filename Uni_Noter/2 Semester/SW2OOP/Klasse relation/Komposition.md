Den ene klasse skaber den anden. 
dør car dræber du også engine.

![[Pasted image 20260613231340.png]]
Deklaration 
`````c++
class Engine {
public:
    void start();
};

class Car {
public:
    void drive();
private:
    Engine _engine; // ejet — ikke pointer
};
`````

Implementering 
`````c++
void Engine::start() {}

void Car::drive() {
    _engine.start();
}
`````

Main 
`````c++
Car car;
car.drive(); // Engine lever med Car
`````
