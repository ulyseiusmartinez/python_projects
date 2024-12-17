import random

#create global constant
MAX_LINES = 3 
MAX_BET = 100
MIN_BET = 1


ROWS = 3
COLS = 3

#create symbol library
symbol_count = {
    "A": 2,
    "B": 4,
    "C": 6,
    "D": 8
}

symbol_value = {
    "A": 5,
    "B": 4,
    "C": 3,
    "D": 2
}


def check_winnings(columns, lines, bet, values):
    winnings = 0
    winning_lines = []
    for line in range(lines): #loop through every line(row)
        symbol = columns[0][line]  #check symbol in first column of row
        for column in columns: #loop through columns
            symbol_to_check = column[line] #check for symbol
            if symbol != symbol_to_check: #break loop if they don't win, AKA no matching symbols
                break
            else: 
                winnings += values[symbol] * bet #winnings if they won, multiplier of symbol multiplied by their bet
                winning_lines.append(line + 1)
    return winnings, winning_lines


def get_slotmachine_spin(rows, cols, symbols):
    all_symbols = [] #create library for symbols
    for symbol, symbol_count in symbols.items(): #loop through each symbol in library and append all_symbols to have appropriate count of symbols
        for _ in range(symbol_count):
            all_symbols.append(symbol)
    
    columns = [] # define columns list   
    for _ in range(cols): #generate column for every single column 
        column = []
        current_symbols = all_symbols[:] #create copy of all_symbols that won't impact original library
        for _ in range(rows): #loop will pick random values, loop through number of values that need to be generated = amount of rows
            value = random.choice(current_symbols) #choose random value from symbol list
            current_symbols.remove(value) #removes value from list
            column.append(value) #adds value to column
        columns.append(column)
    return columns


#function to transpose matrix
def print_slotmachine(columns): 
    for row in range(len(columns[0])): #loop through every row
         #loop through every column and print first value, enumerate will give index and item as you loop through, only print column for row we are on
        for i, column in enumerate(columns): 
            if i != len(columns) - 1: #this is saying that any index
                print(column[row], end = " | ")
            else:
                print(column[row], end = "")
        print() #will move to next line to print since end of other print statements has been changed to remove /n
        
            
#Create function for user deposit
def deposit():
    while True: #open loop
        amount = input("What would you like to deposit? $") #prompt user for input
        if amount.isdigit(): #check that input is a digit
            amount = int(amount) #set deposit amount
            if amount > 0: #ensure value is greater than 0.
                break
            else: 
                print("Amount must be greater than 0. ") 
        else:
            print("Please enter a  number. ")
    
    return amount


def get_number_of_lines():
    while True: #open loop
        lines = input("Enter the number of lines to bet on (1- " + str(MAX_LINES) + ")? ") #prompt user for bet input
        if lines.isdigit(): #check that input is a digit
            lines = int(lines) #set deposit amount
            if 1 <= lines <= MAX_LINES: #ensure bet is within bounds
                break
            else: 
                print("Enter a valid number of lines. ") 
        else:
            print("Please enter a valid bet. ")
    return lines
    
    
def get_bet():
    while True: #open loop
        amount = input("What would you like to bet on each line? $") #prompt user for input
        if amount.isdigit(): #check that input is a digit
            amount = int(amount) #set deposit amount
            if MIN_BET <= amount <= MAX_BET: #ensure value is greater than 0.
                break
            else: 
                print(
                    f"Amount must be between ${MIN_BET} - ${MAX_BET}. ") 
        else:
            print("Please enter a  number. ")
    
    return amount
   
    
def spin(balance):
    lines = get_number_of_lines()
    while True:
        bet = get_bet()
        total_bet = bet*lines

        if total_bet > balance:
            print(
                f"You do not have enough to bet that amount. Your current balance is ${balance}")
        else:
            break
    print(
        f"You are betting ${bet} on {lines} lines. Your total bet is: ${total_bet}")
    
    slots = get_slotmachine_spin(ROWS, COLS, symbol_count)
    print_slotmachine(slots)
    winnings, winning_lines = check_winnings(slots, lines, bet, symbol_value)
    print(f"You won ${winnings}! ")
    print(f"You won on lines:", *winning_lines)
    return winnings - total_bet
 
    
def main():
    balance = deposit()
    while True:
        print(f"Current balance is ${balance}")
        answer = input("Press enter to play (q to quit).")
        if answer == "q":
            break
        balance += spin(balance)
    print(f"You left with ${balance}")    

main()
