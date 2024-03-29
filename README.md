# Menu dictionary
menu = {
    "Snacks": {
        "Cookie": 0.99,
        "Banana": 0.69,
        "Apple": 0.49,
        "Granola bar": 1.99
    },
    "Meals": {
        "Burrito": 4.49,
        "Teriyaki Chicken": 9.99,
        "Sushi": 7.49,
        "Pad Thai": 6.99,
        "Pizza": {
            "Cheese": 8.99,
            "Pepperoni": 10.99,
            "Vegetarian": 9.99
        },
        "Burger": {
            "Chicken": 7.49,
            "Beef": 8.49
        }
    },
    "Drinks": {
        "Soda": {
            "Small": 1.99,
            "Medium": 2.49,
            "Large": 2.99
        },
        "Tea": {
            "Green": 2.49,
            "Thai iced": 3.99,
            "Irish breakfast": 2.49
        },
        "Coffee": {
            "Espresso": 2.99,
            "Flat white": 2.99,
            "Iced": 3.49
        }
    },
    "Dessert": {
        "Chocolate lava cake": 10.99,
        "Cheesecake": {
            "New York": 4.99,
            "Strawberry": 6.49
        },
        "Australian Pavlova": 9.99,
        "Rice pudding": 4.99,
        "Fried banana": 4.49
    }
}

# 1. Set up order list. Order list will store a list of dictionaries for
# menu item name, item price, and quantity ordered
customer_order = [
  {
    "Item name": "string",
    "Price": float,
    "Quantity": int
  },
  {
    "Item name": "string",
    "Price": float,
    "Quantity": int
  },
]
# Launch the store and present a greeting to the customer
print("Welcome to the variety food truck.")

# Customers may want to order multiple items, so let's create a continuous
# loop
place_order = True
while place_order:
    # Ask the customer from which menu category they want to order
    print("From which menu would you like to order? ")
    for i, key in enumerate(menu.keys(), start=1):
        print(f"{i}: {key}")

# Create a variable for the menu item number
    i=1
# Create a dictionary to store the menu for later retrieval
    menu_selection = input("Type menu number: ")
    # Validate if input is a number
    if menu_selection.isdigit():
    
        menu_selection = int(menu_selection)
        if 1 <= menu_selection <= len(menu):
            menu_category_name = list(menu.keys())[menu_selection - 1]

    # Print the options to choose from menu headings (all the first level
    # dictionary items in menu).
            print(f"You selected {menu_category_name}")
            print(f"What {menu_category_name} item would you like to order?")
            i = 1
            for key, value in menu[menu_category_name].items():
                print(f"{i}: {key} - ${value}")
                i += 1

        # 2. Ask customer to input menu item number
            item_number = input("Type item number: ")
            if item_number.isdigit():
                item_number = int(item_number)
                if 1 <= item_number <= len(menu[menu_category_name]):
                    item_name = list(menu[menu_category_name].keys())[item_number - 1]
                    item_price = menu[menu_category_name][item_name]

                    # Get quantity from the customer
                    quantity = input(f"Enter quantity for {item_name}: ")
                    if quantity.isdigit():
                        quantity = int(quantity)
                    else:
                        quantity = 1

                    # Append order to the order list
                    customer_order.append({
                        "Item name": item_name,
                        "Price": item_price,
                        "Quantity": quantity
                    })
                    print("Item added to your order.")
                else:
                    print("Invalid item number.")
            else:
                print("Invalid input for item number.")
        else:
            print("Invalid menu number.")
    else:
        print("Invalid input for menu number.")

    while True:
    # Ask the customer if they would like to order anything else
        order_again = input("Would you like to keep ordering? (Y)es or (N)o ").lower()
        match order_again.case:
            case 'y':
                place_order = True
                break
            case 'n':
                place_order = False
                print("Thank you for your order.")
                break
            case _:
                print("Please try again.")

# Print order receipt
print("This is what we are preparing for you.\n")
print("Item name                 | Price  | Quantity")
print("--------------------------|--------|----------")

total_cost = 0
for item in customer_order:
    item_name = item["Item name"]
    price = item["Price"]
    quantity = item["Quantity"]
    total_cost += price * quantity

# 9. Create space strings
    item_spaces = " " * (25 - len(item_name))
    price_spaces = " " * (8 - len(str(price)))
    quantity_spaces = " " * (10 - len(str(quantity)))

# 10. Print the item name, price, and quantity
    print(f"{item_name}{item_spaces} | ${price}{price_spaces} | {quantity}{quantity_spaces}")

# 11. Calculate the cost of the order using list comprehension
# Multiply the price by quantity for each item in the order list, then sum()
# and print the prices
print(f"\nTotal Cost: ${total_cost:.2f}")
