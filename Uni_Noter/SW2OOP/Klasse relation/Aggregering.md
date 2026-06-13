Begge klasser lever hver for sig. den ene klasse indenholder referance til mange af den anden klasse. spiller på et hold

![[Pasted image 20260613231905.png]]

Deklaration 
`````c++
class Player {
public:
    Player(int id);
    int id() const;
private:
    int _id;
};

class Team {
public:
    void add(Player* p);
private:
    std::vector<Player*> _players;
};
`````

Implementering 
`````c++
Player::Player(int id) : _id(id) {}
int Player::id() const { return _id; }

void Team::add(Player* p) {
    _players.push_back(p);
}
`````

Main 
`````c++
Player p1(1), p2(2);
Team team;
team.add(&p1);
team.add(&p2); // Players lever videre uden Team
`````
