virtuel funktionen er en funktion der står top men blir overflowet af klassen der kalder den. den implementering sker i en seperat h file

### Implemanterin
`````c++
class Amplifier {
public:
    virtual void amplify(Signal& signal)=0;
    virtual ~Amplifier() = default;

};
`````

Filer der overwriter funktionen:
### .h file
`````c++
class Broadrate {
public:
    void amplify(Signal& signal) override;
};
`````

### c++ file
`````c++
void BroadBandAmplifier::amplify(Signal& signal) {
//bla bla bla
}
`````