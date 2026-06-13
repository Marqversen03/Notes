

Deklaration 
`````c++
class MyClass {
public:
    MyClass(int factor);
    int operator()(int x) const;
private:
    int _factor;
};
`````

Implementering 
`````c++
int MyClass::operator()(int x) const {
    return x * _factor;
}
`````

Main 
`````c++
#include <algorithm>
MyClass doubler(2);
int r = doubler(5); // r == 10
std::vector<int> v = {1,2,3};
std::transform(v.begin(), v.end(), v.begin(), doubler);
`````
