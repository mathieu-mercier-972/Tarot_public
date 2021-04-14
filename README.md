import random
from random import randint


def cardDeck():
    color = ["D","H","C","S"]
    high_values = ["1","2","3","4","5","6","7","8","9","10","V","C","Q","K"]
    deck = [(x,y) for y in color for x in high_values]
    for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21]:
        deck.append(str(x))
    deck.append('fool')
    random.shuffle(deck)
    return deck


def distribution(listD):
    if listD == p1:
        for x in [0, 1, 2]:
            for y in [0, 12, 24, 36, 48, 60]:
                listD.append(finalDeck[x + y])
    if listD == p2:
        for x in [3, 4, 5]:
            for y in [0, 12, 24, 36, 48, 60]:
                listD.append(finalDeck[x + y])
    if listD == p3:
        for x in [6, 7, 8]:
            for y in [0, 12, 24, 36, 48, 60]:
                listD.append(finalDeck[x + y])
    if listD == p4:
        for x in [9, 10, 11]:
            for y in [0, 12, 24, 36, 48, 60]:
                listD.append(finalDeck[x + y])
    return listD


def draw(n, listA):
    for _ in range(n) :
        y = random.randint(0,75)  #j'ai mis entre 0 et 75 car il ne faut pas que les 3 dernières cartes du jeu soit distribuées dans le chien. non ? à verifier
        listA.append(finalDeck[y])
        finalDeck.remove(finalDeck[y])
    return listA


def card_classification():
    color = ["D","H","C","S"]
    high_values = ["1","2","3","4","5","6","7","8","9","10","V","C","Q","K"]
    deck = [(x,y) for y in color for x in high_values]
    for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21]:
        deck.append(str(x))
    deck.append('fool')

    number = []
    for x in range(79):
        x = x + 1
        number.append(x)
        
    classification = {x:y for x,y in zip(deck, number)}

    return classification


def reverse_card_classification():
    color = ["D","H","C","S"]
    high_values = ["1","2","3","4","5","6","7","8","9","10","V","C","Q","K"]
    deck = [(x,y) for y in color for x in high_values]
    for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21]:
        deck.append(str(x))
    deck.append('fool')

    number = []
    for x in range(79):
        x = x + 1
        number.append(x)

    reverse_classification = {x:y for x,y in zip(number, deck)}

    return reverse_classification


def card_sorted(listB):
    
    transformation = card_classification()
    reverse_transformation = reverse_card_classification()

    nb_sort = []
    for i in listB:
        nb_sort_i = transformation[i]
        nb_sort.append(nb_sort_i)
    nb_sort.sort()

    listC = []
    for j in nb_sort:
        card_sort_j = reverse_transformation[j]
        listC.append(card_sort_j)

    return listC


def player_choice_for_the_chien():

    card_chien = int(input(f"in the chien {chien} wich card do you want to take ? "))
    card_hand = int(input(f"which card in you hand {player_alone} do you want to replace ?"))

    card_chosen_from_the_chien = chien[card_chien]
    card_chosen_from_the_hand = player_alone[card_hand]

    chien.remove(card_chosen_from_the_chien)
    chien.append(card_chosen_from_the_hand)
    player_alone.remove(card_chosen_from_the_hand)
    player_alone.append(card_chosen_from_the_chien)

    return chien, player_alone


def creation_of_the_chien():
    print("\n\nBe careful! You cannot put an asset or a king in the chien."
    "\nTo replace a card in the chien or in your hand give the rank number of the card."
    "\nFrom 0 to 5 for the dog and from 0 to 17 for your deck.\n\n")
    m = 1
    while m == 1:

        print(player_choice_for_the_chien())

        transformation = card_classification()

        listG = []
        for i in chien:
            value_i = transformation[i]
            listG.append(value_i)

        m = 0
        for i in range(0,6):
            if listG[i] == 14 or listG[i] == 28 or listG[i] == 42 or listG[i] == 56:
                m = 1
            for n in range(57,79):
                if listG[i] == n:
                    m = 1

    end = str(input(f"\nyour hand is :{player_alone}\nand the chien is :{chien}\n\nIs it ok ?"))
    list(end.strip())

    while end[0] == "N" or end[0] == "n":

        print(player_choice_for_the_chien())

        end = str(input(f"\nyour hand is :{player_alone}\nand the chien is :{chien}\n\nIs it ok ?"))
        list(end.strip())
    
    return f"\n\n\n\nfinally the chien is {card_sorted(chien)}\nAnd your hand is {card_sorted(player_alone)}\n\n\n"


def list_transormation_nb(listB):
    
    transformation = card_classification()

    nb_list = []
    for i in listB:
        nb_list_i = transformation[i]
        nb_list.append(nb_list_i)
    
    return nb_list


def reverse_list_transormation_nb(listC):
    
    reverse_transformation = reverse_card_classification()
    
    list_card = []
    for j in listC:
        card = reverse_transformation[j]
        list_card.append(card)
        
    return list_card


def allowed_cards(hand, a, b):
    
    hand_number = list_transormation_nb(hand)

    pli_transormation_nb = list_transormation_nb(pli)
    allowed_cards = []

    for i in range(a, b):
        for j in range(0,len(hand)):
            if hand_number[j] == i:
                allowed_cards.append(hand_number[j])

    if allowed_cards == []:
        for i in range(57,79):
            for j in range(0,len(hand)):
                if hand_number[j] == i:
                    allowed_cards.append(hand_number[j])  

    return reverse_list_transormation_nb(allowed_cards)






# étape 1 : creation du jeu

p1 = []
p2 = []
p3 = []
p4 = []
chien = []
finalDeck = cardDeck()
print(f'final deck : {finalDeck}\n\n\n') 

# étape 2 : chien (en anglais ?)

chien = draw(6, chien) 
print(f'this is the "chien" : \n{chien}\n\n\n\n\n')

# étape 3 : distribution

i = 0
for j in [p1, p2, p3, p4]:
    i = i + 1
    print(f'Player {i} has \n{distribution(j)}\n\n')

# étape 3 bis : trier les cartes

print("\n\n\n\n\n\n\nCARDS SORTING :\n\n")
m = 0
for n in [p1, p2, p3, p4]:
    m = m + 1
    print(f'Player {m} cards sorted : \n{card_sorted(n)}\n\n')

p1 = card_sorted(p1)
p2 = card_sorted(p2)
p3 = card_sorted(p3)
p4 = card_sorted(p4)

# étape 4 : organisation du chien

for i in range(1,5):
    wich_player = i
    player_choice = str(input((f'player {i} do you want to take the "chien" ? (yes/no)')))
    list(player_choice.strip())
    if player_choice[0] == "Y" or player_choice[0] == "y" or player_choice[0] == "O" or player_choice[0] == "o":
        print("\nOK\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n")
        break

if player_choice[0] == "N" or player_choice[0] == "n":
    print('\n\n\nnobody wants to take the chien \nGAME OVER')
    wich_player = 5
    # mettre fin au jeu et commencer une autre partie

if wich_player == 1:
    player_alone = p1
elif wich_player == 2:
    player_alone = p2
elif wich_player == 3:
    player_alone = p3
elif wich_player == 4:
    player_alone = p4
elif wich_player == 5:
    player_alone = []
    chien = []

print(creation_of_the_chien())

if wich_player == 1:
    p1 = card_sorted(player_alone)
if wich_player == 2:
    p2 = card_sorted(player_alone)
if wich_player == 3:
    p3 = card_sorted(player_alone)
if wich_player == 4:
    p4 = card_sorted(player_alone)

# étape 5 : la partie commence

print('\n\n\n\n\n\n\n\n\n\n\n\n\n\nthe game begin ! \n')

for i in range(18):

    print(f'\n\n\nround {i+1}\n\n')
    m = 0
    u = -1
    pli = []

    for n in [p1, p2, p3, p4]:

        m = m + 1
        no_cards = 0
        pli_transormation_nb = list_transormation_nb(pli)

        if pli == []:
            n = allowed_cards(n, 1, 79)

        else:

            for i in range(1,15):
                if pli_transormation_nb[0] == i:
                    n = allowed_cards(n, 1, 15)
                else: no_cards = no_cards + 1

            for i in range(15,29):
                if pli_transormation_nb[0] == i:
                    n = allowed_cards(n, 15, 29)
                else: no_cards = no_cards + 1

            for i in range(29,43):
                if pli_transormation_nb[0] == i:
                    n = allowed_cards(n, 29, 43)
                else: no_cards = no_cards + 1

            for i in range(43,57):
                if pli_transormation_nb[0] == i:
                    n = allowed_cards(n, 43, 57)
                else: no_cards = no_cards + 1

            for i in range(57,79):                       
                if pli_transormation_nb[0] == i:
                    n = allowed_cards(n, 57, 79)
                else: no_cards = no_cards + 1

            if no_cards == 5:
                for i in range(57,79):
                    if pli_transormation_nb[0] == i:
                        n = allowed_cards(n, 57, 79)
                    else: n = allowed_cards(n, 1, 79)        #faire def pour bien jouer les atouts

        print(f'player {m} with your hand you can only play :\n{n}')

        pn_r = int(input("what do you want to choose ?"))
        pli.append(n[pn_r])
        card = n[pn_r]
        
        if m == 1: n = p1
        elif m == 2: n = p2
        elif m == 3: n = p3
        elif m == 4: n = p4

        n.remove(card)

        print(f'The current pli is :\n {pli}\n')       #comment on dit pli/levée en anglais ?


        #qui gagne ?
