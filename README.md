# Task-5-
#include <iostream>
#include <vector>
#include <string>

struct Book {
    std::string title;
    std::string author;
    bool is_issued;
};

class Library {
private:
    std::vector<Book> books;

public:
    void addBook(const std::string& title, const std::string& author) {
        books.push_back({title, author, false});
        std::cout << "Book added: " << title << " by " << author << std::endl;
    }

    void viewBooks() const {
        if (books.empty()) {
            std::cout << "No books in the library." << std::endl;
        } else {
            std::cout << "Books in the library:" << std::endl;
            for (size_t i = 0; i < books.size(); ++i) {
                std::cout << i + 1 << ". " << books[i].title 
                          << " by " << books[i].author 
                          << " [" << (books[i].is_issued ? "Issued" : "Available") << "]" << std::endl;
            }
        }
    }

    void issueBook(int bookIndex) {
        if (bookIndex < 1 || bookIndex > books.size()) {
            std::cout << "Invalid book number!" << std::endl;
        } else if (books[bookIndex - 1].is_issued) {
            std::cout << "Book already issued!" << std::endl;
        } else {
            books[bookIndex - 1].is_issued = true;
            std::cout << "Book issued: " << books[bookIndex - 1].title << std::endl;
        }
    }

    void returnBook(int bookIndex) {
        if (bookIndex < 1 || bookIndex > books.size()) {
            std::cout << "Invalid book number!" << std::endl;
        } else if (!books[bookIndex - 1].is_issued) {
            std::cout << "Book is not issued!" << std::endl;
        } else {
            books[bookIndex - 1].is_issued = false;
            std::cout << "Book returned: " << books[bookIndex - 1].title << std::endl;
        }
    }

    void deleteBook(int bookIndex) {
        if (bookIndex < 1 || bookIndex > books.size()) {
            std::cout << "Invalid book number!" << std::endl;
        } else {
            std::cout << "Book deleted: " << books[bookIndex - 1].title << " by " << books[bookIndex - 1].author << std::endl;
            books.erase(books.begin() + bookIndex - 1);
        }
    }
};

int main() {
    Library library;
    int choice;

    do {
        std::cout << "\nLibrary Management System Menu:\n";
        std::cout << "1. Add Book\n";
        std::cout << "2. View Books\n";
        std::cout << "3. Issue Book\n";
        std::cout << "4. Return Book\n";
        std::cout << "5. Delete Book\n";
        std::cout << "6. Exit\n";
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1: {
                std::cin.ignore(); // Clear the newline character from the input buffer
                std::string title, author;
                std::cout << "Enter book title: ";
                std::getline(std::cin, title);
                std::cout << "Enter book author: ";
                std::getline(std::cin, author);
                library.addBook(title, author);
                break;
            }
            case 2:
                library.viewBooks();
                break;
            case 3: {
                int bookIndex;
                std::cout << "Enter book number to issue: ";
                std::cin >> bookIndex;
                library.issueBook(bookIndex);
                break;
            }
            case 4: {
                int bookIndex;
                std::cout << "Enter book number to return: ";
                std::cin >> bookIndex;
                library.returnBook(bookIndex);
                break;
            }
            case 5: {
                int bookIndex;
                std::cout << "Enter book number to delete: ";
                std::cin >> bookIndex;
                library.deleteBook(bookIndex);
                break;
            }
            case 6:
                std::cout << "Exiting program." << std::endl;
                break;
            default:
                std::cout << "Invalid choice! Please try again." << std::endl;
        }
    } while (choice != 6);

    return 0;
}
