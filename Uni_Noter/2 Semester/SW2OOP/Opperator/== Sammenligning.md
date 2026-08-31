




free - Deklaration 
`````c++
bool operator==(const MyClass& Left, const MyClass& Right);

bool operator!=(const MyClass& Left, const MyClass& Right);
`````

Implementering 
`````c++
bool operator==(const MyClass& Left, const MyClass& Right) {
    return Left._val == Right._val;
}

bool operator!=(const MyClass& Left, const MyClass& Right) {
    return !(Left == Right);
}
`````

Main 
`````c++
a == b;

a != b;
`````
