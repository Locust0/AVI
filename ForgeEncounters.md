- [HOME](https://avijr.com)

---

# The Forge Encounters Prefab

The task I was initially given was to create a highly reusable prefab which could be placed into the world and changed easily wherever the encounter needed to take place. I did this by creating a pattern of fighting areas which looks like the following image:

![Output sample](https://github.com/Polaros/AVI/raw/master/images/SabateurEncounter.png)

The main boss (the Forge Saboteur) inhabits the red center of each position. That boss's protection initially inhabits the green outer ring until their numbers are thinned. They retreat to the yellow ring, and if further pressed, the red center.

When the boss's health is significantly damaged or his protection is significantly picked off, they will all retreat to the next formation and the boss's protection will take their places back at the outer ring. The same process will then repeat until the final formation.

From the final formation, the boss cannot retreat. Notably, its impossible for the boss to retreat to this final position unless it's significantly wounded.

### Why Rings?

The boss's protection are assigned to rings for a simple reason. They are programmed to take the closest position to the player that they can. The result of this and their ring is that they will always place themselves between the player and the boss. The ring is further subdivided into sections (not pictured) to prevent the enemies from clumping to closely together.

This formation will also accommodate multiple players because a couple enemies will choose to target any other players, spreading out and placing themselves between them and that player.

### How is this used?

These rings were placed into the world in 4 locations: 2 in the EDZ and 2 on Nessus. The design of the ringed retreats meant that I could place the second and third formation in better and better positions so the boss would appear to retreat to a better area when damaged. The actual boss and group of enemies protecting them were all exchanged appropriately depending on the area.

### How were these encounters used?

These 4 encounters were the preamble to the Black Armory DLC. They guard boxes which drop weapon frames needed for Black Armory weapon quests. The bosses also drop high level loot which is sometimes colored with the Black Armory colors. These encounters were farmed by players repeatedly because they were released before the rest of the DLC.

### The Black Armory Shield

These shields described [here](https://avijr.com/Destiny), were added to all of the forge saboteur bosses to increase their difficulty and introduce players to this new mechanic which is featured in the forges themselves and the quests to unlock them.

---

- [HOME](https://avijr.com)
