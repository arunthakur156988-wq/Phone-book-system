#include <stdio.h>
#include <string.h>

#define MAX 100

// Structure for contact
struct Contact {
    char name[50];
    char phone[15];
};

struct Contact phoneBook[MAX];
int count = 0;

// Function to add contact
void addContact() {
    if (count >= MAX) {
        printf("Phone book is full!\n");
        return;
    }

    printf("Enter Name: ");
    scanf(" %[^\n]", phoneBook[count].name);

    printf("Enter Phone Number: ");
    scanf("%s", phoneBook[count].phone);

    count++;
    printf("Contact added successfully!\n");
}

// Function to display contacts
void displayContacts() {
    if (count == 0) {
        printf("Phone book is empty!\n");
        return;
    }

    printf("\n--- Contact List ---\n");
    for (int i = 0; i < count; i++) {
        printf("%d. %s - %s\n", i + 1, phoneBook[i].name, phoneBook[i].phone);
    }
}

// Function to search contact
void searchContact() {
    char name[50];
    int found = 0;

    printf("Enter name to search: ");
    scanf(" %[^\n]", name);

    for (int i = 0; i < count; i++) {
        if (strcmp(phoneBook[i].name, name) == 0) {
            printf("Found: %s - %s\n", phoneBook[i].name, phoneBook[i].phone);
            found = 1;
        }
    }

    if (!found) {
        printf("Contact not found!\n");
    }
}

// Function to delete contact
void deleteContact() {
    char name[50];
    int found = 0;

    printf("Enter name to delete: ");
    scanf(" %[^\n]", name);

    for (int i = 0; i < count; i++) {
        if (strcmp(phoneBook[i].name, name) == 0) {
            for (int j = i; j < count - 1; j++) {
                phoneBook[j] = phoneBook[j + 1];
            }
            count--;
            printf("Contact deleted successfully!\n");
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Contact not found!\n");
    }
}

// Main function
int main() {
    int choice;

    while (1) {
        printf("\n--- Phone Book Menu ---\n");
        printf("1. Add Contact\n");
        printf("2. Display Contacts\n");
        printf("3. Search Contact\n");
        printf("4. Delete Contact\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addContact(); break;
            case 2: displayContacts(); break;
            case 3: searchContact(); break;
            case 4: deleteContact(); break;
            case 5: printf("Exiting...\n"); return 0;
            default: printf("Invalid choice!\n");
        }
    }

    return 0;
}
