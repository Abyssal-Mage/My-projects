# James Wagaman

rooms = {
    "1-Entry Hall": {
        "West": "2-Alchemist Lab",
        "East": "3-Barracks",
        "North": "4-Main Hall",
    },
    "2-Alchemist Lab": {"East": "1-Entry Hall"},
    "3-Barracks": {"West": "1-Entry Hall"},
    "4-Main Hall": {
        "North": "7-Display Room",
        "East": "9-Library",
        "South": "1-Entry Hall",
        "West": "5-Armory",
    },
    "5-Armory": {"North": "6-Treasury", "East": "4-Main Hall"},
    "6-Treasury": {"South": "5-Armory"},
    "7-Display Room": {"East": "8-Enchanter Circle", "South": "4-Main Hall"},
    "8-Enchanter Circle": {"West": "7-Display Room"},
    "9-Library": {"North": "10-Boss", "West": "4-Main Hall"},
    "10-Boss": {"South": "9-Library"},
}
room_discription = {
    "Entry Hall": {
        "item description": "You have arrived into the entry hall,\n"
        "the cobwebs make it seem deserted."
    },
    "Alchemist Lab": {
        "itemless description": "You walk through the door, see the empty\n"
                                "potion shelf and remember you looted here already.",
        "item description": "You walk through the door and see a cauldron,\n"
                            "some potions on the shelf, and various ingredients.",
    },
    "Barracks": {
        "itemless description": "You walk through the door, see the dead dragyr\n"
                                "and remember you looted here already.",
        "item description": "You walk through the door and see a magic orb\n"
                            "on a pedestal. It is guarded by a dragyr.",
    },
    "Main Hall": {
        "itemless description": "You walk through the door, there is a magic fog to the east,\n"
                                "and remember you looted here already.",
        "item description": "You walk through the door, there is a magic fog to the east,\n"
                            "and you see various weapons from unfortunate adventures.",
    },
    "Armory": {
        "itemless description": "You walk through the door, see nothing new.",
        "item description": "You walk through the door and see rusted\n"
                            "weapons and armor in piles around you.",
    },
    "Treasury": {
        "itemless description": "You walk through the door, see the sleeping mimic\n"
                                "and remember you looted here already.",
        "item description": "You walk through the door and see the Lich Kings\n"
                            "treasure stash. There are piles of gold and chests strewn about.",
    },
    "Display Room": {
        "itemless description": "You walk through the door, see no other useful items.",
        "item description": "You walk through the door and see rows of artifacts.\n"
                            "There is a magic sword on the wall.",
    },
    "Enchanter Circle": {
        "itemless description": "You walk through the door, see the faded magic\n"
                                "circle and remember you looted here already.",
        "item description": "You walk through the door, see a glowing magic circle\n"
                            "on the floor and a magic orb in the middle of it.",
    },
    "Library": {
        "itemless description": "You walk through the door, see the empty room.\n"
                                "North seems dangerous.",
        "item description": "You walk through the fog and see an amulet\n"
                            "in the center of the room. North seems dangerous.\n",
    },
    "Boss": {"item description": "The lich king is standing there. He attacks you"},
}

items = []
user_input = ""
current_room = "1-Entry Hall"



def instructions():
    print(
        "These are the instructions.\n",
        "Go to rooms, grab items and defeat the Lich King.\n",
        "To move use: North, East, South or West.\n",
        "To grab an item use: Item.\n",
        "-------------------------------------------------\n"

    )


def valid_input(user_input):
    user_input = input("What would you like to do?")
    while user_input != "Exit":
        if (  # check if input is direction or item
            user_input == "North"
            or user_input == "South"
            or user_input == "East"
            or user_input == "West"
            or user_input == "Item"
        ):
            return user_input
        else:  # start over
            user_input = input("Try again. What would you like to do?")
    if user_input == "Exit":  # checks if exit
        exit()  # Exit


def grab_item(current_room):
    if current_room == "2-Alchemist Lab":
        if "Sleep Draught" in items:
            return
        else:
            print("You browse the shelves and find a usable potion.\n")
            items.append("Sleep Draught")
    if current_room == "3-Barracks":
        if "Orb of Courage" in items:
            return
        if ("Shield" in items) and ("Dagger" in items):
            print("You fight off the Dragyr. Your Dagger and Shield Break.\n")
            items.remove("Dagger")
            items.remove("Shield")
            items.append("Orb of Courage")
        else:
            print("The Dragyr fought you off, come back with weapons.\n")
    if current_room == "4-Main Hall":
        if "Dagger" in items:
            return
        else:
            print(
                "You grab a bloodstained dagger left behind. The owner won't miss it.\n"
            )
            items.append("Dagger")
    if current_room == "5-Armory":
        if "Shield" in items:
            return
        else:
            print("You rummage around and find a usable Shield.\n")
            items.append("Shield")
    if current_room == "6-Treasury":
        if "Orb of Wisdom" in items:
            return
        if "Sleep Draught" in items:
            print(
                "You open a chest and find its a mimic!\n",
                "You drop your Sleep Draught on accident.\n",
                "The mimic falls asleep and an orb rolls by.\n",
                "You grab the orb.\n",
            )
            items.remove("Sleep Draught")
            items.append("Orb of Wisdom")
    if current_room == "7-Display Room":
        if "Magic Sword" in items:
            return
        else:
            print("You grab the Magic Sword. It radiates power.\n")
            items.append("Magic Sword")
    if current_room == "8-Enchanter Circle":
        if "Orb of Power" in items:
            return
        else:
            print("You grab the orb from the Enchanter Circle.\n", "The circle dims.\n")
            items.append("Orb of Power")
    if current_room == "9-Library":
        if "Amulet" in items:
            return
        else:
            print("You break the glass and grab the shiny Amulet.\n")
            items.append("Amulet")


def movement(current_room):
    while current_room != "1-Boss":  # Validate room is in dictionary
        print("{} is the current room".format(current_room))
        print(room_disc(current_room))  # prints current rooms description
        print("Items:", items)  # prints current items
        print("You can move:", rooms[current_room])
        print("Grab 'Item'")
        print("Or Exit")
        direction = valid_input(user_input)  # check for direction or Item
        if (
            (current_room == "4-Main Hall")
            and ("Orb of Courage" not in items)
            and (direction == "East")
        ):  # blocks fog wall
            print(
                "You walk through the fog wall, but you walk back into the Main Hall.\n"
            )
            continue
        if direction == "Item":  # grab item if input is Item
            grab_item(current_room)
            print("--------------------------------------\n")  # Space the lines
        else:
            if direction not in rooms[current_room]:  # checks if you can move direction
                print("Can't move there. \n")
                continue
            print("You moved", direction)  # move rooms
            current_room = rooms[current_room][direction]  # get dictionary value
            print("--------------------------------------\n")  # Space the lines


def room_disc(current_room):  # checks if items are in list and chooses item or itemless description
    if current_room == "1-Entry Hall":
        print(room_discription["Entry Hall"]["item description"])
    elif current_room == "2-Alchemist Lab":
        if "Sleep Draught" in items:
            print(room_discription["Alchemist Lab"]["itemless description"])
        else:
            print(room_discription["Alchemist Lab"]["item description"])
    elif current_room == "3-Barracks":
        if "Orb of Courage" in items:
            print(room_discription["Barracks"]["itemless description"])
        else:
            print(room_discription["Barracks"]["item description"])
    elif current_room == "4-Main Hall":
        if "Dagger" in items:
            print(room_discription["Main Hall"]["itemless description"])
        else:
            print(room_discription["Main Hall"]["item description"])
    elif current_room == "5-Armory":
        if "Shield" in items:
            print(room_discription["Armory"]["itemless description"])
        else:
            print(room_discription["Armory"]["item description"])
    elif current_room == "6-Treasury":
        if "Orb of Wisdom" in items:
            print(room_discription["Treasury"]["itemless description"])
        else:
            print(room_discription["Treasury"]["item description"])
    elif current_room == "7-Display Room":
        if "Magic Sword" in items:
            print(room_discription["Display Room"]["itemless description"])
        else:
            print(room_discription["Display Room"]["item description"])
    elif current_room == "8-Enchanter Circle":
        if "Orb of Power" in items:
            print(room_discription["Enchanter Circle"]["itemless description"])
        else:
            print(room_discription["Enchanter Circle"]["item description"])
    elif current_room == "9-Library":
        if "Amulet" in items:
            print(room_discription["Library"]["itemless description"])
        else:
            print(room_discription["Library"]["item description"])
    else:
        print(room_discription["Boss"]["item description"])
        if (
            ("Orb of Courage" in items)
            and ("Orb of Power" in items)
            and ("Orb of Wisdom" in items)
            and ("Amulet" in items)
            and ("Magic Sword" in items)
        ):  # checks for every Item
            print(
                "The Amulet protected you from his attck.\n",
                "The Orbs gather around your body.\n",
                "You swing a powered attack with your sword.\n",
                "The Lich King dies!\n",
            )
            exit()
        else:
            print("You were unprepared and died.\n", "GAME OVER")
            exit()


def main():
    instructions()
    while True:
        movement(current_room)

main()
