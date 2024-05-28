Bag Of Marble program is just a simple program to have a few classes that store information in this example it would be marbles and see how well it does this. The Bag itself and the marbles may be different colors that will all be stored and then either read to output or to keep adding values to the program.

Representing a Marble in this program could be as stated before as a class that has different properties such as either colors or size 

Making a bag class would also be useful to include since it will be where we store the information and has other properties where we could add a marble and then it asks what type and color and the same with subtraction. We could make a subtract random and add random that adds a random marble color and size added 
as well with a list that could make a list of all the marbles in the bag

Test cases
Adding Marbles: Verify that marbles are correctly added to the bag.
Removing Marbles: Verify that a random marble is removed and that the count of marbles decreases.
Empty Bag Removal: Verify that removing a marble from an empty bag returns None.
List Marbles: Verify that the list of marbles in the bag is accurate.
Pseudocode for Tests

Another test we could do is as well see what would happen to the program if we add 100 random marbles if it prints the same marble 100 times or if each one is distinct too and if it even capable of doing so 

IMPLEMENTATION

#include <iostream>
#include <vector>
#include <string>
#include <cstdlib>
#include <ctime>

// Marble class
class Marble {
public:
    std::string color;
    std::string size;
    float weight;

    Marble(std::string c, std::string s, float w) : color(c), size(s), weight(w) {}

    std::string toString() {
        return "Marble(color=" + color + ", size=" + size + ", weight=" + std::to_string(weight) + ")";
    }
};

// BagOfMarbles class
class BagOfMarbles {
private:
    std::vector<Marble> marbles;

public:
    void addMarble(const Marble& marble) {
        marbles.push_back(marble);
    }

    Marble removeRandomMarble() {
        if (marbles.empty()) {
            throw std::runtime_error("No marbles in the bag!");
        }
        int index = rand() % marbles.size();
        Marble removedMarble = marbles[index];
        marbles.erase(marbles.begin() + index);
        return removedMarble;
    }

    int countMarbles() const {
        return marbles.size();
    }

    std::vector<Marble> listMarbles() const {
        return marbles;
    }
};

// Main function for testing the implementation
int main() {
    srand(time(0));

    // Create a BagOfMarbles object
    BagOfMarbles bag;

    // Add marbles to the bag
    bag.addMarble(Marble("red", "small", 5.0));
    bag.addMarble(Marble("blue", "medium", 6.0));

    // List marbles in the bag
    std::cout << "Marbles in the bag:" << std::endl;
    for (const Marble& marble : bag.listMarbles()) {
        std::cout << marble.toString() << std::endl;
    }

    // Remove a random marble
    std::cout << "Removing a random marble..." << std::endl;
    Marble removedMarble = bag.removeRandomMarble();
    std::cout << "Removed: " << removedMarble.toString() << std::endl;

    // List marbles in the bag after removal
    std::cout << "Marbles left in the bag:" << std::endl;
    for (const Marble& marble : bag.listMarbles()) {
        std::cout << marble.toString() << std::endl;
    }

    // Count marbles in the bag
    std::cout << "Total marbles in the bag: " << bag.countMarbles() << std::endl;

    return 0;
}
