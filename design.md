Weekend At Byakuyas Design Documentation
========================================

This is a document dictating the general design of the game logic and data storage for weekend at Byakuyas.

Item JSON Information:
======================

Items will be stored in a map of their name to the object holding the item's information.

Item:
-----

{
  "name": String,
  "sprite": String
  "type": String, // light, medium, heavy, or immovable
  "uses": Uses,
  "attributes": [String],
  "interactions": {
    <String Character>: {
      "text": String
      "effects": [Effect]
    }
  },
  "suspicion": {
    "on-person-before-crime": Float,
    "on-person-after-crime": Float,
    "in-room-before-crime": Float,
    "in-room-after-crime": Float,
    "links-to": {
      <String character>: Float
    }
  }
}

Examples of items:

{
  "name": "bat",
  "weight" "medium",
  "uses": {
    "destructable": [{
      "name": "destroy-target",
      "data": []
    }]
  },
  "attributes": [
    "weapon"
  ],
  "interactions" {
    "togami": {
      "text": "It's a standard baseball bat.",
      "effects": []
    }
  }
}

Uses:
-----

{
  <String attribute>: [Effect]
}

Special attributes:

-- __PLAYER__ (when an item is used on the player)
-- __CHARACTER__ (when an item is used on a character)

Effect:
-----------

{
  "name": String,
  "data": [Object]
}

Some effect names are:

- "destroy-self"
- "destroy-target"
- "blunt-traum"
- "stab-wound"
- "create-item"

Inventory System
================

The inventory is a list of item names.

Items fall into one of three categories.

Items fall into one of three type categories:

- light
- medium
- heavy
- immovable

Light Items
-----------

You can carry up to six light items. No one will find these unless they actively try to search you.

Medium Items
------------

You can carry two medium items in your hands, but these will be seen by everyone. With a bag, you can carry up to four, but characters will take note of the fact that you're carrying a bag.

Heavy Items
-----------

You can carry one heavy item. Everyone who sees you will know that you have it on you.

Immovable
---------

An immovable item cannot be moved.

Character JSON Information:
===========================

{
  "name": String,
  "sprites": [String],
  "trust": {
    "<String character>": Float
  },
  "frequent-locations": [<String location>],
  "wakes-up": Integer,
  "sleeps": Integer,
  "strength": Float,
  "intelligence": Float,
  "luck": Boolean
}

