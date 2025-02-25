Food Ordering App

The "Food Ordering App" Project was built with Python as part of my First Semester Exam With Altschool Africa - 2025.

def display_menu():
    """
    Description: Prints the menu options for the food items available in the ordering app.
                 since the app only has 3 food items you can order we add a fourth option to exit
                 the menu when they are done ordering.
    """
    print("Menu:")
    print("1. Pizza - 6500")
    print("2. Burger - 3000")
    print("3. Noodles - 1300")
    print("4. Exit Menu")

def get_user_choice():
    """
    Description: Takes user input to get the number corresponding to the chosen food item from the menu.
                 Ensures the input is a valid choice between 1 and 4.
                 If the input is not an integer return the error'Invalid input. Please enter a valid number'.

                 If the input is an integer but not between 1 and 4 return the error
                 'Invalid choice. Please enter a number between 1 and 4.' 
    """
    while True:  # Keep prompting until valid input
        user_food_choice = input().strip()
        try:
            choice = int(user_food_choice)
        except ValueError:
            print('Invalid input. Please enter a valid number.')
            continue  # Restart loop after error
            
        if 1 <= choice <= 3:
            return choice  # Exit function with valid choice
        elif choice == 4:
            break
        else:
            print('Invalid choice. Please enter a number between 1 and 4.')

def get_quantity():
    """Description: Takes user input to get the quantity of the selected food item.
                 and ensures the input is a positive integer.

                 If the input is not an integer return the error 
                 'Invalid input. Please enter a valid number.' 
                 
                 If the input is a negative integer or zero return the error
                 'Quantity must be greater than 0.'"""
    while True:
        user_input = input("Enter quantity: ")
        try:
            quantity = int(user_input)
            if quantity > 0:
                return quantity
            else:
                print("Quantity must be greater than 0.")
        except ValueError:
            print("Invalid input. Please enter a valid number.")

def get_item_name(choice):
    """
    Description: Retrieves and returns the name of a food item
    based on the user's choice number from the menu.
    """
    menu = {1: "Pizza", 2: "Burger", 3: "Noodles"}
    return menu.get(choice, None)

def get_item_price(choice):
    """
    Description: Retrieves and returns the price of a food item based on
    the user's choice number from the menu.
    """
    item_price = {1: 6500, 2: 3000, 3: 1300}
    return item_price.get(choice, None)

def calculate_total_price(item_price, quantity):
    """
    Description: Calculates and returns the total price of a specific food item
    based on its price and the quantity ordered.
    """
    return item_price * quantity

def place_order():
    """
    Description: Manages the process of adding items to a shopping cart.
                 USES A DICTIONARY FOR THE CART.
                 Calls other functions to get user choices, quantities, and calculates total prices.

                 Your cart should look something like this assuming this user ordered 3 pizzas and 3 burgers.
                 {
                    'Pizza': {'quantity': 3, 'total_price': 19500},
                    'Burger': {'quantity': 3, 'total_price': 9000}
                 }
    """
    cart = {}
    
    while True:
        print("\nMenu:")
        print("1: Pizza - 6500")
        print("2: Burger - 3000")
        print("3: Noodles - 1300")
        print("4: Checkout")
        
        choice = get_user_choice()
       
        if choice is None:
            break
        
        item_name = get_item_name(choice)
        item_price = get_item_price(choice)
        quantity = get_quantity()

        if not item_name or not item_price:
            print("Invalid choice. Please try again")
        
        total_price = calculate_total_price(item_price, quantity)
        
        if item_name in cart:
            cart[item_name]['quantity'] += quantity
            cart[item_name]['total_price'] += total_price 
        else:
            cart[item_name] = {'quantity': quantity, 'total_price': total_price}
        
        print(f"Added {quantity} {item_name}(s) to the cart.")
    
    return cart

def check_out(cart):
    """
    Description: Finalizes the order by displaying the contents of the shopping cart, including quantities and total prices.
                 Prints the total order price like a receipt.

                 The receipt would look like this if the cart is empty:
                 
                     Your cart is empty. No items to check out.

                 If the cart has items in it, the receipt should look exactly like this:

                     Checking out...
                     Your order details:
                     Item 1: Quantity - 2, Total Price - 2000
                     Item 2: Quantity - 3, Total Price - 1500
                     Total Order Price: 3500
                     Thank you for ordering!
    """
    if not cart:
        print("Your cart is empty. No items to check out.")
        return

    print("Checking out...")
    print("Your order details:")
    
    total_price = 0
    for item, details in cart.items():
        quantity = details['quantity']
        item_total = details['total_price']
        total_price += item_total
        print(f"{item}: Quantity - {quantity}, Total Price - ${item_total}")
    
    print(f"Total Order Price: ${total_price}")
    print("Thank you for ordering!")
    
def food_ordering_app():
    """
    Description: The main function that initiates the food ordering application.
                 Calls place_order() to build the shopping cart and then calls check_out() to complete the order.

                 NOTE THAT IF ANY OF THE OTHER FUNCTIONS ARE NOT CORRECTLY WRITTEN THIS WILL FAIL
                 PLEASE DO NOT MODIFY THIS CELL
    """
    print("Welcome to the Food Ordering App!")
    cart = place_order()
    check_out(cart)
