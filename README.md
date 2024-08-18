"# Python-Project-new" 
def welcome_message():3
print("Welcome to the Daily Expense Tracker!\n")


def log_expense():
    while True:
        try:
            amount = float(input("Enter the expense amount: "))
            if amount <= 0:
                print("Amount should be a positive number. Please try again.")
            else:
                break
        except ValueError:
            print("Invalid input. Please enter a number.")

    # Predefined categories
    categories = ["Food", "Transport", "Entertainment", "Other"]
    
    print("\nSelect a category:")
    for i, category in enumerate(categories, 1):
        print(f"{i}. {category}")

    while True:
        try:
            category_choice = int(input("Enter the number corresponding to the category: "))
            if 1 <= category_choice <= len(categories):
                category = categories[category_choice - 1]
                break
            else:
                print("Invalid choice. Please choose a valid category number.")
        except ValueError:
            print("Invalid input. Please enter a number.")
    
    description = input("Enter a description for the expense: ")

    # Create and return the expense dictionary
    return {"amount": amount, "category": category, "description": description}


def display_summary(expenses):
    if not expenses:
        print("No expenses recorded.")
        return

    total_amount = sum(expense["amount"] for expense in expenses)
    print("\n--- Expense Summary ---")
    print(f"Total amount spent: ${total_amount:.2f}\n")
    
    # Calculate total spent per category
    category_totals = {}
    for expense in expenses:
        category = expense["category"]
        amount = expense["amount"]
        if category in category_totals:
            category_totals[category] += amount
        else:
            category_totals[category] = amount
    
    # Display total per category
    print("Total spent per category:")
    for category, total in category_totals.items():
        print(f"{category}: ${total:.2f}")

    # List all expenses with details
    print("\nList of all expenses:")
    for i, expense in enumerate(expenses, 1):
        print(f"{i}. ${expense['amount']:.2f} - {expense['category']} - {expense['description']}")


def thank_you_message():
    print("\nThank you for using the Daily Expense Tracker. Goodbye!")


def main():
    welcome_message()

    expenses = []
    
    while True:
        print("\nWhat would you like to do?")
        print("1. Log a new expense")
        print("2. View expense summary")
        print("3. Exit")

        choice = input("Enter the number corresponding to your choice: ")

        if choice == "1":
            expense = log_expense()
            expenses.append(expense)
            print("Expense logged successfully!")
        elif choice == "2":
            display_summary(expenses)
        elif choice == "3":
            thank_you_message()
            break
        else:
            print("Invalid choice. Please select 1, 2, or 3.")


# Run the program
if __name__ == "__main__":
    main()
