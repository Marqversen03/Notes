
Template er en variable for return types så istedet for erklære en type kan du bare eklære typen til at være T også finde ud af hvad den skal være senere. 

Før klassen og alle implementering af metoderne:
`````c++
template <typename T>
`````

derefter erstate alle værdier der skal bruge t med T.
når du kalder en klasse metode skal du erklære T sådan her
`````c++
T measurements_template<T>::average() const {
```
her er return typen T meeen vigtigt du tilføjger <T> som siger klassen har denne template og gør det mulgit at bruge den i den metode
`````

i main scriptet når du kalder eklære dit objekt skriver du så hvilken type den skal være:
````` c++
measurements_template<double> m;
`````

opgaven kan bede dig om at skifte parameteren til en klasse istedet. så skriver du klassen istedet for double og når du tilføjer en ny værdi tilføjer du den så som den klasse derfor skal man eklære det er en bestemt værdi. her er et simple eksemple

OG
````` c++
measurements_template<double> m;  
m.add(10);
`````

NY
````` c++
measurements_template<temperature> m;  
m.add(temperature(10));
`````

I det du ændre double til en klasse bliver metoden add tvunget til at bruge en klassse istedet for en simple tal. derfor skal talet du add'ere ændres til at være en del af en opsætning af et objek.t