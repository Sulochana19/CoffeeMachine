# CoffeeMachine
MENU = {
    "espresso": {
        "ingredients": {
            "water": 50,
            "coffee": 18,
        },
        "cost": 1.5,
    },
    "latte": {
        "ingredients": {
            "water": 200,
            "milk": 150,
            "coffee": 24,
        },
        "cost": 2.5,
    },
    "cappuccino": {
        "ingredients": {
            "water": 250,
            "milk": 100,
            "coffee": 24,
        },
        "cost": 3.0,
    }
}

resources = {
    "water": 300,
    "milk": 200,
    "coffee": 100,
}


## TODO : make a function named report to give the user details about the coffee machine tank.
def report(water, milk, coffee, money):
    # water = resources['water'] - MENU[coffee_type]['ingredients']['water']
    print(f'''
Water: {water}
Milk: {milk}
Coffee: {coffee}
Money: ${money}''')


def resource_sufficient(water, milk, coffee, user_choice):
    if water < MENU[user_choice]['ingredients']['water']:
        print(" Sorry there is not enough water.")
        machine(water, milk, coffee, money)
    elif coffee < MENU[user_choice]['ingredients']['coffee']:
        print(" Sorry there is not enough coffee.")
        machine(water, milk, coffee, money)
    elif user_choice == "espresso":
        return
    elif milk < MENU[user_choice]['ingredients']['milk']:
        print(" Sorry there is not enough milk.")
        machine(water, milk, coffee, money)
    else:
        return


def process_coins(user_choice):
    number_of_quarters = int(input("How many quarters?: "))
    number_of_dimes = int(input("How many dimes?: "))
    number_of_nickles = int(input("How many nickles?: "))
    number_of_pennies = int(input("How many pennies?: "))
    money = float(number_of_quarters*0.25 + number_of_nickles*0.05 + number_of_dimes*0.10 + number_of_pennies*0.01)
    if money <= MENU[user_choice]['cost']:
        print("Sorry that's not enough money. Money refunded.")
    else:
        change = money - MENU[user_choice]['cost']
        print(f"Here is ${change} in change.")
        print(f"Here is your {user_choice}. Enjoy!")


def machine(water, milk, coffee, money):
    user_choice = input(" What would you like? (espresso/latte/cappuccino): ").lower()
    if user_choice == "report":
        report(water, milk, coffee, money)
        machine(water, milk, coffee, money)
    else:
        resource_sufficient(water, milk, coffee, user_choice)
        print("Please insert coins.")
        process_coins(user_choice)
        water = water - MENU[user_choice]['ingredients']['water']
        if user_choice == "espresso":
            milk = 0
        else:
            milk = milk - MENU[user_choice]['ingredients']['milk']
        coffee = coffee - MENU[user_choice]['ingredients']['coffee']
        money = money + MENU[user_choice]['cost']
        machine(water, milk, coffee, money)


user_choice = input(" What would you like? (espresso/latte/cappuccino): ").lower()
water = resources['water']
milk = resources['milk']
coffee = resources['coffee']
money = 0
if user_choice == "report":
    print(f'''Water: {water}ml
Milk: {milk}ml
Coffee: {coffee}g
Money: ${money}''')
else:
    print("Please insert coins.")
    process_coins(user_choice)
    water = water - MENU[user_choice]['ingredients']['water']
    if user_choice == "espresso":
        milk = milk - 0
    else:
        milk = milk - MENU[user_choice]['ingredients']['milk']
    coffee = coffee - MENU[user_choice]['ingredients']['coffee']
    money = money + MENU[user_choice]['cost']
machine(water, milk, coffee, money)
