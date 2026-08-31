
i dont fucking know tbh

Deklaration 
`````c++
class MyClass {
public:
    MyClass(int size);                       // constructor
    ~MyClass();                               // 1. destruktor
    MyClass(const MyClass& other);           // 2. copy ctor
    MyClass& operator=(const MyClass& other); // 3. copy assign

    int&       operator[](int i);
    const int& operator[](int i) const;
    int size() const;

private:
    int* _data;
    int  _size;
};
`````

Implementering 
`````c++
MyClass::MyClass(int size)
    : _size(size), _data(new int[size]()) {}

MyClass::~MyClass() {
    delete[] _data;
}

MyClass::MyClass(const MyClass& other)
    : _size(other._size), _data(new int[other._size]) {
    for (int i = 0; i < _size; ++i)
        _data[i] = other._data[i];
}

MyClass& MyClass::operator=(const MyClass& other) {
    if (this == &other) return *this;
    delete[] _data;
    _size = other._size;
    _data = new int[_size];
    for (int i = 0; i < _size; ++i)
        _data[i] = other._data[i];
    return *this;
}

int& MyClass::operator[](int i)       { return _data[i]; }
const int& MyClass::operator[](int i) const { return _data[i]; }
int MyClass::size() const { return _size; }
`````

Main 
`````c++
MyClass a(3);
a[0] = 10; a[1] = 20; a[2] = 30;

MyClass b = a;   // copy constructor — deep copy
b[0] = 99;       // ændrer kun b, ikke a

MyClass c(1);
c = a;           // copy assignment — deep copy
`````
