

``` c++
class KlasseNavn {
public:
    // Constructor (eksempel)
    KlasseNavn(Type vardi) {
        pointer_ = new Type(vardi);
    }

    // 1. DESTRUCTOR: Frigiver hukommelsen [7, 8]
    ~KlasseNavn() {
        delete pointer_; 
    }

    // 2. COPY CONSTRUCTOR: Laver en "deep copy" ved oprettelse [3, 9]
    KlasseNavn(const KlasseNavn& other) {
        if (other.pointer_ != nullptr) {
            // Alloker ny hukommelse og kopier værdien
            pointer_ = new Type(*other.pointer_); 
        } else {
            pointer_ = nullptr;
        }
    }

    // 3. ASSIGNMENT OPERATOR: Håndterer tildeling mellem eksisterende objekter [10]
    KlasseNavn& operator=(const KlasseNavn& other) {
        // Tjek for selv-tildeling (vigtigt!)
        if (this != &other) {
            // Slet eksisterende data for at undgå memory leak [8]
            delete pointer_;

            if (other.pointer_ != nullptr) {
                // Alloker ny hukommelse og kopier værdi
                pointer_ = new Type(*other.pointer_);
            } else {
                pointer_ = nullptr;
            }
        }
        return *this; // Returner reference til sig selv [11]
    }

private:
    Type* pointer_;
};
```