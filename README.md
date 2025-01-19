#creating  dictionary with categories prices and stock  for the menu.

menu={
    "Chips":{
        "L1":{"Name":"Doritos","Price":5.0,"stock":10},
        "L2":{"Name":"Lays","Price":5.0,"stock":8},
        "L3":{"Name":"Cheetos","Price":6.0,"stock":5},
    },
    "Chocolates":{
        "Y1":{"Name":"Kitkat","Price":3.0,"stock":7},
        "Y2":{"Name":"Lunchbar","Price":4.0,"stock":4},
        "Y3":{"Name":"Snickers","Price":4.0,"stock":5},
    },

    "Drinks":{
        "N1":{"Name":"Fanta","Price":4.0,"stock":7},
        "N2":{"Name":"Pepsi","Price":3.0,"stock":8},
        "N3":{"Name":"7up","Price":4.0,"stock":8},

    },"Cookies":{
        "C1":{"Name":"Digestive","Price":5.0,"stock":8},
        "C2":{"Name":"Cocozoo","Price":4.0,"stock":4},
        "C3":{"Name":"Marie","Price":5.0,"stock":5},
    },

    "Gummies":{
        "H1":{"Name":"Albanese","Price":6.0,"stock":10},
        "H2":{"Name":"Ricolino","Price":7.0,"stock":3},
        "H3":{"Name":"Gomitas","Price":8.0,"stock":7},
    }
}


# Function to display the menu
def display_menu():
    print("Welcome to Lynn's Vending Machine!")
    print("Here's the menu:")
    for category, items in menu.items():  # Loop through categories
        print(f"\n{category}:")  # Print category name
        for code, details in items.items():  # Loop through items
            print(f"  {code}: {details['Name']} - AED{details['Price']} (Stock: {details['stock']})")

# Function to handle the customer's selection
def vending_machine():
    display_menu()
    total_money = float(input("\nEnter the amount of money you have: AED "))
    while True:
        category_choice = input("\nSelect a category (chips, chocolates,drinks,cookies,gummies): ").capitalize()
        if category_choice not in menu:
            print("Invalid category. Please try again.")
            continue

        item_code = input(f"Enter the code of the item you want from {category_choice}: ").upper()

        # Check if the item code exists in the selected category
        if item_code in menu[category_choice]:
            item = menu[category_choice][item_code]
            if item["stock"] > 0:
                if total_money >= item["Price"]:
                    total_money -= item["Price"]
                    item["stock"] -= 1
                    print(f"\nDispensing {item['Name']}...")
                    print(f"Your remaining balance is: AED{total_money:.2f}")
                else:
                    print("\nYou don't have enough money for this item.")
            else:
                print("\nSorry, this item is out of stock.")
        else:
            print("\nInvalid item code. Please try again.")

        # Ask the user if they want to buy another item or exit
        continue_choice = input("\nDo you want to buy another item? (yes/no): ").lower()
        if continue_choice != 'yes':
            break

    print("\nThank you for buying from Lynn's vending machine!")
    print(f"Your final change is: AED{total_money:.2f}")

# Run the vending machine
vending_machine()
