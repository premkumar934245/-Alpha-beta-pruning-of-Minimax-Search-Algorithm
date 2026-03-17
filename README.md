<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:  PREM KUMAR S   </h3>
<h3>Register Number:  212223240125         </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

<h2> Program:</h2>

```python
def initialize_game():
    current_state = [['.','.','.'],['.','.','.'],['.','.','.']]
    player_turn = 'X'
def drawboard():
    for i in range(3):
        for j in range(3):
            print("{}|".format(current_state[i][j]),end="")
        print()
def isvalid(px,py):
    if px<0 or px>2 or py<0 or py>2:
        return False
    elif current_state[px][py]!='.':
        return False
    else:
        return True
def is_end():
    #vertical win
    for i in range(3):
        if (current_state[0][i]!='.' and current_state[0][i]==current_state[1][i] and
            current_state[1][i]==current_state[2][i]):
            return current_state[0][i]
    #horizontal win
    for i in range(3):
        if current_state[i]==['X','X','X']:
            return 'X'
        elif current_state[i]==['O','O','O']:
            return 'O'
    #inverse diagonal win
    for i in range(3):
        if (current_state[0][2]==current_state[1][1] and current_state[1][1]==current_state[2][0]
            and current_state[0][2]!='.'):
            return current_state[0][2]
    #diagonal win
    for i in range(3):
        if (current_state[0][0]==current_state[1][1] and current_state[1][1]==current_state[2][2]
            and current_state[0][0]!='.'):
            return current_state[0][0]
    #check for board
    for i in range(3):
        for j in range(3):
            if current_state[i][j]=='.':
                return None
    return '.' #it is a tie
def minimum():
    minv=2
    qx=None
    qy=None
    result=is_end()
    if result=='X':
        return(-1,0,0)
    elif result=='O':
        return(+1,0,0)
    elif result=='.':
        return(0,0,0)
    for i in range(3):
        for j in range(3):
            if current_state[i][j]=='.':
                current_state[i][j]='X'
                (m,min_i,min_j)=maximum()
                if m<minv:
                    minv=m
                    qx=i
                    qy=j
                current_state[i][j]='.'
    return (minv,qx,qy)
def maximum():
    maxv=-2
    px=None
    py=None
    result=is_end()
    if result=='X':
        return(-1,0,0)
    elif result=='O':
        return(+1,0,0)
    elif result=='.':
        return(0,0,0)
    for i in range(3):
        for j in range(3):
            if current_state[i][j]=='.':
                current_state[i][j]='O'
                (m,max_i,max_j)=minimum()
                if m>maxv:
                    maxv=m
                    px=i
                    py=j
                current_state[i][j]='.'
    return (maxv,px,py)
def play():
    #initialize_game()
    #drawboard()
    player_turn = 'X'
    while True:
        result = is_end()
        drawboard()
        if result != None:
            if result == 'X':
                print("The winner is X")
            elif result == 'O':
                print("The winner is O")
            else:
                print("It is a tie!")
            initialize_game()
            return
        if player_turn == 'X':
            (m,qx,qy)=minimum()
            while True:
                print("x:{},y:{}".format(qx,qy))
                px = int(input())
                py = int(input())
                (qx, qy) = (px, py)
                if isvalid(px,py):
                    current_state[px][py]='X'
                    player_turn = 'O'
                    break
                else:
                    print("Enter correct values for x and y")
        else:
            (m,px,py)=maximum()
            current_state[px][py]='O'
            player_turn='X'
current_state = [['.','.','.'],['.','.','.'],['.','.','.']]
play()
```

<h2> Output:</h2>
<img width="1792" height="986" alt="image" src="https://github.com/user-attachments/assets/7797904b-1289-419f-9871-3221827601ce" />

<img width="1920" height="754" alt="image" src="https://github.com/user-attachments/assets/34d5a71d-60d5-4e78-bd8a-12b08448d7a6" />

