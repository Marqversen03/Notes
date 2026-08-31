
For at sortere en vektor skal man  include

`````c++
#include <algorithm>
`````

For det meste skal du kopier en anden vektor du gerne vil have sorted:
`````c++
std::vector<box> sorted=boxes_;
`````
Her er listen fyldt med box som er fordi det er en aggretions klasse vi arbejder med

derefter skal den sortes
`````c++
std::sort(sorted.begin(), sorted.end());
`````

også printes som altid
`````c++
for (const auto& b : sorted) {  
    result += std::to_string(b.volume()) + ",";  
}  
return result;
`````