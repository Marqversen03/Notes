



`````c++
#include "MyClass.cpp" 

template <typename T>
class MyClass {
private:
    T value;
public:
    MyClass(T v);
	T getValue() const;

    void setValue(T v);

    MyClass<T> operator+(const MyClass<T>& other) const;
};
`````


`````c++
template <typename T>
MyClass<T>::MyClass(T v) {
    value = v;
}

template <typename T>
T MyClass<T>::getValue() const {
    return value;
}

template <typename T>
void MyClass<T>::setValue(T v) {
    value = v;
}

template <typename T>
MyClass<T> MyClass<T>::operator+(const MyClass<T>& other) const {
    return MyClass<T>(value + other.value);
}
`````


`````c++
int main() {
    MyClass<int> a(5), b(10);
    MyClass<int> c = a + b;

    std::cout << c.getValue() << std::endl;

    MyClass<double> d(2.5), e(1.5);
    MyClass<double> f = d + e;

    std::cout << f.getValue() << std::endl;

    return 0;
}
`````
