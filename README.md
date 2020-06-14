# Tic-Tac-Toe
Play tic-tac-toe with a computer!

## Intialization
```python
import random
new = ['','','','','','','','','']
man = ''
machine = ''
null = ''
```
Firstly, I import the `random` module. This is used for the computer opponent who can randomly mark their symbol on the tic-tac-toe table.

I define a `sign()` function in order to get the user to select which sign ("X" or "O") they want to choose. `while` loop is used to validate user input.

```python
def sign(man, machine):
    man = input("What team you want to be? X or O ")
    while man not in ('x','X','o','O'):
        print ("Invalid Choice!")
        man =input("What team you want to be? X or O ")
    if man == 'x' or man == 'X':
        print ("Ok, X is yours!")
        machine = 'o'
    else:
        print ("Ok, O is yours!")
        machine = 'x'
    return man.upper(), machine.upper()
```

Next, I define the `decide_turn()` function to prompt the user if they want to go first or not:
```python
def decide_turn():
    turn = None
    while turn not in ('y','Y','n','N'):
        turn =input("Do you want to go first? ")
        if turn == 'y' or turn == 'Y':
            return 1
        elif turn == 'n' or turn == 'N':
            return 0
        else:
            print ("its an invalid choice.")
```

## Gameplay
```python
def draw(a):
    
    print ("\n\t",a[0],"|",a[1],"|",a[2])
    print ("\t", "--------")
    print ("\n\t",a[3],"|",a[4],"|",a[5])
    print ("\t", "--------")
    print ("\n\t",a[6],"|",a[7],"|",a[8], "\n")
```
The function `draw()` will draw out the tic-tac-toe board using string slicing.

```python
def congo_man():
    print("You won!!")

def congo_machine():
    print ("Hahha, I won!!!")
```
These two functions will output who is the winner when either player draws a line on the board.

```python
def man_first(man, machine, new):
    while winn(man, machine, new) is None:
        move = man_move(man, new)
        new[int(move)] = man
        draw(new)
        if winn(man, machine, new) != None:
            break
        else:
            pass
        print ("ummmm....i'll take..")
        p_move = machine_move(man, machine, new)
        print (p_move)
        new[int(p_move)] = machine
        draw(new)
    q = winn(man, machine, new)
    if q == 1:
        congo_man()
    elif q == 0:
        congo_machine()
    else:
        print ("Its tie man...")
```
The `man_first()` function will run if the user starts first. The user and the computer will take turns to put their signs on the board until one of them draws a 'line' on the board, either the `congo_man()` function or the `congo_machine()` function will run to output the winner.

```python
def machine_first(man, machine, new):
    while not winn(man, machine, new):
        print ("i'll take...")
        p_move = machine_move(man, machine, new)
        print (p_move)
        new[p_move] = machine
        draw(new)
        if winn(man, machine, new) != None:
            break
        else:
            pass
        move = man_move(man, new)
        new[int(move)] = man
        draw(new)
    q = winn(man, machine, new)
    if q == 1:
        congo_man()
    elif q == 0:
        congo_machine()
    else:
        print ("Its tie man...")
```
The exact same function runs, except when the user chooses to let the computer start first.

```python
def winn(man, machine, new):
    ways = ((0,1,2),(3,4,5),(6,7,8),(0,3,6),(1,4,7),(2,5,8),(0,4,8),(2,4,6))
    for i in ways:
        if new[i[0]] == new[i[1]] == new[i[2]] != null:
            winner = new[i[0]]
            if winner == man:
                return 1
            elif winner == machine:
                return 0
            if null not in new: 
                return 'TIE'
    if null not in new: 
        return 'TIE'    
    return None
```
This function foresees all combinations of a winning 'line' being formed on the board based on the index of the board.

```python
def man_move(man, new): 
    a = input("where you want to move? ")
    while True:
        if a not in ('0','1','2','3','4','5','6','7','8'):
            print ("Sorry, invalid move")
            a =input("where you want to move? ")
        elif new[int(a)] != null:
            print ("Sorry, the place is already taken")
            a = input("where you want to move? ")
        else:
            return int(a)
```
The `man_move()` function is a validation for the user input on where to put their signs. A `while` loop iterate the input if the user inputs an inappropriate index or is out of range.

```python
def display_instruction():
      """ Displays Game Instuructions. """
      print 
      """
      Welcome to the Game...
      You will make your move known by entering a number, 0 - 8.
      The will correspond to the board position as illustrated:
                          0 | 1 | 2            
                         -----------
                          3 | 4 | 5            
                         -----------
                          6 | 7 | 8
                          
      Prepare yourself, the ultimate bettel is about to begin.....
      """
 ```
  Displays instructions if user requests for instructions.
  
 ```python
 def main(man, machine, new):
    display_instruction()
    print ("so lets begin..")
    a = sign(man, machine)
    man = a[0]
    machine = a[1]
    b = decide_turn()
    if b == 1:
        print ("Ok, you are first!")
        print ("Lets get started, here's a new board!")
        draw(new)
        man_first(man, machine, new)
    elif b == 0:
        print ("Ok, I'll be the first!")
        print ("So, lets start..")
        draw(new)
        machine_first(man, machine, new)
    else:
        pass
```
The `main()` function runs all the defined functions earlier.

Excecution of code:

```python
main(man, machine, new)
input("Press enter to exit")
```

## Dry Run
```
so lets begin..
What team you want to be? X or O X
Ok, X is yours!
Do you want to go first? Y
Ok, you are first!
Lets get started, here's a new board!

      |  | 
     --------

      |  | 
     --------

      |  |  

where you want to move? 0

     X |  | 
     --------

      |  | 
     --------

      |  |  

ummmm....i'll take..
8

     X |  | 
     --------

      |  | 
     --------

      |  | O 

where you want to move? 6

     X |  | 
     --------

      |  | 
     --------

     X |  | O 

ummmm....i'll take..
3

     X |  | 
     --------

     O |  | 
     --------

     X |  | O 

where you want to move? 2

     X |  | X
     --------

     O |  | 
     --------

     X |  | O 

ummmm....i'll take..
1

     X | O | X
     --------

     O |  | 
     --------

     X |  | O 

where you want to move? 5

     X | O | X
     --------

     O |  | X
     --------

     X |  | O 

ummmm....i'll take..
4

     X | O | X
     --------

     O | O | X
     --------

     X |  | O 

where you want to move? 7

     X | O | X
     --------

     O | O | X
     --------

     X | X | O 

Its tie man...
Press enter to exit
```

Scenario #2
```
so lets begin..
What team you want to be? X or O O
Ok, O is yours!
Do you want to go first? Y
Ok, you are first!
Lets get started, here's a new board!

      |  | 
     --------

      |  | 
     --------

      |  |  

where you want to move? 6

      |  | 
     --------

      |  | 
     --------

     O |  |  

ummmm....i'll take..
7

      |  | 
     --------

      |  | 
     --------

     O | X |  

where you want to move? 3

      |  | 
     --------

     O |  | 
     --------

     O | X |  

ummmm....i'll take..
0

     X |  | 
     --------

     O |  | 
     --------

     O | X |  

where you want to move? 2

     X |  | O
     --------

     O |  | 
     --------

     O | X |  

ummmm....i'll take..
4

     X |  | O
     --------

     O | X | 
     --------

     O | X |  

where you want to move? 1

     X | O | O
     --------

     O | X | 
     --------

     O | X |  

ummmm....i'll take..
8

     X | O | O
     --------

     O | X | 
     --------

     O | X | X 

Hahha, I won!!!
Press enter to exit
```
