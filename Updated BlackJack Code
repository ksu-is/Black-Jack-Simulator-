# Blackjack Simulator Updates
# Improved version with added comments and functionality
# Roadmap: Basic structure, key actions, probability calculations
-----------------------------------------------------------------

import random
import time

# Constants for suits, ranks, and values
suits = ("Spades ♠", "Clubs ♣", "Hearts ♥", "Diamonds ♦")
ranks = ("2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A")
values = {
    "2": 2,
    "3": 3,
    "4": 4,
    "5": 5,
    "6": 6,
    "7": 7,
    "8": 8,
    "9": 9,
    "10": 10,
    "J": 10,
    "Q": 10,
    "K": 10,
    "A": 11,  # Aces can also be 1 (adjusted dynamically)
}

playing = True  # Global flag for gameplay state

# Classes


class Card:
    """Represents a single card in the deck."""

    def __init__(self, suit, rank):
        self.suit = suit
        self.rank = rank

    def __str__(self):
        return f"{self.rank} of {self.suit}"


class Deck:
    """Represents the deck of cards."""

    def __init__(self):
        self.deck = [Card(suit, rank) for suit in suits for rank in ranks]

    def shuffle(self):
        """Shuffles the deck."""
        random.shuffle(self.deck)

    def deal(self):
        """Deals a single card from the deck."""
        return self.deck.pop()


class Hand:
    """Represents a player's hand."""

    def __init__(self):
        self.cards = []  # Cards in the hand
        self.value = 0   # Total value of the hand
        self.aces = 0    # Count of aces in the hand

    def add_card(self, card):
        """Adds a card to the hand and adjusts value for aces."""
        self.cards.append(card)
        self.value += values[card.rank]
        if card.rank == "A":
            self.aces += 1
        self.adjust_for_ace()

    def adjust_for_ace(self):
        """Adjusts hand value if an ace causes the hand to exceed 21."""
        while self.value > 21 and self.aces:
            self.value -= 10
            self.aces -= 1


# Functions


def hit(deck, hand):
    """Handles the 'Hit' action."""
    hand.add_card(deck.deal())


def hit_or_stand(deck, hand):
    """Prompts player to Hit or Stand."""
    global playing

    while True:
        action = input("\nWould you like to Hit or Stand? Enter [h/s]: ").lower()

        if action == "h":
            hit(deck, hand)
        elif action == "s":
            print("Player stands. Dealer is playing.")
            playing = False
        else:
            print("Invalid input. Please enter 'h' or 's'.")
            continue
        break


def show_some(player, dealer):
    """Displays partial dealer hand and full player hand."""
    print("\nPlayer's Hand:", *player.cards, sep="\n ")
    print("Player's Hand Value =", player.value)
    print("\nDealer's Hand:")
    print(" <card hidden>")
    print("", dealer.cards[1])


def show_all(player, dealer):
    """Displays all cards for both player and dealer."""
    print("\nPlayer's Hand:", *player.cards, sep="\n ")
    print("Player's Hand Value =", player.value)
    print("\nDealer's Hand:", *dealer.cards, sep="\n ")
    print("Dealer's Hand Value =", dealer.value)


# Outcome Functions


def player_busts():
    print("\n--- Player busts! ---")


def player_wins():
    print("\n--- Player wins! ---")


def dealer_busts():
    print("\n--- Dealer busts! You win! ---")


def dealer_wins():
    print("\n--- Dealer wins! ---")


def push():
    print("\n--- It's a tie! ---")


# Main Gameplay Loop

while True:
    print("\n---------------------------------------------------------------")
    print("               ♠♣♥♦ WELCOME TO BLACKJACK! ♠♣♥♦")
    print("---------------------------------------------------------------")
    print(
        "Rules: Get as close to 21 as possible without going over.\n"
        "Dealer hits until they reach 17. Aces count as 1 or 11.\n"
    )

    # Initialize the deck and hands
    deck = Deck()
    deck.shuffle()

    player_hand = Hand()
    dealer_hand = Hand()

    for _ in range(2):  # Deal two cards each to player and dealer
        player_hand.add_card(deck.deal())
        dealer_hand.add_card(deck.deal())

    # Show initial hands
    show_some(player_hand, dealer_hand)

    # Player's turn
    while playing:
        hit_or_stand(deck, player_hand)
        show_some(player_hand, dealer_hand)

        if player_hand.value > 21:
            player_busts()
            break

    # Dealer's turn
    if player_hand.value <= 21:
        while dealer_hand.value < 17:
            hit(deck, dealer_hand)

        # Display results
        print("\nFinal Results:")
        show_all(player_hand, dealer_hand)

        if dealer_hand.value > 21:
            dealer_busts()
        elif dealer_hand.value > player_hand.value:
            dealer_wins()
        elif dealer_hand.value < player_hand.value:
            player_wins()
        else:
            push()

    # Ask to play again
    new_game = input("\nPlay another hand? [y/n]: ").lower()
    if new_game == "y":
        playing = True
        continue
    else:
        print("\nThanks for playing!")
        break
