
## **Steps to Shuffle and Rank a Deck of Cards**

1. **Shuffle the deck** – Use **Fisher-Yates Algorithm** (O(n) time complexity).
2. **Rank the cards** – Define a ranking order for suits and values.

---

## **Implementation in Python**

Here’s a Python solution that shuffles a deck of 52 playing cards and sorts them based on rank:








```python
import random

# Define suits and values
suits = ['Hearts', 'Diamonds', 'Clubs', 'Spades']
values = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']

# Create the deck
deck = [(value, suit) for suit in suits for value in values]

# Shuffle using Fisher-Yates Algorithm
random.shuffle(deck)

# Function to rank cards (Ace high, suit order: Hearts < Diamonds < Clubs < Spades)
def card_rank(card):
    value_order = {v: i for i, v in enumerate(values)}
    suit_order = {s: i for i, s in enumerate(suits)}
    
    # Ensure the card exists in our predefined values and suits
    value_rank = value_order.get(card[0])
    suit_rank = suit_order.get(card[1])

    if value_rank is None or suit_rank is None:
        raise ValueError(f"Invalid card found: {card}")

    return value_rank, suit_rank

# Sort deck based on rank
sorted_deck = sorted(deck, key=card_rank)

# Print shuffled and sorted deck
print("Shuffled Deck:", deck)
print("\nSorted Deck:", sorted_deck)
```

### Explanation of Fisher-Yates Algorithm

The Fisher-Yates algorithm, also known as the **Knuth shuffle**, is an efficient method for randomly shuffling an array. It works in **O(n) time complexity**, making it optimal for large datasets.

#### **Steps of the Fisher-Yates Algorithm**:

1. Start with an ordered list (the deck of cards in this case).
2. Iterate from the last index of the list down to the second index.
3. For each index `i`, pick a random index `j` (where `0 <= j <= i`).
4. Swap the elements at indices `i` and `j`.
5. Continue until the entire list is shuffled.

This ensures that every permutation of the array is equally likely, giving a perfectly randomized shuffle.
## **Explanation**

1. **Shuffling**: Uses `random.shuffle(deck)`, implementing **Fisher-Yates shuffle**.
2. **Sorting**:
    - Assigns numeric values to each rank and suit.
    - Sorts the deck based on **value first, then suit**.

#### **Python Implementation of Fisher-Yates Shuffle**

```python
import random

def fisher_yates_shuffle(deck):
    for i in range(len(deck) - 1, 0, -1):
        j = random.randint(0, i)
        deck[i], deck[j] = deck[j], deck[i]

deck = [(value, suit) for suit in suits for value in values]
fisher_yates_shuffle(deck)
print(deck)
```

### **Golang Implementation of Fisher-Yates Shuffle**

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func fisherYatesShuffle(deck []string) {
    rand.Seed(time.Now().UnixNano())
    for i := len(deck) - 1; i > 0; i-- {
        j := rand.Intn(i + 1)
        deck[i], deck[j] = deck[j], deck[i]
    }
}

func main() {
    suits := []string{"Hearts", "Diamonds", "Clubs", "Spades"}
    values := []string{"2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"}
    
    var deck []string
    for _, suit := range suits {
        for _, value := range values {
            deck = append(deck, value+" of "+suit)
        }
    }
    
    fisherYatesShuffle(deck)
    fmt.Println("Shuffled Deck:", deck)
}
```