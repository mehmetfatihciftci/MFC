class Library:
    def __init__(self):
        self.file_path = "books.txt"
        self.file = open(self.file_path, "a+")

    def __del__(self):
        self.file.close()

    def list_books(self):
        self.file.seek(0)
        book_lines = self.file.read().splitlines()

        for line in book_lines:
            book_info = line.split(',')
            book_title, book_author, release_date, num_pages = book_info
            print(f"Title: {book_title}, Author: {book_author}")

    def add_book(self):
        title = input("Enter book title: ")
        author = input("Enter book author: ")
        release_date = input("Enter release year: ")
        num_pages = input("Enter number of pages: ")

        book_info = f"{title},{author},{release_date},{num_pages}\n"
        self.file.write(book_info)
        print(f"Book '{title}' added successfully.")

    def remove_book(self):
        title_to_remove = input("Enter the title of the book to remove: ")
        book_lines = self.file.readlines()
        self.file.seek(0)
        self.file.truncate()

        for line in book_lines:
            if title_to_remove not in line:
                self.file.write(line)

        print(f"Book '{title_to_remove}' removed successfully.")

# Creating Library object
lib = Library()

# Menu
while True:
    print("\n*** MENU ***")
    print("1) List Books")
    print("2) Add Book")
    print("3) Remove Book")
    print("4) Exit")

    choice = input("Enter your choice (1-4): ")

    if choice == "1":
        lib.list_books()
    elif choice == "2":
        lib.add_book()
    elif choice == "3":
        lib.remove_book()
    elif choice == "4":
        print("Exiting Library Management System. Goodbye!")
        break
    else:
        print("Invalid choice. Please enter a number between 1 and 4.")
