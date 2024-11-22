# Contact Book Program

def display_menu():
    """
    Displays the main menu options for the Contact Book.
    """
    print("\nContact Book Menu:")
    print("1. Add Contact")
    print("2. View Contacts")
    print("3. Search Contact")
    print("4. Update Contact")
    print("5. Delete Contact")
    print("6. Exit")

def add_contact(contact_list):
    """
    Adds a new contact to the contact list.
    """
    name = input("Enter Name: ").strip()
    phone = input("Enter Phone Number: ").strip()
    email = input("Enter Email (optional): ").strip()

    # Check for duplicate names
    if any(contact['name'] == name for contact in contact_list):
        print("A contact with this name already exists.")
        return
    
    contact = {'name': name, 'phone': phone, 'email': email}
    contact_list.append(contact)
    print("Contact added successfully!")

def view_contacts(contact_list):
    """
    Displays all contacts in the contact list.
    """
    if not contact_list:
        print("No contacts found.")
        return
    
    print("\nContact List:")
    for i, contact in enumerate(contact_list, start=1):
        print(f"{i}. Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")

def search_contact(contact_list):
    """
    Searches for a contact by name.
    """
    search_name = input("Enter the name to search: ").strip()
    results = [contact for contact in contact_list if search_name.lower() in contact['name'].lower()]

    if results:
        print("\nSearch Results:")
        for contact in results:
            print(f"Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")
    else:
        print("No matching contacts found.")

def update_contact(contact_list):
    """
    Updates an existing contact.
    """
    name = input("Enter the name of the contact to update: ").strip()
    for contact in contact_list:
        if contact['name'].lower() == name.lower():
            print("Contact found. Leave fields blank to keep the current value.")
            new_name = input(f"New Name (current: {contact['name']}): ").strip() or contact['name']
            new_phone = input(f"New Phone (current: {contact['phone']}): ").strip() or contact['phone']
            new_email = input(f"New Email (current: {contact['email']}): ").strip() or contact['email']
            
            contact.update({'name': new_name, 'phone': new_phone, 'email': new_email})
            print("Contact updated successfully!")
            return
    print("Contact not found.")

def delete_contact(contact_list):
    """
    Deletes a contact by name.
    """
    name = input("Enter the name of the contact to delete: ").strip()
    for contact in contact_list:
        if contact['name'].lower() == name.lower():
            contact_list.remove(contact)
            print("Contact deleted successfully!")
            return
    print("Contact not found.")

def main():
    """
    Main function to run the Contact Book program.
    """
    contact_list = []

    while True:
        display_menu()
        choice = input("Enter your choice (1-6): ").strip()

        if choice == '1':
            add_contact(contact_list)
        elif choice == '2':
            view_contacts(contact_list)
        elif choice == '3':
            search_contact(contact_list)
        elif choice == '4':
            update_contact(contact_list)
        elif choice == '5':
            delete_contact(contact_list)
        elif choice == '6':
            print("Exiting the Contact Book. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

# Run the Contact Book program
if __name__ == "__main__":
    main()
