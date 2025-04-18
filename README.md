# Phonebook application using binary search

def binary_search(contacts, target):
    """Binary search to find contact index by name (case-insensitive)"""
    low, high = 0, len(contacts) - 1
    target = target.lower()
    while low <= high:
        mid = (low + high) // 2
        mid_name = contacts[mid][0].lower()
        if mid_name == target:
            return mid
        elif mid_name < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

def add_contact(contacts):
    """Add a new contact to the phonebook"""
    name = input("Enter name: ").strip()
    phone = input("Enter phone number: ").strip()
    contacts.append((name, phone))
    contacts.sort(key=lambda x: x[0].lower())  # keep sorted for binary search
    print("Contact added successfully.")

def delete_contact(contacts):
    """Delete a contact by name"""
    name = input("Enter name to delete: ").strip()
    index = binary_search(contacts, name)
    if index != -1:
        deleted = contacts.pop(index)
        print(f"Contact '{deleted[0]}' deleted.")
    else:
        print("Contact not found.")

def search_contact(contacts):
    """Search for a contact by name"""
    name = input("Enter name to search: ").strip()
    index = binary_search(contacts, name)
    if index != -1:
        print(f"Contact found: {contacts[index][0]} - {contacts[index][1]}")
    else:
        print("Contact not found.")

def display_contacts(contacts):
    """Display all contacts"""
    if not contacts:
        print("Phonebook is empty.")
    else:
        print("\n--- All Contacts ---")
        for name, phone in contacts:
            print(f"{name} - {phone}")
        print("---------------------")

def main():
    contacts = []

    while True:
        print("\n===== Phonebook Menu =====")
        print("1. Add Contact")
        print("2. Delete Contact")
        print("3. Search Contact")
        print("4. Display All Contacts")
        print("5. Exit")

        choice = input("Choose an option (1-5): ").strip()

        if choice == '1':
            add_contact(contacts)
        elif choice == '2':
            delete_contact(contacts)
        elif choice == '3':
            search_contact(contacts)
        elif choice == '4':
            display_contacts(contacts)
        elif choice == '5':
            print("Exiting Phonebook. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
