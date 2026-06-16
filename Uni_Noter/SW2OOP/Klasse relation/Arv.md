En klasse er arv'er egenskaber fra en anden klasse.  
![[Pasted image 20260614224207.png]]
Deklaration 
`````c++
class Animal {
public:
    virtual void speak() = 0; // ren virtuel
    virtual ~Animal() = default;
};

class Dog : public Animal {
public:
    void speak() override;
};

class Cat : public Animal {
public:
    void speak() override;
};
`````

Implementering 
`````c++
void Dog::speak() { /* Vuf */ }
void Cat::speak() { /* Miav */ }
`````

Main 
`````c++
Animal* a = new Dog();
a->speak(); // Dog::speak() — polymorfisme
delete a;
`````

Vis override bliver markered rødt er det formeneligt fordi de to funktioner ikke matcher altså superklassen og arven. tjek ==Const==