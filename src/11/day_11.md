---
title: Day 11 - Advent of Code 2022
date: 11/12/2022
author: Jeb
h1: Advent of Code 2022 - Day 11
href: https://adventofcode.com/2022/day/11

HeaderLink:

- {text: Previous day, link: /day_10.html}
- {text: Next day, link: /day_12.html}

FooterLink:

- {text: Previous day, link: /day_10.html}
- {text: Next day, link: /day_12.html}

---

## Challenge

### --- Day 11: Monkey in the Middle ---

As you finally start making your way upriver, you realize your pack is much lighter than you remember. Just then, one of
the items from your pack goes flying overhead. Monkeys are playing Keep Away with your missing things!

To get your stuff back, you need to be able to predict where the monkeys will throw your items. After some careful
observation, you realize the monkeys operate based on **how worried you are about each item**.

You take some notes (your puzzle input) on the items each monkey currently has, how worried you are about those items,
and how the monkey makes decisions based on your worry level. For example:

````
Monkey 0:
  Starting items: 79, 98
  Operation: new = old * 19
  Test: divisible by 23
    If true: throw to monkey 2
    If false: throw to monkey 3

Monkey 1:
  Starting items: 54, 65, 75, 74
  Operation: new = old + 6
  Test: divisible by 19
    If true: throw to monkey 2
    If false: throw to monkey 0

Monkey 2:
  Starting items: 79, 60, 97
  Operation: new = old * old
  Test: divisible by 13
    If true: throw to monkey 1
    If false: throw to monkey 3

Monkey 3:
  Starting items: 74
  Operation: new = old + 3
  Test: divisible by 17
    If true: throw to monkey 0
    If false: throw to monkey 1
````

Each monkey has several attributes:

- `Starting items` lists your **worry level** for each item the monkey is currently holding in the order they will be
  inspected.
- `Operation` shows how your worry level changes as that monkey inspects an item. (An operation like `new = old * 5`
  means that your worry level after the monkey inspected the item is five times whatever your worry level was before
  inspection.)
- `Test` shows how the monkey uses your worry level to decide where to throw an item next.
    - `If true` shows what happens with an item if the `Test` was true.
    - `If false` shows what happens with an item if the `Test` was false.

After each monkey inspects an item but before it tests your worry level, your relief that the monkey's inspection didn't
damage the item causes your worry level to be **divided by three** and rounded down to the nearest integer.

The monkeys take turns inspecting and throwing items. On a single monkey's **turn**, it inspects and throws all the
items it is holding one at a time and in the order listed. Monkey `0` goes first, then monkey `1`, and so on until each
monkey has had one turn. The process of each monkey taking a single turn is called a **round**.

When a monkey throws an item to another monkey, the item goes on the **end** of the recipient monkey's list. A monkey
that starts a round with no items could end up inspecting and throwing many items by the time its turn comes around. If
a monkey is holding no items at the start of its turn, its turn ends.

In the above example, the first round proceeds as follows:

````
Monkey 0:
  Monkey inspects an item with a worry level of 79.
    Worry level is multiplied by 19 to 1501.
    Monkey gets bored with item. Worry level is divided by 3 to 500.
    Current worry level is not divisible by 23.
    Item with worry level 500 is thrown to monkey 3.
  Monkey inspects an item with a worry level of 98.
    Worry level is multiplied by 19 to 1862.
    Monkey gets bored with item. Worry level is divided by 3 to 620.
    Current worry level is not divisible by 23.
    Item with worry level 620 is thrown to monkey 3.
Monkey 1:
  Monkey inspects an item with a worry level of 54.
    Worry level increases by 6 to 60.
    Monkey gets bored with item. Worry level is divided by 3 to 20.
    Current worry level is not divisible by 19.
    Item with worry level 20 is thrown to monkey 0.
  Monkey inspects an item with a worry level of 65.
    Worry level increases by 6 to 71.
    Monkey gets bored with item. Worry level is divided by 3 to 23.
    Current worry level is not divisible by 19.
    Item with worry level 23 is thrown to monkey 0.
  Monkey inspects an item with a worry level of 75.
    Worry level increases by 6 to 81.
    Monkey gets bored with item. Worry level is divided by 3 to 27.
    Current worry level is not divisible by 19.
    Item with worry level 27 is thrown to monkey 0.
  Monkey inspects an item with a worry level of 74.
    Worry level increases by 6 to 80.
    Monkey gets bored with item. Worry level is divided by 3 to 26.
    Current worry level is not divisible by 19.
    Item with worry level 26 is thrown to monkey 0.
Monkey 2:
  Monkey inspects an item with a worry level of 79.
    Worry level is multiplied by itself to 6241.
    Monkey gets bored with item. Worry level is divided by 3 to 2080.
    Current worry level is divisible by 13.
    Item with worry level 2080 is thrown to monkey 1.
  Monkey inspects an item with a worry level of 60.
    Worry level is multiplied by itself to 3600.
    Monkey gets bored with item. Worry level is divided by 3 to 1200.
    Current worry level is not divisible by 13.
    Item with worry level 1200 is thrown to monkey 3.
  Monkey inspects an item with a worry level of 97.
    Worry level is multiplied by itself to 9409.
    Monkey gets bored with item. Worry level is divided by 3 to 3136.
    Current worry level is not divisible by 13.
    Item with worry level 3136 is thrown to monkey 3.
Monkey 3:
  Monkey inspects an item with a worry level of 74.
    Worry level increases by 3 to 77.
    Monkey gets bored with item. Worry level is divided by 3 to 25.
    Current worry level is not divisible by 17.
    Item with worry level 25 is thrown to monkey 1.
  Monkey inspects an item with a worry level of 500.
    Worry level increases by 3 to 503.
    Monkey gets bored with item. Worry level is divided by 3 to 167.
    Current worry level is not divisible by 17.
    Item with worry level 167 is thrown to monkey 1.
  Monkey inspects an item with a worry level of 620.
    Worry level increases by 3 to 623.
    Monkey gets bored with item. Worry level is divided by 3 to 207.
    Current worry level is not divisible by 17.
    Item with worry level 207 is thrown to monkey 1.
  Monkey inspects an item with a worry level of 1200.
    Worry level increases by 3 to 1203.
    Monkey gets bored with item. Worry level is divided by 3 to 401.
    Current worry level is not divisible by 17.
    Item with worry level 401 is thrown to monkey 1.
  Monkey inspects an item with a worry level of 3136.
    Worry level increases by 3 to 3139.
    Monkey gets bored with item. Worry level is divided by 3 to 1046.
    Current worry level is not divisible by 17.
    Item with worry level 1046 is thrown to monkey 1.
````

After round 1, the monkeys are holding items with these worry levels:

````
Monkey 0: 20, 23, 27, 26
Monkey 1: 2080, 25, 167, 207, 401, 1046
Monkey 2: 
Monkey 3: 
````

Monkeys 2 and 3 aren't holding any items at the end of the round; they both inspected items during the round and threw
them all before the round ended.

This process continues for a few more rounds:

````
After round 2, the monkeys are holding items with these worry levels:
Monkey 0: 695, 10, 71, 135, 350
Monkey 1: 43, 49, 58, 55, 362
Monkey 2: 
Monkey 3: 

After round 3, the monkeys are holding items with these worry levels:
Monkey 0: 16, 18, 21, 20, 122
Monkey 1: 1468, 22, 150, 286, 739
Monkey 2: 
Monkey 3: 

After round 4, the monkeys are holding items with these worry levels:
Monkey 0: 491, 9, 52, 97, 248, 34
Monkey 1: 39, 45, 43, 258
Monkey 2: 
Monkey 3: 

After round 5, the monkeys are holding items with these worry levels:
Monkey 0: 15, 17, 16, 88, 1037
Monkey 1: 20, 110, 205, 524, 72
Monkey 2: 
Monkey 3: 

After round 6, the monkeys are holding items with these worry levels:
Monkey 0: 8, 70, 176, 26, 34
Monkey 1: 481, 32, 36, 186, 2190
Monkey 2: 
Monkey 3: 

After round 7, the monkeys are holding items with these worry levels:
Monkey 0: 162, 12, 14, 64, 732, 17
Monkey 1: 148, 372, 55, 72
Monkey 2: 
Monkey 3: 

After round 8, the monkeys are holding items with these worry levels:
Monkey 0: 51, 126, 20, 26, 136
Monkey 1: 343, 26, 30, 1546, 36
Monkey 2: 
Monkey 3: 

After round 9, the monkeys are holding items with these worry levels:
Monkey 0: 116, 10, 12, 517, 14
Monkey 1: 108, 267, 43, 55, 288
Monkey 2: 
Monkey 3: 

After round 10, the monkeys are holding items with these worry levels:
Monkey 0: 91, 16, 20, 98
Monkey 1: 481, 245, 22, 26, 1092, 30
Monkey 2: 
Monkey 3: 

...

After round 15, the monkeys are holding items with these worry levels:
Monkey 0: 83, 44, 8, 184, 9, 20, 26, 102
Monkey 1: 110, 36
Monkey 2: 
Monkey 3: 

...

After round 20, the monkeys are holding items with these worry levels:
Monkey 0: 10, 12, 14, 26, 34
Monkey 1: 245, 93, 53, 199, 115
Monkey 2: 
Monkey 3: 
````

Chasing all the monkeys at once is impossible; you're going to have to focus on the**two most active** monkeys if you
want any hope of getting your stuff back. Count the **total number of times each monkey inspects items** over 20 rounds:

````
Monkey 0 inspected items 101 times. << this
Monkey 1 inspected items 95 times.
Monkey 2 inspected items 7 times.
Monkey 3 inspected items 105 times. << and this
````

In this example, the two most active monkeys inspected items 101 and 105 times.
The level of **monkey business** in this situation can be found by multiplying these together: **10605**.

Figure out which monkeys to chase by counting how many items they inspect over 20 rounds.
**What is the level of monkey business after 20 rounds of stuff-slinging simian shenanigans?**

#### Your puzzle answer was 62491.

### --- Part Two ---

You're worried you might not ever get your items back. So worried, in fact, that your relief that a monkey's inspection
didn't damage an item **no longer causes your worry level to be divided by three**.

Unfortunately, that relief was all that was keeping your worry levels from reaching **ridiculous levels**. You'll need
to **find another way to keep your worry levels manageable**.

At this rate, you might be putting up with these monkeys for a **very long time** - possibly `10000` **rounds**!

With these new rules, you can still figure out the monkey business after `10000` rounds. Using the same example above:

````
== After round 1 ==
Monkey 0 inspected items 2 times.
Monkey 1 inspected items 4 times.
Monkey 2 inspected items 3 times.
Monkey 3 inspected items 6 times.

== After round 20 ==
Monkey 0 inspected items 99 times.
Monkey 1 inspected items 97 times.
Monkey 2 inspected items 8 times.
Monkey 3 inspected items 103 times.

== After round 1000 ==
Monkey 0 inspected items 5204 times.
Monkey 1 inspected items 4792 times.
Monkey 2 inspected items 199 times.
Monkey 3 inspected items 5192 times.

== After round 2000 ==
Monkey 0 inspected items 10419 times.
Monkey 1 inspected items 9577 times.
Monkey 2 inspected items 392 times.
Monkey 3 inspected items 10391 times.

== After round 3000 ==
Monkey 0 inspected items 15638 times.
Monkey 1 inspected items 14358 times.
Monkey 2 inspected items 587 times.
Monkey 3 inspected items 15593 times.

== After round 4000 ==
Monkey 0 inspected items 20858 times.
Monkey 1 inspected items 19138 times.
Monkey 2 inspected items 780 times.
Monkey 3 inspected items 20797 times.

== After round 5000 ==
Monkey 0 inspected items 26075 times.
Monkey 1 inspected items 23921 times.
Monkey 2 inspected items 974 times.
Monkey 3 inspected items 26000 times.

== After round 6000 ==
Monkey 0 inspected items 31294 times.
Monkey 1 inspected items 28702 times.
Monkey 2 inspected items 1165 times.
Monkey 3 inspected items 31204 times.

== After round 7000 ==
Monkey 0 inspected items 36508 times.
Monkey 1 inspected items 33488 times.
Monkey 2 inspected items 1360 times.
Monkey 3 inspected items 36400 times.

== After round 8000 ==
Monkey 0 inspected items 41728 times.
Monkey 1 inspected items 38268 times.
Monkey 2 inspected items 1553 times.
Monkey 3 inspected items 41606 times.

== After round 9000 ==
Monkey 0 inspected items 46945 times.
Monkey 1 inspected items 43051 times.
Monkey 2 inspected items 1746 times.
Monkey 3 inspected items 46807 times.

== After round 10000 ==
Monkey 0 inspected items 52166 times.
Monkey 1 inspected items 47830 times.
Monkey 2 inspected items 1938 times.
Monkey 3 inspected items 52013 times.
````

After 10000 rounds, the two most active monkeys inspected items 52166 and 52013 times. Multiplying these together, the
level of **monkey business** in this situation is now **2713310158**.

Worry levels are no longer divided by three after each item is inspected; you'll need to find another way to keep your
worry levels manageable. Starting again from the initial state in your puzzle input, **what is the level of monkey
business after 10000 rounds?**

#### Your puzzle answer was 17408399184.

---

## Solution

This solution is written in `R`.

<p style="color: red;">Disclaimer</p> Solution in R was not compleat. 
Part II of python solution needed some help online, all brainpower was used for R :D

````R
# Unready solution for Advent of Cyber 2022

Item <- function(id, worry_level) {
  # attributes
  self.id <- id
  self.worry_level <- worry_level
  structure(class = "Item", list(
    # methods
    get_id = function() self.id,
    get_worry_level = function() self.worry_level,
    set_worry_level = function(worry_level) self.worry_level <<- worry_level,
    divide_worry_level = function() self.worry_level <<- round(self.worry_level / 3, 0)
  ))
}

Monkey <- function(id = 0, items, multiply = 1, increase = 0, test = NULL, on_true = NULL, on_false = NULL) {
  # attributes
  self.id <- id
  self.items <- items
  self.item <- NULL
  self.multiply <- multiply
  self.increase <- increase
  self.test <- test
  self.on_true <- on_true
  self.on_false <- on_false
  print("Created new Monkey")

  structure(class = "Monkey", list(
    # methods
    get_id = function() self.id,
    get_multiply = function() returnself.multiply,

    inspect = function() {
      print(length(self.items))
      self.item <- tail(self.items, 1)
      print(length(self.items))
      item <- self.item
      print(item$get_id())
      worry_level <- item.get_worry_level
      worry_level <- worry_level + self.increase
      worry_level <- worry_level * self.multiply
      item.set_worry_level()
    },

    test_item = function() {
      if (self.item %% self.test == 0) {
        target <- get_monkey_by_id(self.on_true)
        target.add_item(self.item)
      } else {
        target <- get_monkey_by_id(self.on_false)
        target.add_item(self.item)
      }
      self.item <- NULL
    },

    add_item = function(item) {
      self.items <- append(self.items, item, 1)
    },
    get_items = function() {
      self.items
      return(length(self.items))
    }
  ))

}

get_monkey_by_id <- function(id) {
  if (id == 0) return(a)
  if (id == 1) return(b)
  if (id == 2) return(c)
  if (id == 3) return(d)
  if (id == 4) return(e)
}

items = list()

item = Item(1, 2)
item2 = Item(2, 8)

items <- append(items, item)
items <- append(items, item2)

item$get_id()
items[1]$get_id()

print(" ")

monkis = list()

monki <- Monkey(1, list())
# monki2 <- Monkey(2, list())
# monki3 <- Monkey(3, list())

monkis <- append(monkis, monki)
# monkis <- append(monkis, monki2)
# monkis <- append(monkis, monki3)

aa <- monkis[[5]](Item(66, 16))
aa <- monkis[[5]](Item(88, 112))
# monkis[[11]](Item(6, 8))
# monkis[[17]](Item(8, 32))

monkis[[6]]()
````

This solution is written in `Python`.

````Python
from functools import reduce

PART_1 = False
debug = False

monkies = []


def reduce_worry():
    # Got to find this solution from reddit, no thinking power left after R
    # Source: https://github.com/Dullstar/Advent_Of_Code/blob/fa063a3692e5806ba4ff17cf23a62ede4ca10955/python/year2022/day11.py#L77
    return reduce(lambda x, y: x * y, [i for i in map(lambda n: n.test, monkies)])


class Item:
    def __init__(self, worry_level):
        self.worry_level: int = worry_level

    def update_worry_level(self, worry):
        self.worry_level = worry // 3 if PART_1 else worry % reduce_worry()
        if debug: print(f"Monkey gets bored with item. Worry level is divided by 3 to {self.worry_level}.")

    def get_worry(self):
        return self.worry_level


class Monkey:
    def __init__(self, id: int, items: list, multiply, increase: int, test: int, on_true: int, on_false: int):
        self.id = id
        self.items = items or []
        self.multiply = multiply or 1
        self.increase = increase or 0
        self.test = test
        self.on_true = on_true
        self.on_false = on_false

        self.monkey_business = 0
        self.item = None

    def get_id(self):
        return self.id

    def inspect(self):
        self.monkey_business += 1
        self.item = self.items.pop(0)
        worry_level = int(self.item.worry_level)
        if debug: print(f"\nMonkey inspects an item with a worry level of {worry_level}.")
        worry_level *= int(self.multiply) if str(self.multiply).isdigit() else worry_level
        if debug: print(
            f"Worry level is multiplied by {self.multiply if str(self.multiply).isdigit() else 'itself'} to {worry_level}.")
        worry_level += int(self.increase)
        if debug: print(f"Worry level increases by {self.increase} to {worry_level}.")
        self.item.update_worry_level(worry_level)

    def test_item(self):
        if self.item.worry_level % self.test == 0:
            if debug: print(f"Current worry level is divisible by {self.test}.")
            target: Monkey = monkies[self.on_true]
        else:
            target: Monkey = monkies[self.on_false]
            if debug: print(f"Current worry level is not divisible by {self.test}.")

        target.add_item(self.item)
        if debug: print(f"Item with worry level {self.item.worry_level} is thrown to monkey {target.get_id()}.")
        self.item = None

    def add_item(self, item):
        self.items.append(item)

    def monkey_handler(self):
        if debug: print(f"\nMonkey {self.get_id()}:")
        while len(self.items) > 0:
            self.inspect()
            self.test_item()

    def get_monkey_business(self):
        return self.monkey_business


with open("../input.txt", "r") as file:
    id = 0
    items = []
    multiply = 1
    increase = 0
    test = 0
    on_true = 0
    on_false = 0

    data = file.read().split("\n\n")

    for index, monkey in enumerate(data):
        id = monkey.split()[1][0]
        [items.append(Item(item)) for item in
         "".join(monkey.split("Starting items: ")[1].split("\n  Operation")[0]).split(", ")]
        # print([item.worry_level for item in items])
        if monkey.split("Operation: new = old ")[1][0] == "+":
            increase = monkey.split("Operation: new = old + ")[1].split("\n")[0]
            multiply = 1
        else:
            multiply = monkey.split("Operation: new = old * ")[1].split("\n")[0]
            increase = 0
        test = monkey.split("Test: divisible by ")[1].split("\n")[0]
        on_true = monkey.split("If true: throw to monkey ")[1].split("\n")[0]
        on_false = monkey.split("If false: throw to monkey ")[1].split("\n")[0]
        monkies.append(Monkey(id=int(id), items=items, multiply=multiply, increase=increase, test=int(test),
                              on_true=int(on_true), on_false=int(on_false)))
        if debug: print(f"Generated Monkey: id {id}, items {[item.get_worry() for item in items]}")
        items = []
    n = 20 if PART_1 else 10000
    for rnd in range(0, n):
        for monkey in monkies:
            monkey.monkey_handler()

    monkey_business = []
    for monkey in monkies:
        monkey_business.append(monkey.get_monkey_business())
        if debug:
            print(f"{[item.get_worry() for item in monkey.items]}")
            print(f"monkey business {monkey.get_id()} {monkey.get_monkey_business()}")
    monkey_business.sort(reverse=True)

    print(f"Part Part {'I' if PART_1 else 'II'} {monkey_business[0] * monkey_business[1]}")


````

