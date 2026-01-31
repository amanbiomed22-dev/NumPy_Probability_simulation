# Complete Project Explanation

## *Clash Royale Perfect Deck Probability Simulator*

---

## Project Overview

This project is a **Python-based probability and Monte Carlo simulation** inspired by the deck-building mechanics of the mobile game **Clash Royale**.

In Clash Royale, players build an **8-card battle deck** from a pool of **121 available cards**, each belonging to different categories such as **Evolution**, **Champion**, **Hero**, and **Other cards**.

The objective of this project is to:

* Define what a **“perfect deck”** means under strict rules
* Calculate the **exact mathematical probability** of obtaining such a deck
* Simulate **random deck generation** using Monte Carlo methods
* Allow users to **interactively try their luck** in generating a perfect deck

---

## Motivation Behind the Project

Many players believe that repeatedly generating random decks will eventually produce an ideal or “perfect” deck.

However, human intuition often **underestimates how rare certain combinations are**.

This project was created to:

* Demonstrate how **probability theory applies to real games**
* Show the difference between **intuition and actual odds**
* Use **random simulation** to validate mathematical results
* Provide an **educational yet engaging** learning experience

---

##  Deck Categories and Constraints

The game consists of **121 total cards**, divided into four main categories:

| Category        | Number of Cards |
| --------------- | --------------- |
| Evolution Cards | 39              |
| Champion Cards  | 8               |
| Hero Cards      | 6               |
| Other Cards     | 68              |

Champion and Hero cards are treated as a **single combined category** during deck validation.

---

##  Definition of a Perfect Deck

A deck is considered **perfect** if it satisfies **all** of the following conditions:

| Category              | Required Count |
| --------------------- | -------------- |
| Evolution Cards       | 2              |
| Champion / Hero Cards | 2              |
| Other Cards           | 4              |
| **Total Cards**       | **8**          |

Any deck that does not meet **exactly** this pattern is rejected.

---

##  Mathematical Probability Calculation

###  Combinatorics Used

The project uses **combinations (nCr)** to compute probabilities, where:

[
nCr = \frac{n!}{r!(n-r)!}
]

###  Favorable Outcomes

The number of favorable decks is calculated as:

* Choosing 2 Evolutions from 39
* Choosing 2 Champions/Heroes from 14
* Choosing 4 Other cards from 68

[
\binom{39}{2} \times \binom{14}{2} \times \binom{68}{4}
]

###  Total Possible Decks

Any 8 cards can be chosen from 121:

[
\binom{121}{8}
]

###  Final Probability

[
P = \frac{\text{Favorable Decks}}{\text{Total Decks}}
]

The program converts this probability into:

* Decimal probability
* Percentage chance
* “1 in N decks” explanation for easier understanding

---

##  Monte Carlo Simulation Approach

Rather than generating decks that already follow the perfect pattern, the project uses a **true Monte Carlo simulation**:

* Cards are selected **randomly** from all 121 cards
* No card can repeat in a deck (`replace=False`)
* Each deck is checked after generation
* The process is repeated across multiple attempts

This ensures:

* **Unbiased randomness**
* **Realistic simulation of game mechanics**
* Results that match theoretical probability over time

---

##  Randomness and Fairness

Randomness is implemented using:

```python
np.random.choice(ALL_CARDS, 8, replace=False)
```

Key properties:

* Every card has an equal chance of selection
* No duplicates in a single deck
* No forced pattern or bias
* Results differ on every run

This accurately reflects **real-world random deck generation**.

---

##  Game Flow and User Interaction

1. The program displays the **perfect deck format**
2. Probability results are shown automatically
3. The player is invited to try their luck
4. The user gets **5 attempts per round**
5. Each attempt:

   * Generates a new random deck
   * Displays cards slot-wise
   * Validates the deck
6. The game ends when:

   * A perfect deck is achieved, or
   * All attempts are exhausted
7. The user may restart the game after each round

---

##  Key Functions Explained

### `generate_random_deck()`

Generates a truly random 8-card deck from all available cards.

### `is_perfect_deck(deck)`

Checks whether the deck satisfies the exact category requirements.

### `calculate_probability()`

Computes the theoretical probability using combinatorics.

### `nCr(n, r)`

Calculates combinations using Python’s `math.comb()` for accuracy and efficiency.

---

##  Technologies Used

* **Python 3**
* **NumPy** (random sampling)
* **Math module** (combinatorics)
* Terminal-based user interface

---

##  Conclusion

This project proves that:

> Even though a perfect deck is possible, its probability is extremely low.

It highlights how **randomness, probability, and persistence** interact in games and real-world systems.

By combining **mathematical rigor** with **interactive simulation**, the project offers both **educational value** and **engaging gameplay**.

---

## ⭐ Final Takeaway

> *“Luck feels powerful, but mathematics tells the truth.”*
