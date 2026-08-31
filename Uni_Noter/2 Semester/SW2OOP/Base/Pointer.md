
Pointer er pisse smart når du arbejder med strings eller array fordi en pointer er 8 bytes istedet for strings og array som kan være større eller placeret rundt omkring. 

````` c++
&variable // addressen af variablen
int* // type af pointer
*ptr // dereference af pointer

// -- eksemple --

int i{1};
int* i_ptr = &i // i_ptr = 0xADDRESSE
*i = 1;
`````

Pointer er arithmetik. lyder fancy men basicly bare et normal variable hvis du plusser en ptr med 1 får du en ny addresse. dette er brugbart i array for næste addresse er næste værdi i et array

````` c++
int arr[3] ={5,7,9}
int* ptr = arr;

*ptr == 5;
*(ptr +1) ==7
`````
her er det vigtig at se der mangler et & foran arr. dette er fordi vi arbejder med array. og ved sætte et & foran for man pointeren til hele arrayet og ikke første element
````` c++
int* ptr = arr;

int* ptr = &arr[0];
`````

## Const too pointer
const og pointere er lidt fucked... her er basics

### Pointer til const
````` c++
const int* p = &x;
`````
Du kan ikke ændre værdien via pointer.

### Const pointer
````` c++
int* const p = &x;
`````
Du kan ikke ændre hvor pointeren peger

