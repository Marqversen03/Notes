arv + aggregering kombineret. Leaf og Composite deler interface.

Deklaration 
`````c++
class Component {
public:
    virtual void show() = 0;
    virtual ~Component() {}
};

class Leaf : public Component {
public:
    void show() override;
};

class Composite : public Component {
public:
    void add(Component* c);
    void show() override;
private:
    std::vector<Component*> _children;
};
`````

Implementering 
`````c++
void Leaf::show() { /* vis leaf */ }

void Composite::add(Component* c) {
    _children.push_back(c);
}
void Composite::show() {
    for (auto* c : _children)
        c->show(); // kalder Leaf eller Composite
}
`````

Main 
`````c++
Leaf l1, l2;
Composite root;
root.add(&l1);
root.add(&l2);
root.show(); // traverserer hele træet
`````
