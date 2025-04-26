# Logical Puzzles

## Pay an employee using a gold rod of 7 units

An employee works for an employer for 7 days. The employer has a gold rod of 7 units. How does the employer pay to the employee, so that the number of employee’s rod units increases by one at the end of each day? The employer can make at most 2 cuts in the rod. 

```
Divide 7 unit of rod into 2 part such that we will have 3 blocks:
Rod -> 
    Block A: 1 
    Block B: 23 
    Block C: 4,5,6,7

Day 1: Block A => Employer-Block B,C
Day 2: Ask Block A, Give Block B => Employer-> BlockA,C
Day 3: Give Block A => Employer-> Block C
Day 4: Ask Block A,B, Give Block C => Employer -> Block A, B
Day 5: Give Block A
Day 6: Ask Block A, Give Block B
Day 7: Give Block A

| Day | Action                                                               | Employer Holds | Employee Holds | Example (Total Units) |
|-----|----------------------------------------------------------------------|----------------|----------------|------------------------|
| 1   | Give **Block A** (1 unit)                                            | B, C           | A              | 1                      |
| 2   | Take back **Block A**, give **Block B** (2 units)                    | A, C           | B              | 2                      |
| 3   | Give **Block A** (1 unit)                                            | C              | A, B           | 3 (1+2)                |
| 4   | Take back **Blocks A & B**, give **Block C** (4 units)               | A, B           | C              | 4                      |
| 5   | Give **Block A** (1 unit)                                            | B              | A, C           | 5 (1+4)                |
| 6   | Take back **Block A**, give **Block B** (2 units)                    | A              | B, C           | 6 (2+4)                |
| 7   | Give **Block A** (1 unit)                                            | —              | A, B, C        | 7 (1+2+4)              |

```

## Fastest 3 Horses

There are 25 horses among which you need to find out the fastest 3 horses. You can conduct a race among at most 5 to find out their relative speed. At no point, you can find out the actual speed of the horse in a race. Find out the minimum no. of races which are required to get the top 3 horses.

```
First 5 race to get top 3 from each category
R1 -> A1>A2>A3
R2 -> B1>B2>B3
R3 -> C1>C2>C3
R4 -> D1>D2>D3
R5 -> E1>E2>E3

Race 6: Race for Group winners
A1, B1, C1, D1, E1 will compete
A1>B1>C1>D1>E1

Top fastest -> A1

Race 7:
A2, A3, B1, B2, C1

A2>A3>B1>B2>C1

Second fastest - A2
Third fastest - A3
```
<b>Total Number of Race Required: 7 </b>

### 3 Bulbs and 3 Switches

There is a room with a door (closed) and three light bulbs inside the room. Outside the room, there are three switches, connected to the bulbs. You may manipulate the switches as you wish, but once you open the door you can’t change them. All bulbs are in working condition and you can open the door only once. Identify each switch with respect to its bulb.

```
Note: If we lighten the bulb for some minutes, it becomes hot.

So, Switch on first switch for some time and then switch off
Then switch on second switch and keep 3rd switch off

Now, move to any room
If room light is on -> 2nd switch
If room light is off -> check bulb heating -> if heated -> first switch else third switch
```

### Camel and Banana Puzzle

A person has 3000 bananas and a camel. The person wants to transport the maximum number of bananas to a destination which is 1000 KMs away, using only the camel as a mode of transportation. The camel cannot carry more than 1000 bananas at a time and eats a banana every km it travels. What is the maximum number of bananas that can be transferred to the destination using only camel (no other mode of transportation is allowed). 

```
Move 3,000 bananas to R₁ (200 km away):

    3 forward trips and 2 backward trips.

    First trip: 1,000 bananas → 300 bananas eaten, 300 kept for return → 400 at R₁.

    Second trip: 400 bananas at R₁.

    Last trip: 700 bananas left.

    Total at R₁ = 400 + 400 + 700 = 1,500 bananas.

Move 1,500 bananas to R₂ (533.33 km away):

    2 forward trips and 1 backward trip.

    First trip: 1,000 bananas → 400 bananas left at R₂.

    Second trip: 500 bananas → 200 bananas left at R₂.

    Total at R₂ = 600 bananas.

Move 600 bananas from R₂ to the destination (400 km away):

    600 bananas → 200 bananas left at the destination.
```