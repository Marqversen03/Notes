

``` c++
class KlasseNavn {
public:
    // Constructor (eksempel med fast størrelse)
    KlasseNavn(int size) : size_(size) {
        array_ = new Type[size_]{}; // Initialiseret array [5]
    }

    // 1. DESTRUCTOR: Skal bruge delete[] til arrays [6, 7]
    ~KlasseNavn() {
        delete[] array_; 
    }

    // 2. COPY CONSTRUCTOR: Laver deep copy af hele arrayet [3, 13]
    KlasseNavn(const KlasseNavn& other) : size_(other.size_) {
        if (other.array_ != nullptr) {
            array_ = new Type[size_];
            for (int i = 0; i < size_; ++i) {
                array_[i] = other.array_[i]; // Kopier hvert element
            }
        } else {
            array_ = nullptr;
        }
    }

    // 3. ASSIGNMENT OPERATOR: Deep copy og rensning af gammel data [10]
    KlasseNavn& operator=(const KlasseNavn& other) {
        if (this != &other) {
            // Slet det gamle array først [6, 12]
            delete[] array_;

            size_ = other.size_;
            if (other.array_ != nullptr) {
                array_ = new Type[size_];
                for (int i = 0; i < size_; ++i) {
                    array_[i] = other.array_[i];
                }
            } else {
                array_ = nullptr;
            }
        }
        return *this;
    }

private:
    Type* array_;
    int size_;
};
```