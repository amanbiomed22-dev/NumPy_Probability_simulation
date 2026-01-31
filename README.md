# NumPy_Probability_simulation
A Python-based Monte Carlo simulation that calculates and demonstrates the probability of generating a perfect Clash Royale deck using combinatorics and randomness.


import numpy as np
import math

# ===============================
# CARD DATA
# ===============================

evolution_cards = [
    "Archers","Baby Dragon","Barbarians","Bats","Battle Ram","Bomber","Cannon",
    "Dart Goblin","Electro Dragon","Executioner","Firecracker","Furnace",
    "Goblin Barrel","Goblin Cage","Goblin Drill","Goblin Giant","Giant Snowball",
    "Hunter","Ice Spirit","Inferno Dragon","Knight","Lumberjack","Mega Knight",
    "Mortar","Musketeer","P.E.K.K.A.","Royal Giant","Royal Recruits","Royal Hogs",
    "Skeletons","Skeleton Army","Tesla","Valkyrie","Wall Breakers","Witch",
    "Wizard","Zap","Skeleton Barrel","Royal Ghost"
]

champions = [
    "Archer Queen","Golden Knight","Skeleton King","Mighty Miner",
    "Monk","Little Prince","Goblinstein","Boss Bandit"
]

heroes = [
    "Hero Knight","Hero Giant","Hero Mini P.E.K.K.A.",
    "Hero Musketeer","Hero Ice Golem","Hero Wizard"
]

other_cards = [
    "Arrows","Barbarian Barrel","Bomb Tower","Bowler","Clone","Dark Prince",
    "Earthquake","Electro Giant","Electro Spirit","Electro Wizard",
    "Elite Barbarians","Fireball","Fire Spirit","Freeze","Goblin Curse",
    "Goblin Gang","Goblin Hut","Goblin Machine","Goblins","Guards","Heal Spirit",
    "Inferno Tower","Lightning","Mirror","Minion Horde","Minions","Prince",
    "Princess","Rocket","Rage","Royal Delivery","Skeleton Dragons",
    "Spear Goblins","Spirit Empress","Suspicious Bush","Tombstone","Tornado",
    "Void","Vines","X-Bow","Elixir Collector","Fisherman","Giant Skeleton",
    "Ice Wizard","Mother Witch","Night Witch","Phoenix","Ram Rider","Rascals",
    "Three Musketeers","Balloon","Elixir Golem","Battle Healer",
    "Rune Giant","Berserker","Goblin Demolisher","Cannon Cart"
]

ALL_CARDS = evolution_cards + champions + heroes + other_cards

# ===============================
# MATHEMATICS
# ===============================

def nCr(n, r):
    return math.comb(n, r)

def calculate_probability():
    favorable = nCr(39, 2) * nCr(14, 2) * nCr(68, 4)
    total = nCr(121, 8)
    return favorable / total

# ===============================
# RANDOM DECK
# ===============================

def generate_random_deck():
    return list(np.random.choice(ALL_CARDS, 8, replace=False))

def is_perfect_deck(deck):
    evo = sum(card in evolution_cards for card in deck)
    champ_hero = sum(card in champions + heroes for card in deck)
    others = sum(card in other_cards for card in deck)
    return evo == 2 and champ_hero == 2 and others == 4

# ===============================
# DISPLAY FUNCTIONS
# ===============================

def show_example_layout():
    print("\n🟪🟪🟨🟨🟦🟦🟦🟦  PERFECT DECK FORMAT\n")
    print("Slot 1 (Evolution)")
    print("Slot 2 (Evolution)")
    print("Slot 3 (Champion / Hero)")
    print("Slot 4 (Champion / Hero)")
    print("Slot 5 (Other Card)")
    print("Slot 6 (Other Card)")
    print("Slot 7 (Other Card)")
    print("Slot 8 (Other Card)")

def show_instructions():
    print("\n📜 INSTRUCTIONS 📜")
    print("• Total attempts: 5")
    print("• Press ENTER before each attempt")
    print("• Perfect pattern required:")
    print("  2 Evolution | 2 Champion/Hero | 4 Other\n")

# ===============================
# GAME START
# ===============================

print("\n🎮 WELCOME TO CLASH ROYALE PERFECT DECK GAME 🎮")
show_example_layout()

# Probability shown automatically
prob = calculate_probability()
percentage = prob * 100
odds = int(1 / prob)

print(f"\n📊 Probability of getting a perfect deck: {percentage:.4f}%")
print(f"🎯 Meaning: On average, ONE perfect deck appears after about {odds:,} random decks.")

print("\n🔥 LET'S TRY YOUR LUCK 🔥")

# ===============================
# MAIN GAME LOOP
# ===============================

while True:
    show_instructions()

    messages = {
        1: "😬 Warm-up round!",
        2: "⚔️ Still fighting!",
        3: "🔥 RNG is testing you!",
        4: "💥 Last push!",
        5: "💔 Tough luck!"
    }

    for attempt in range(1, 6):
        input(f"\n➡ Press ENTER to try Attempt {attempt}/5...")

        deck = generate_random_deck()

        print("\n🃏 GENERATED DECK:")
        slot_names = [
            "🟪Slot 1","🟪Slot 2","🟨Slot 3","🟨Slot 4",
            "🟦Slot 5","🟦Slot 6","🟦Slot 7","🟦Slot 8"
        ]

        for slot, card in zip(slot_names, deck):
            print(f"{slot}: {card}")

        if is_perfect_deck(deck):
            print("\n🎉🎉 PERFECT DECK ACHIEVED! 🎉🎉")
            print("👑 You beat the odds — absolute legend!")
            break
        else:
            if attempt < 5:
                print(f"\n❌ Not this time… {5-attempt}/5 chances left.")
                print(messages[attempt])
            else:
                print("\n❌ No chances left!")
                print("🌟 Probability is low — persistence is high!")

    restart = input("\n🔁 Restart from instructions? (Y/N): ").upper()
    if restart != "Y":
        print("\n🙏 Thank you for playing. Stay legendary!")
        break
