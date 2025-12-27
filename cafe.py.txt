from datetime import datetime

menu = {
    "Pizza": 80,
    "Pasta": 110,
    "Burger": 70,
    "Salad": 65,
    "Coffee": 75
}

def display_menu():
    print("\n Welcome to Bastian Restaurant ")
    print("-" * 30)
    for item, price in menu.items():
        print(f"{item}: Rs {price}")

def take_order():
    order_total = 0
    ordered_items = []

    while True:
        item = input("\nEnter item name: ").title()
        if item in menu:
            order_total += menu[item]
            ordered_items.append(item)
            print(f"{item} added to your order ")
        else:
            print("Item not available ")

        more = input("Do you want to add another item? (Yes/No): ").lower()
        if more != "yes":
            break

    return ordered_items, order_total

def generate_bill(items, total):
    print("\n Order Summary")
    print("-" * 30)
    for item in items:
        print(f"{item}: Rs {menu[item]}")

    print(f"\nTotal Amount: Rs {total}")
    print("Thank you for visiting ")

    with open("orders.txt", "a") as f:
        f.write(f"{datetime.now()} - {items} - Rs {total}\n")

# Program starts here
display_menu()
items, total = take_order()
generate_bill(items, total)
