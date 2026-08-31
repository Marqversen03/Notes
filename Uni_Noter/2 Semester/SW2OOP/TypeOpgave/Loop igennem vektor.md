Klassisk Spørgsmål
loop igennem hele listen og returner alles x

I din h file laver du metoden i klassen
`````c++
class boxes
public:
	std::string tostring() const;
`````

i cpp filen

laver et for loop der gør alle b igennem i vektoren boxes.
`````c++
std::string boxes::tostring() const {  
    std::string result;  
    for (const auto& b : boxes_) {  
        result += std::to_string(b.volume()):
    }  
    return result;  
}
`````

klassiske fejl:

- to_string
- Myclass::
- const auto&