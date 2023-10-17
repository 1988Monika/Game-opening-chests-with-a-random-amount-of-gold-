# Game-opening-chests-with-a-random-amount-of-gold-
"""A short game in which you have 5 moves in one direction through the CHAMBER. Each time you have a chance to encounter a box or NOTHING along the way.

The boxes have different colors.

The color of the box indicates how rare the box is.

green - 75%
orange - 20%
purple - 4%
gold (legendary) - 1%

You have a 40% chance of encountering nothing. 60% that there will be a box.

Winnings you can get:
green - 1000,
orange - 4000,
purple - 9000,
gold - 16,000
"""
import random
from enum import Enum

Event = Enum('Event', ['Chest', 'Empty'])

eventDictionary = {
                    Event.Chest: 0.6,
                    Event.Empty: 0.4
                  }
eventList = tuple(eventDictionary.keys())
eventProbability = tuple(eventDictionary.values())


Colours = Enum('Colours', {'Green': 'green',
                           'Orange': 'orange',
                           'Purple': 'purple',
                           'Gold': 'goldye'
                          }
               )

chestColoursDictionary = {
                            Colours.Green :  0.75,
                            Colours.Orange : 0.2,
                            Colours.Purple : 0.04,
                            Colours.Gold : 0.01
                         }
chestColourList = tuple(chestColoursDictionary.keys())
chestColourProbability = tuple(chestColoursDictionary.values())

rewardsForChests = {
                       chestColourList[reward]: (reward + 1) * (reward + 1) * 1000
                       for reward in range(len(chestColourList))
                   }

gameLength = 5
goldAcquired = 0

print("Welcome in my game called KOMNATA")
print("""You have only 5 steps to make,
see yourself how much gold you gonna acquire till the end!""")

while gameLength > 0:
    gamerAnswer = input("Do you want to move forward?")
    if (gamerAnswer == "yes"):
        print("Great, let's see what you got...")
        drawnEvent = random.choices(eventList,eventProbability)[0]
        if (drawnEvent == Event.Chest):
            print("You've drawn a CHEST")
            drawnColour = random.choices(chestColourList,chestColourProbability)[0]
            print("The chest color is", drawnColour.value)
            gamerReward = rewardsForChests[drawnColour]
            goldAcquired = goldAcquired + gamerReward
        elif(drawnEvent == Event.Empty):
            print("You've drawn nothing, you are so unlucky!")
            
    else:
        print("You can go just straight man, nothing else, this game is dumb")
        continue
    
    gameLength = gameLength - 1

print("Congratulation, you have acquired: ", goldAcquired)
