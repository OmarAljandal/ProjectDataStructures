# ProjectDataStructures
Project for Library using C++ .



#include<iostream>
#include<string>
using namespace std;



// now classes for Book : 


class Book
{

public:
	Book()
	{
		Title = "Unknown";
		Edition = 0;
		PublisherRef = "Unknown";
		Price = 0;
	}
	Book(string title, double edition, string publishRef, double price)
	{
		Title = title;
		Edition = edition;
		PublisherRef = publishRef;
		Price = price;
	}
	void setTitle(string title)
	{
		Title = title;
	}
	void setEidtion(double edition)
	{
		Edition = edition;
	}
	void setPublishRef(string publishRef)
	{
		PublisherRef = publishRef;
	}
	void setPrice(double price)
	{
		Price = price;
	}
	string getTitle()
	{
		return Title;
	}
	double getEdition()
	{
		return Edition;
	}
	string getPublishRef()
	{
		return PublisherRef;
	}
	double getPrice()
	{
		return Price;
	}

	void printBookDetails()
	{
		cout << "The Title of Book is : " << getTitle() << endl;
		cout << "The Edition of Book is : " << getEdition() << endl;
		cout << "The Publisher Reference of Book is : " << getPublishRef() << endl;
		cout << "The Price of Book is : " << getPrice() << endl;
	}

private:
	string Title, PublisherRef;
	double Edition, Price;

};


class Book_Node
{
public:
	Book data;
	Book_Node* next;
	Book_Node() { next = NULL; }
	void DisplayInsideFunctionDisplay()
	{
		cout << "##################\nThe Title of Book is : " << data.getTitle() << endl;
		cout << "\nThe Edition of Book is : " << data.getEdition() << endl;
		cout << "\nThe Publisher Reference of Book is : " << data.getPublishRef() << endl;
		cout << "\nThe Price of Book is : " << data.getPrice() << endl << "##################";
	}
};


class Book_List
{
private:
	Book_Node* head;
	Book_Node* last;
	int length;

	friend class Book_Stack;

public:
	Book_List()
	{
		head = last = NULL;
	}
	void insertBook()
	{
		Book BookInsert;

		string title;
		double edition;
		string publishRef;
		double price;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		BookInsert.setTitle(title);
		BookInsert.setEidtion(edition);
		BookInsert.setPublishRef(publishRef);
		BookInsert.setPrice(price);

		Book_Node* New_Node_Book = new Book_Node;
		New_Node_Book->data = BookInsert;
		if (length == 0)
		{
			head = last = New_Node_Book;
			New_Node_Book->next = NULL;
		}
		else
		{
			head->next = New_Node_Book;
			New_Node_Book->next = NULL;
			last = New_Node_Book;
		}
		length++;

		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;

	}
	void DisplayBook()
	{
		Book_Node* New_Node_Book = new Book_Node;
		if (head == NULL)
			cout << "\nThe List is Empty ..!" << endl;
		else
		{
			New_Node_Book = head;
			int counter = 0; // this is for incrment and for number of books .. 
			while (New_Node_Book != NULL)
			{
				cout << "\nBook Number #" << counter + 1 << endl;
				New_Node_Book->DisplayInsideFunctionDisplay();
				New_Node_Book = New_Node_Book->next;
				counter++;
			}
			cout << endl << "\n\n##################\nThe number of books is " << counter << "\n##################\n";
		}
	}
	void DeleteBook()
	{
		Book_Node* Remove_Node_Book = new Book_Node;
		if (head == NULL)
			cout << "List is Empty  ..!" << endl;
		else
		{
			Remove_Node_Book = head;
			head = head->next;
			delete Remove_Node_Book;
			cout << "\nSuccessfully Deleted ....!" << endl;
		}

	}
	void FindBook()
	{
		string curTitle;
		Book_Node* Current_Node_Book = head;
		cout << "\nEnter the Title of Book You want to find  " << endl
			<< "Be carefull You have to put it correctly " << endl;
		cin >> curTitle;
		if (Current_Node_Book == NULL)
			cout << "List is Empty .. " << endl;
		while (Current_Node_Book != NULL)
		{
			if (Current_Node_Book->data.getTitle() == curTitle)
			{
				Current_Node_Book->DisplayInsideFunctionDisplay();
				break;
			}
			else if (Current_Node_Book->next != NULL)
				Current_Node_Book = Current_Node_Book->next;
			else
			{
				cout << "\nWe cannot found your title sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}
	void ModifyBook()
	{
		string title;
		double edition;
		string publishRef;
		double price;

		string curTitle;
		Book update_Book;
		Book_Node* New_Node_Book;
		New_Node_Book = head;

		cout << "\nEnter the Title of Book You want to Modify" << endl
			<< "Be carefull You have to put it correctly" << endl;
		cin >> curTitle;
		if (New_Node_Book == NULL)
			cout << "\nList is Empty .. " << endl;
		while (New_Node_Book != NULL)
		{
			if (New_Node_Book->data.getTitle() == curTitle)
			{
				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;

				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);

				New_Node_Book->data = update_Book;

				cout << "\nSuccessfully Modified ....!" << endl;
				break;

			}
			else if (New_Node_Book->next != NULL)
				New_Node_Book = New_Node_Book->next;
			else
			{
				cout << "\nWe cannot found your title sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

};

class Book_Stack : public Book_List
{
public:
	Book_Stack() {}
	~Book_Stack() {}

	void push()
	{
		Book BookInsert;

		string title;
		double edition;
		string publishRef;
		double price;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		BookInsert.setTitle(title);
		BookInsert.setEidtion(edition);
		BookInsert.setPublishRef(publishRef);
		BookInsert.setPrice(price);

		Book_Node* New_Node_Book = new Book_Node;
		New_Node_Book->data = BookInsert;
		New_Node_Book->next = head;
		head = New_Node_Book;

		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;
	}
	void pop()
	{
		if (head == NULL)
		{
			cout << "Error: Stack is empty " << endl;
		}
		else
			DeleteBook();
	}
	void DisplayStack()
	{
		DisplayBook();
	}

	void Top() // like Find but Top will print the book in the Top
	{
		Book_Node* Top = head;
		if (head == NULL)
		{
			cout << "Error: Stack is empty " << endl;
		}
		else
			Top->DisplayInsideFunctionDisplay();
	}
	void ModifyStack()
	{
		string title;
		double edition;
		string publishRef;
		double price;

		Book update_Book;
		Book_Node* New_Node_Book;
		New_Node_Book = head;


		if (New_Node_Book == NULL)
			cout << "\nList is Empty .. " << endl;
		while (New_Node_Book != NULL)
		{
			cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
			cout << "Enter Book Title : ";
			cin >> title;
			cout << "Enter Book Edition : ";
			cin >> edition;
			cout << "Enter Publisher Reference of Book : ";
			cin >> publishRef;
			cout << "Enter Price of Book : ";
			cin >> price;

			update_Book.setTitle(title);
			update_Book.setEidtion(edition);
			update_Book.setPublishRef(publishRef);
			update_Book.setPrice(price);

			New_Node_Book->data = update_Book;

			cout << "\nSuccessfully Modified ....!" << endl;
			break;
		}
	}

};

class Book_Queue
{
private:
	Book_Node* front;
	Book_Node* rear;
public:
	Book_Queue() { front = NULL; rear = NULL; }
	void Enqueue()
	{
		Book BookEnqueue;

		string title;
		double edition;
		string publishRef;
		double price;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		BookEnqueue.setTitle(title);
		BookEnqueue.setEidtion(edition);
		BookEnqueue.setPublishRef(publishRef);
		BookEnqueue.setPrice(price);

		Book_Node* New_Node_Book = new Book_Node;
		New_Node_Book->data = BookEnqueue;

		if (rear == NULL)
		{
			front = rear = New_Node_Book;
		}
		else
		{
			rear->next = New_Node_Book;
			rear = New_Node_Book;
		}

		cout << "\nSuccessfully Enqueued ^_^ \n" << endl;
	}

	void DisplayQueue()
	{
		Book_Node* New_Node_Book = new Book_Node;
		if (front == NULL) { cout << "Queue Is Empty ^_^ " << endl; }
		else
		{
			New_Node_Book = front;
			while (New_Node_Book != NULL)
			{
				New_Node_Book->DisplayInsideFunctionDisplay();
				New_Node_Book = New_Node_Book->next;
			}
			cout << endl << endl;
		}
	}

	void Dequeue()
	{
		Book_Node* New_Node_Book = new Book_Node;
		if (front == NULL) { cout << "Queue Is Empty ^_^ " << endl; }
		else
		{
			New_Node_Book = front;
			front = front->next;
			if (front == NULL)
				rear = NULL;
			delete New_Node_Book;
			cout << "\nSuccessfully Dequeued ^_^ \n" << endl;
		}
	}

	void FindQueue()
	{
		string curTitle;
		Book_Node* Current_Node_Book = front;
		cout << "\nEnter the Title of Book You want to find  " << endl
			<< "Be carefull You have to put it correctly " << endl;
		cin >> curTitle;
		if (Current_Node_Book == NULL)
			cout << "Queue is Empty .. " << endl;
		while (Current_Node_Book != NULL)
		{
			if (Current_Node_Book->data.getTitle() == curTitle)
			{
				Current_Node_Book->DisplayInsideFunctionDisplay();
				break;
			}
			else if (Current_Node_Book->next != NULL)
				Current_Node_Book = Current_Node_Book->next;
			else
			{
				cout << "\nWe cannot found your title sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

	void ModifyQueue()
	{
		string title;
		double edition;
		string publishRef;
		double price;

		string curTitle;
		Book update_Book;
		Book_Node* New_Node_Book;
		New_Node_Book = front;

		cout << "\nEnter the Title of Book You want to Modify" << endl
			<< "Be carefull You have to put it correctly" << endl;
		cin >> curTitle;
		if (New_Node_Book == NULL)
			cout << "\nList is Empty .. " << endl;
		while (New_Node_Book != NULL)
		{
			if (New_Node_Book->data.getTitle() == curTitle)
			{
				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;

				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);

				New_Node_Book->data = update_Book;

				cout << "\nSuccessfully Modified Queue ....!" << endl;
				break;

			}
			else if (New_Node_Book->next != NULL)
				New_Node_Book = New_Node_Book->next;
			else
			{
				cout << "\nWe cannot found your title sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

};

// now classes for Author : 


class Author
{
public:
	Author()
	{
		Name = "Unknown";
		Code = "Unknown";
		BookName = "Unknown";
	}
	Author(string name, string code, string bookname)
	{
		Name = name;
		Code = code;
		BookName = bookname;
	}
	void setName(string name)
	{
		Name = name;
	}
	void setCode(string code)
	{
		Code = code;
	}
	void setBookName(string bookname)
	{
		BookName = bookname;
	}

	string getName()
	{
		return Name;
	}
	string getCode()
	{
		return Code;
	}
	string getBookName()
	{
		return BookName;
	}

	void printAuthorInfo()
	{
		cout << "The Name of Author is : " << getName() << endl;
		cout << "The Code of Author is : " << getCode() << endl;
		cout << "The BookName of Author is : " << getBookName() << endl;
	}

private:
	string Name, BookName, Code;
};





class Author_Node
{
public:
	Author data;
	Author_Node* next;
	Book book;
	Author_Node() { next = NULL; }
	void DisplayInsideFunctionDisplay()
	{
		cout << "##################\nThe Name of Author is : " << data.getName() << endl;
		cout << "\nThe Code of Author is : " << data.getCode() << endl;
		cout << "\nThe BookName of Author is : " << data.getBookName() << endl;
		cout << "\nThe Title of Book is : " << book.getTitle() << endl;
		cout << "\nThe Edition of Book is : " << book.getEdition() << endl;
		cout << "\nThe Publisher Reference of Book is : " << book.getPublishRef() << endl;
		cout << "\nThe Price of Book is : " << book.getPrice() << endl << "##################";
	}
};




class Author_List
{
private:
	Author_Node* head;
	Author_Node* last;
	int length;
	friend class Author_Stack;
public:
	Author_List()
	{
		head = last = NULL;
	}
	void insertAuthor()
	{
		Author AuthorInsert;
		Book InsertBook;

		string title;
		double edition;
		string publishRef;
		double price;

		string name;
		string code;
		string bookname;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Author Name : ";
		cin >> name;
		cout << "Enter Author Code : ";
		cin >> code;
		cout << "Enter Author BookName : ";
		cin >> bookname;


		AuthorInsert.setName(name);
		AuthorInsert.setCode(code);
		AuthorInsert.setBookName(bookname);

		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		InsertBook.setTitle(title);
		InsertBook.setEidtion(edition);
		InsertBook.setPublishRef(publishRef);
		InsertBook.setPrice(price);


		Author_Node* New_Node_Author = new Author_Node;
		New_Node_Author->data = AuthorInsert;
		New_Node_Author->book = InsertBook;
		if (length == 0)
		{
			head = last = New_Node_Author;
			New_Node_Author->next = NULL;
		}
		else
		{
			head->next = New_Node_Author;
			New_Node_Author->next = NULL;
			last = New_Node_Author;
		}
		length++;

		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;
	}

	void DisplayAuthor()
	{
		Author_Node* New_Node_Author = new Author_Node;
		if (head == NULL)
			cout << "\nThe List is Empty ..!" << endl;
		else
		{
			New_Node_Author = head;
			int counter = 0; // this is for incrment and for number of books .. 
			while (New_Node_Author != NULL)
			{
				cout << "\nAuthor Number #" << counter + 1 << endl;
				New_Node_Author->DisplayInsideFunctionDisplay();
				New_Node_Author = New_Node_Author->next;
				counter++;
			}
			cout << endl << "\n\n##################\nThe number of Author is " << counter << "\n##################\n";
		}
	}
	void DeleteAuthor()
	{
		Author_Node* Delete_Node_Author = head;
		if (head == NULL)
			cout << "List is Empty  ..!" << endl;
		else
		{
			head = head->next;
			delete Delete_Node_Author;
			cout << "\nSuccessfully Deleted ....!" << endl;
		}

	}
	void FindAuthor()
	{
		string curName;
		Author_Node* Current_Node_Author = head;
		cout << "\nEnter the Name of Author You want to find  " << endl
			<< "Be carefull You have to put it correctly " << endl;
		cin >> curName;
		if (Current_Node_Author == NULL)
			cout << "List is Empty .. " << endl;
		while (Current_Node_Author != NULL)
		{
			if (Current_Node_Author->data.getName() == curName)
			{
				Current_Node_Author->DisplayInsideFunctionDisplay();
				break;
			}
			else if (Current_Node_Author->next != NULL)
				Current_Node_Author = Current_Node_Author->next;
			else
			{
				cout << "\nWe cannot found your name sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

	void ModifyAuthor()
	{
		string name;
		string code;
		string bookname;
		string curName;

		string title;
		double edition;
		string publishRef;
		double price;

		Book update_Book;
		Author update_Author;
		Author_Node* New_Node_Author;
		New_Node_Author = head;

		cout << "\nEnter the Name of Author You want to Modify" << endl
			<< "Be carefull You have to put it correctly" << endl;
		cin >> curName;
		if (New_Node_Author == NULL)
			cout << "\nList is Empty .. " << endl;
		while (New_Node_Author != NULL)
		{
			if (New_Node_Author->data.getName() == curName)
			{
				cout << "\n\nEnter the new data to update the old data of Author\n" << endl;
				cout << "Enter Author Name : ";
				cin >> name;
				cout << "Enter Author Code : ";
				cin >> code;
				cout << "Enter Author BookName : ";
				cin >> bookname;

				update_Author.setName(name);
				update_Author.setCode(code);
				update_Author.setBookName(bookname);


				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;
				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);


				New_Node_Author->data = update_Author;
				New_Node_Author->book = update_Book;

				cout << "\nSuccessfully Modified ....!" << endl;
				break;

			}
			else if (New_Node_Author->next != NULL)
				New_Node_Author = New_Node_Author->next;
			else
			{
				cout << "\nWe cannot found your name sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

};

class Author_Stack : public Author_List
{
public:
	Author_Stack() {}
	~Author_Stack() {}

	void push()
	{
		Author AuthorInsert;
		Book InsertBook;

		string title;
		double edition;
		string publishRef;
		double price;

		string name;
		string code;
		string bookname;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Author Name : ";
		cin >> name;
		cout << "Enter Author Code : ";
		cin >> code;
		cout << "Enter Author BookName : ";
		cin >> bookname;


		AuthorInsert.setName(name);
		AuthorInsert.setCode(code);
		AuthorInsert.setBookName(bookname);

		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		InsertBook.setTitle(title);
		InsertBook.setEidtion(edition);
		InsertBook.setPublishRef(publishRef);
		InsertBook.setPrice(price);

		Author_Node* New_Node_Author = new Author_Node;
		New_Node_Author->data = AuthorInsert;
		New_Node_Author->next = head;
		head = New_Node_Author;
		New_Node_Author->book = InsertBook;

		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;
	}
	void pop()
	{
		if (head == NULL)
		{
			cout << "Error: Stack is empty " << endl;
		}
		else
			DeleteAuthor();
	}
	void DisplayStack()
	{
		DisplayAuthor();
	}

	void Top() // like Find but Top will print the Author in the Top
	{
		Author_Node* Top = head;
		if (head == NULL)
		{
			cout << "Error: Stack is empty " << endl;
		}
		else
			Top->DisplayInsideFunctionDisplay();
	}
	void ModifyStack()
	{
		string name;
		string code;
		string bookname;

		string title;
		double edition;
		string publishRef;
		double price;

		Author update_Author;
		Book update_Book;
		Author_Node* New_Node_Author;
		New_Node_Author = head;


		if (New_Node_Author == NULL)
			cout << "\nList is Empty .. " << endl;
		while (New_Node_Author != NULL)
		{
			cout << "\n\nEnter the new data to update the old data of Author\n" << endl;
			cout << "Enter Author Name : ";
			cin >> name;
			cout << "Enter Author Code : ";
			cin >> code;
			cout << "Enter Author BookName : ";
			cin >> bookname;

			update_Author.setName(name);
			update_Author.setCode(code);
			update_Author.setBookName(bookname);

			cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
			cout << "Enter Book Title : ";
			cin >> title;
			cout << "Enter Book Edition : ";
			cin >> edition;
			cout << "Enter Publisher Reference of Book : ";
			cin >> publishRef;
			cout << "Enter Price of Book : ";
			cin >> price;
			update_Book.setTitle(title);
			update_Book.setEidtion(edition);
			update_Book.setPublishRef(publishRef);
			update_Book.setPrice(price);



			New_Node_Author->data = update_Author;
			New_Node_Author->book = update_Book;


			cout << "\nSuccessfully Modified ....!" << endl;
			break;
		}
	}
};

class Author_Queue
{
private:
	Author_Node* front;
	Author_Node* rear;
public:
	Author_Queue() { front = NULL; rear = NULL; }

	void Enqueue()
	{
		Author AuthorEnqueue;
		Book EnqueueBook;

		string title;
		double edition;
		string publishRef;
		double price;

		string name;
		string code;
		string bookname;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Author Name : ";
		cin >> name;
		cout << "Enter Author Code : ";
		cin >> code;
		cout << "Enter Author BookName : ";
		cin >> bookname;


		AuthorEnqueue.setName(name);
		AuthorEnqueue.setCode(code);
		AuthorEnqueue.setBookName(bookname);

		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		EnqueueBook.setTitle(title);
		EnqueueBook.setEidtion(edition);
		EnqueueBook.setPublishRef(publishRef);
		EnqueueBook.setPrice(price);


		Author_Node* New_Node_Author = new Author_Node;
		New_Node_Author->data = AuthorEnqueue;
		New_Node_Author->book = EnqueueBook;

		if (rear == NULL)
		{
			front = rear = New_Node_Author;
		}
		else
		{
			rear->next = New_Node_Author;
			rear = New_Node_Author;
		}

		cout << "\nSuccessfully Enqueued  .!" << endl << endl << endl;
	}

	void DisplayQueue()
	{
		Author_Node* New_Node_Author = new Author_Node;
		if (front == NULL) { cout << "Queue Is Empty ^_^ " << endl; }
		else
		{
			New_Node_Author = front;
			while (New_Node_Author != NULL)
			{
				New_Node_Author->DisplayInsideFunctionDisplay();
				New_Node_Author = New_Node_Author->next;
			}
			cout << endl << endl;
		}
	}

	void Dequeue()
	{
		Author_Node* new_Node_Author = new Author_Node;
		if (front == NULL) { cout << "Queue Is Empty ^_^ " << endl; }
		else
		{
			new_Node_Author = front;
			front = front->next;
			if (front == NULL)
				rear = NULL;
			delete new_Node_Author;
			cout << "\nSuccessfully Dequeued ^_^ \n" << endl;
		}

	}
	void FindQueue()
	{
		string curName;
		Author_Node* Current_Node_Author = front;
		cout << "\nEnter the Name of Author You want to find  " << endl
			<< "Be carefull You have to put it correctly " << endl;
		cin >> curName;
		if (Current_Node_Author == NULL)
			cout << "Queue is Empty .. " << endl;
		while (Current_Node_Author != NULL)
		{
			if (Current_Node_Author->data.getName() == curName)
			{
				Current_Node_Author->DisplayInsideFunctionDisplay();
				break;
			}
			else if (Current_Node_Author->next != NULL)
				Current_Node_Author = Current_Node_Author->next;
			else
			{
				cout << "\nWe cannot found your name sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

	void ModifyQueue()
	{
		string name;
		string code;
		string bookname;
		string curName;

		string title;
		double edition;
		string publishRef;
		double price;

		Book update_Book;
		Author update_Author;
		Author_Node* New_Node_Author;
		New_Node_Author = front;

		cout << "\nEnter the Name of Author You want to Modify" << endl
			<< "Be carefull You have to put it correctly" << endl;
		cin >> curName;
		if (New_Node_Author == NULL)
			cout << "\Queue is Empty .. " << endl;
		while (New_Node_Author != NULL)
		{
			if (New_Node_Author->data.getName() == curName)
			{
				cout << "\n\nEnter the new data to update the old data of Author\n" << endl;
				cout << "Enter Author Name : ";
				cin >> name;
				cout << "Enter Author Code : ";
				cin >> code;
				cout << "Enter Author BookName : ";
				cin >> bookname;

				update_Author.setName(name);
				update_Author.setCode(code);
				update_Author.setBookName(bookname);


				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;
				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);


				New_Node_Author->data = update_Author;
				New_Node_Author->book = update_Book;

				cout << "\nSuccessfully Modified Queue ....!" << endl;
				break;

			}
			else if (New_Node_Author->next != NULL)
				New_Node_Author = New_Node_Author->next;
			else
			{
				cout << "\nWe cannot found your name sorry ....!!" << endl << endl << endl;
				break;
			}
		}
	}

};

// now class Customer : 

class Customer
{
public:
	Customer()
	{
		CustomerInf = "Unknown";
		ID = 0;
		Total = 0;
		Booklist = 0;

	}
	Customer(string Name, unsigned int id, int booklist, int total)
	{
		CustomerInf = Name;
		ID = id;
		Booklist = booklist;
		Total = total;
	}
	void setID(unsigned int id) { ID = id; }
	void setTotal(int total) { Total = total; }
	void setCustomerInf(string FullName) { CustomerInf = FullName; }
	void setBooklist(int booklist) { Booklist = booklist; }
	double getTotal() { return Total; }
	unsigned int getID() { return ID; }
	string getCustomerInf() { return CustomerInf; }
	int getBooklist() { return Booklist; }
	void printCustomerInf()
	{
		cout << "The name of the customer : " << getCustomerInf() << endl
			<< " ID of the customer : " << getID() << endl
			<< "BOOkList of the customer :" << getBooklist() << endl
			<< "The Total is : " << getTotal() << endl;
	}


private:
	int Total;
	unsigned int ID;
	string CustomerInf;
	int Booklist;

};


class Customer_Node
{
public:
	Customer_Node* next;
	Customer data;
	Book book;
	Customer_Node() { next = NULL; }
	void DisplayInsideFunctionDisplay()
	{
		cout << "##################\nThe name of the customer : " << data.getCustomerInf() << endl
			<< "\nThe ID of the customer : " << data.getID() << endl
			<< "\nThe Booklist of the customer :" << data.getBooklist() << endl
			<< "\nThe total :" << data.getTotal() << endl;

		cout << "\nThe Title of Book is : " << book.getTitle() << endl;
		cout << "\nThe Edition of Book is : " << book.getEdition() << endl;
		cout << "\nThe Publisher Reference of Book is : " << book.getPublishRef() << endl;
		cout << "\nThe Price of Book is : " << book.getPrice() << endl << "##################";

	}
};



class Customer_list
{
public:
	Customer_list() { head = last = NULL; }

	void insertCustomer()
	{
		Customer insertCustomer;
		Book InsertBook;
		string title;
		double edition;
		string publishRef;
		double price;
		string customerinf;
		int booklist;
		unsigned int id;
		int total;

		cout << "---------------\n"
			<< "Insert Menu : \n"
			<< "---------------\n"
			<< "Enter the customer name : ";
		cin >> customerinf;
		cout << "Enter Customer ID :";
		cin >> id;
		cout << "Enter booklist :";
		cin >> booklist;
		cout << "Enter the total :";
		cin >> total;


		insertCustomer.setCustomerInf(customerinf);
		insertCustomer.setID(id);
		insertCustomer.setBooklist(booklist);
		insertCustomer.setTotal(total);

		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		InsertBook.setTitle(title);
		InsertBook.setEidtion(edition);
		InsertBook.setPublishRef(publishRef);
		InsertBook.setPrice(price);
		Customer_Node* newNode = new Customer_Node;
		newNode->data = insertCustomer;
		newNode->book = InsertBook;
		if (length == 0)
		{
			head = last = newNode;
			newNode->next = NULL;

		}
		else
		{
			head->next = newNode;
			newNode->next = NULL;
			last = newNode;
		}length++;
		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;
	}
	void DisplayCustomer()
	{
		Customer_Node* temp = new Customer_Node;
		if (head == NULL)
			cout << "\nThe list is empty ..!" << endl;
		else
		{
			temp = head;
			int counter = 0;

			while (temp != NULL)
			{
				cout << "\nCustomer Number #" << counter + 1 << endl;
				temp->DisplayInsideFunctionDisplay();
				temp = temp->next;
				counter++;
			}cout << "\n\n##################\nNumber of customer is " << counter << "\n##################\n";
		}
	}
	void FindCustomer()
	{
		unsigned int CurrID;
		Customer_Node* currCustomer = head;
		cout << "Enter the ID of the customer you want to find : ";
		cin >> CurrID;
		if (currCustomer == NULL)
			cout << "Empty list \n";
		while (currCustomer != NULL)
		{
			if (currCustomer->data.getID() == CurrID) {

				currCustomer->DisplayInsideFunctionDisplay();
				break;
			}
			else if (currCustomer->next != NULL)
				currCustomer = currCustomer->next;
			else
			{
				cout << " Sorry ...Customer is not found " << endl << endl << endl;
				break;
			}

		}
	}

	void deleteCustomer()
	{
		Customer_Node* DeleteCustomer = new Customer_Node;
		if (head == NULL)
			cout << "Empty list ..!\n";

		else
		{
			DeleteCustomer = head;
			head = head->next;
			delete DeleteCustomer;
			cout << "\nSuccessfully Deleted ....!\n";
		}
	}

	void ModifyCustomer()
	{
		string customerinf;
		int booklist;
		unsigned int id;
		int total;
		// above customer
		string title;
		double edition;
		string publishRef;
		double price;
		// above books

		unsigned int currID;

		Customer updated_Customer;
		Book update_Book;
		Customer_Node* newNode;
		newNode = head;

		cout << "Enter the ID of customer you want to Modify\n";
		cin >> currID;
		if (newNode == NULL)
			cout << "Empty list \n";

		while (newNode != NULL)
		{
			if (newNode->data.getID() == currID)
			{
				cout << "Enter the new data to update the old of customer \n\n";
				cout << "Enter the name of customer : ";
				cin >> customerinf;
				cout << "ID of customer : ";
				cin >> id;
				cout << "Enter the Booklist of customer :";
				cin >> booklist;
				cout << "Enter the total : ";
				cin >> total;

				updated_Customer.setCustomerInf(customerinf);
				updated_Customer.setID(id);
				updated_Customer.setBooklist(booklist);
				updated_Customer.setTotal(total);

				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;
				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);


				newNode->data = updated_Customer;
				newNode->book = update_Book;
				cout << "\nSuccessfully Modified ....!\n"; break;
			}
			else if (newNode->next != NULL)
				newNode = newNode->next;
			else
			{
				cout << " Sorry ...Customer is not found " << endl << endl << endl;
				break;
			}
		}

	}


private:
	Customer_Node* head, * last;
	int length;
	friend class  StackCustomer;

};

class StackCustomer : public Customer_list
{
public:
	StackCustomer() {}
	~StackCustomer() {}
	void push() {
		Customer insertCustomer;
		Book InsertBook;
		string title;
		double edition;
		string publishRef;
		double price;
		string customerinf;
		int booklist;
		unsigned int id;
		int total;

		cout << "---------------\n"
			<< "Insert Menu : \n"
			<< "---------------\n"
			<< "Enter the customer name : ";
		cin >> customerinf;
		cout << "Enter Customer ID :";
		cin >> id;
		cout << "Enter booklist :";
		cin >> booklist;
		cout << "Enter the total :";
		cin >> total;


		insertCustomer.setCustomerInf(customerinf);
		insertCustomer.setID(id);
		insertCustomer.setBooklist(booklist);
		insertCustomer.setTotal(total);

		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		InsertBook.setTitle(title);
		InsertBook.setEidtion(edition);
		InsertBook.setPublishRef(publishRef);
		InsertBook.setPrice(price);
		Customer_Node* newNode = new Customer_Node;
		newNode->data = insertCustomer;
		newNode->next = head;
		head = newNode;
		newNode->book = InsertBook;

		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;
	}

	void pop()
	{
		if (head == NULL)cout << "Error :Stack is empty \n";

		else
			deleteCustomer();
	}

	void displayStackCustomer()
	{
		DisplayCustomer();
	}

	void TopCustomer()
	{
		Customer_Node* Top = head;
		if (head == NULL)
			cout << "Error :Stack is empty \n";
		else
			Top->DisplayInsideFunctionDisplay();
	}

	void ModifyStack()
	{
		string customerinf;
		int booklist;
		unsigned int id;
		int total;
		// above customer
		string title;
		double edition;
		string publishRef;
		double price;
		// above books


		Customer updated_Customer;
		Book update_Book;
		Customer_Node* newNode;
		newNode = head;

		if (newNode == NULL)
			cout << "Empty list \n";

		while (newNode != NULL)
		{
			cout << "Enter the new data to update the old of customer \n\n";
			cout << "Enter the name of customer : ";
			cin >> customerinf;
			cout << "ID of customer : ";
			cin >> id;
			cout << "Enter the Booklist of customer :";
			cin >> booklist;
			cout << "Enter the total : ";
			cin >> total;

			updated_Customer.setCustomerInf(customerinf);
			updated_Customer.setID(id);
			updated_Customer.setBooklist(booklist);
			updated_Customer.setTotal(total);

			cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
			cout << "Enter Book Title : ";
			cin >> title;
			cout << "Enter Book Edition : ";
			cin >> edition;
			cout << "Enter Publisher Reference of Book : ";
			cin >> publishRef;
			cout << "Enter Price of Book : ";
			cin >> price;
			update_Book.setTitle(title);
			update_Book.setEidtion(edition);
			update_Book.setPublishRef(publishRef);
			update_Book.setPrice(price);


			newNode->data = updated_Customer;
			newNode->book = update_Book;
			cout << "\nSuccessfully Modified ....!\n"; break;
		}

	}
};

class Customer_Queue
{
	Customer_Node* front, * rear;

public:
	Customer_Queue() { front = rear = NULL; }
	bool IsEmpty()
	{
		if (front == NULL)
			return true;
		else
			return false;
	}
	void EnqueueCustomer()
	{
		Customer CustomerEnqueue;
		Book BookEnqueue;

		string customer_inf;
		unsigned int id;
		int booklist, total;

		string title;
		double edition;
		string publishRef;
		double price;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Customer Name : ";
		cin >> customer_inf;
		cout << "Enter Customer id : ";
		cin >> id;
		cout << "Enter book list : ";
		cin >> booklist;
		cout << "Enter Total : ";
		cin >> total;

		CustomerEnqueue.setCustomerInf(customer_inf);
		CustomerEnqueue.setID(id);
		CustomerEnqueue.setBooklist(booklist);
		CustomerEnqueue.setTotal(total);

		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		BookEnqueue.setTitle(title);
		BookEnqueue.setEidtion(edition);
		BookEnqueue.setPublishRef(publishRef);
		BookEnqueue.setPrice(price);

		Customer_Node* NewCustomer = new Customer_Node;
		NewCustomer->data = CustomerEnqueue;
		NewCustomer->book = BookEnqueue;

		if (IsEmpty())
		{
			front = rear = NewCustomer;
		}
		else
		{
			rear->next = NewCustomer;
			rear = NewCustomer;
		}
		cout << "\nSuccessfully inserted  .!" << endl << endl << endl;
	}
	void Dequeue()
	{
		Customer_Node* temp = new Customer_Node;
		if (IsEmpty())
			cout << "Error : Queue is empty " << endl;
		else
		{
			temp = front;
			front = front->next;
			delete temp;

			cout << "\nSuccessfully Dequeued \n" << endl;
			if (front == NULL)
				rear = NULL;
		}
	}


	void FindCustomer()
	{
		if (IsEmpty())
			cout << "Error Queue is empty \n";
		else
		{
			unsigned int currID;
			Customer_Node* CurrCustomer = front;
			cout << "Enter ID of Customer you want to find  \n";
			cin >> currID;
			if (CurrCustomer == NULL)
			{
				cout << "Queue is Empty .. " << endl;
			}
			while (CurrCustomer != NULL)
			{
				if (CurrCustomer->data.getID() == currID)
				{
					CurrCustomer->DisplayInsideFunctionDisplay();
					break;
				}
				else if (CurrCustomer->next != NULL)
					CurrCustomer = CurrCustomer->next;

				else
				{
					cout << "Sorry not Customer is Found \n";
					break;
				}
			}


		}
	}


	void ModifyCustomer()
	{
		//For Mdoify customer : 
		string customerinf;
		int booklist;
		unsigned int id;
		int total;
		//For Book : 
		string title;
		double edition;
		string publishRef;
		double price;

		Customer_Node* Newcustomer;
		Newcustomer = front;
		Book UpdatedBook;
		Customer UpdatedCustomer;

		unsigned int CurriD;
		cout << "Enter ID of customer you want to modify : ";
		cin >> CurriD;
		if (Newcustomer == NULL)
			cout << "Queue is Empty " << endl;

		while (Newcustomer != NULL)
		{
			if (Newcustomer->data.getID() == CurriD)
			{
				cout << "Enter the new data to update the customer \n\n";
				cout << "Enter customer name : ";
				cin >> customerinf;
				cout << "Enter Customer ID : ";
				cin >> id;
				cout << "Enter the book list : ";
				cin >> booklist;
				cout << "Enter total : ";
				cin >> total;

				UpdatedCustomer.setCustomerInf(customerinf);
				UpdatedCustomer.setID(id);
				UpdatedCustomer.setBooklist(booklist);
				UpdatedCustomer.setTotal(total);

				cout << "Enter the new data to update the book \n\n";
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;

				UpdatedBook.setTitle(title);
				UpdatedBook.setEidtion(edition);
				UpdatedBook.setPublishRef(publishRef);
				UpdatedBook.setPrice(price);

				Newcustomer->data = UpdatedCustomer;
				Newcustomer->book = UpdatedBook;

				cout << "\nSuccessfully modified ....!\n";
				break;
			}
			else if (Newcustomer->next != NULL)
				Newcustomer = Newcustomer->next;
			else
			{
				cout << "Sorry Customer isn't Found \n";
				break;
			}
		}


	}


	void DisplayCustomer()
	{
		if (IsEmpty())
			cout << "Error Queue is Empty \n";
		else
		{
			Customer_Node* temp = front;
			while (temp != NULL)
			{
				temp->DisplayInsideFunctionDisplay();
				temp = temp->next;
			}
			cout << endl << endl;
		}
	}

};



// now classes stockposition : 


class stockposition
{
public:
	stockposition()
	{
		Copies = 0;
		Availablilty = "Unknown";
	}

	stockposition(int copies, bool availablilty)
	{
		Copies = copies;
		Availablilty = availablilty;
	}

	void setCopies(int copies)
	{
		Copies = copies;
	}

	void setAvailability(bool availablilty)
	{
		Availablilty = availablilty;
	}

	int getCopies()
	{
		return Copies;
	}

	bool getAvailability()
	{
		return Availablilty;
	}

	void printStockPositionDetails()
	{
		cout << "##################\nThe number of copies is: " << getCopies() << "\n";
		cout << "\n Is The Book Available? " << getAvailability() << "\n##################";


	}

private:

	int Copies;
	bool Availablilty;

};


class stockposition_node
{
public:

	stockposition_node* next;
	stockposition data;
	Book book;
	stockposition_node() { next = NULL; }
	void DisplayInsideFunctionDisplay()
	{
		cout << "##################\nThe Title of Book is : " << book.getTitle() << endl;
		cout << "\nThe Edition of Book is : " << book.getEdition() << endl;
		cout << "\nThe Publisher Reference of Book is : " << book.getPublishRef() << endl;
		cout << "\nThe Price of Book is : " << book.getPrice() << endl;

		cout << "\nThe number of copies is: " << data.getCopies() << "\n";
		cout << "\nIs The Book Available? " << data.getAvailability() << "\n##################";
	}

};

class stockposition_list
{
private:
	stockposition_node* head;
	stockposition_node* last;
	int length;
	friend class stockposition_Stack;
public:

	stockposition_list()
	{
		head = last = NULL;
	}

	void Insertstockposition()
	{
		stockposition stockpositionInsert;
		Book InsertBook;
		string title;
		double edition;
		string publishRef;
		double price;

		int copies;
		bool availablilty;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		InsertBook.setTitle(title);
		InsertBook.setEidtion(edition);
		InsertBook.setPublishRef(publishRef);
		InsertBook.setPrice(price);

		cout << "Enter Number of Copies : ";
		cin >> copies;
		cout << "Enter if it's availabl or no:- \nNote:Please Write 1 or 0 just otherwise is not correct : ";
		cin >> availablilty;

		stockpositionInsert.setCopies(copies);
		stockpositionInsert.setAvailability(availablilty);

		stockposition_node* New_Node_stockposition = new stockposition_node;
		New_Node_stockposition->data = stockpositionInsert;
		New_Node_stockposition->book = InsertBook;
		if (length == 0)
		{
			head = last = New_Node_stockposition;
			New_Node_stockposition->next = NULL;
		}
		else
		{
			head->next = New_Node_stockposition;
			New_Node_stockposition->next = NULL;
			last = New_Node_stockposition;
		}
		length++;
		cout << "\nSuccessfully inserted  .!" << "\n\n\n";




	}

	void Displaystockposition()
	{
		stockposition_node* New_Node_stockposition = new stockposition_node;
		if (head == NULL)
		{
			cout << "\nThe List is Empty ..!" << endl;
		}
		else
		{
			New_Node_stockposition = head;
			int counter = 0;
			while (New_Node_stockposition != NULL)
			{
				cout << "\nStockposition Number #" << counter + 1 << "\n";
				New_Node_stockposition->DisplayInsideFunctionDisplay();
				New_Node_stockposition = New_Node_stockposition->next;
				counter++;
			}
			cout << "\n##################\nThe number of stockposition is: " << counter << "\n";
		}
	}

	void Deletestockposition()
	{
		stockposition_node* New_Node_stockposition = new stockposition_node;
		if (head == NULL)
			cout << "List is Empty .. \n";
		else
		{
			New_Node_stockposition = head;
			head = head->next;
			delete New_Node_stockposition;
			cout << "\nSuccessfully Deleted  .!\n";
		}
	}

	void Findstockposition()
	{
		string curTitle;
		stockposition_node* Current_Node_stockposition = head;
		cout << "\nEnter the Title of book inside stockposition You want to find  \n"
			<< "Be carefull You have to put it correctly \n";
		cin >> curTitle;
		if (Current_Node_stockposition == NULL)
			cout << "List is Empty .. \n";
		while (Current_Node_stockposition != NULL)
		{
			if (Current_Node_stockposition->book.getTitle() == curTitle)
			{
				Current_Node_stockposition->DisplayInsideFunctionDisplay();
				break;
			}
			else if (Current_Node_stockposition->next != NULL)
				Current_Node_stockposition = Current_Node_stockposition->next;
			else
			{
				cout << "\nWe cannot found your Title sorry ....!!\n\n\n";
				break;
			}
		}
	}
	void Modifystockposition()
	{
		int copies;
		bool availablilty;

		string title;
		double edition;
		string publishRef;
		double price;

		string curTitle;

		stockposition update_stockposition;
		Book update_Book;

		stockposition_node* New_Node_stockposition;
		New_Node_stockposition = head;

		cout << "\nEnter the Title of book inside stockposition You want to Modify  \n"
			<< "Be carefull You have to put it correctly \n";
		cin >> curTitle;
		if (New_Node_stockposition == NULL)
			cout << "List is Empty .. \n";
		while (New_Node_stockposition != NULL)
		{
			if (New_Node_stockposition->book.getTitle() == curTitle)
			{
				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;
				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);

				cout << "\n\nEnter the new data to update the old data of stockposition\n\n";
				cout << "Enter Stockposition Copies: ";
				cin >> copies;
				cout << "Enter if it's availabl or no:- \nNote:Please Write 1 or 0 just otherwise is not correct : ";
				cin >> availablilty;


				update_stockposition.setAvailability(availablilty);
				update_stockposition.setCopies(copies);


				New_Node_stockposition->data = update_stockposition;
				New_Node_stockposition->book = update_Book;

				cout << "\nSuccessfully Modified ....!" << endl;
				break;
			}
			else if (New_Node_stockposition->next != NULL)
				New_Node_stockposition = New_Node_stockposition->next;
			else
			{
				cout << "\nWe cannot found your Title sorry ....!!\n\n\n";
				break;
			}
		}
	}

};

class stockposition_Stack : public stockposition_list
{
public:
	stockposition_Stack() {}
	~stockposition_Stack() {}
	void push()
	{
		stockposition stockpositionInsert;
		Book InsertBook;
		string title;
		double edition;
		string publishRef;
		double price;

		int copies;
		bool availablilty;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		InsertBook.setTitle(title);
		InsertBook.setEidtion(edition);
		InsertBook.setPublishRef(publishRef);
		InsertBook.setPrice(price);

		cout << "Enter Number of Copies : ";
		cin >> copies;
		cout << "Enter if it's availabl or no:- \nNote:Please Write 1 or 0 just otherwise is not correct : ";
		cin >> availablilty;

		stockpositionInsert.setCopies(copies);
		stockpositionInsert.setAvailability(availablilty);

		stockposition_node* New_Node_stockposition = new stockposition_node;
		New_Node_stockposition->data = stockpositionInsert;
		New_Node_stockposition->next = head;
		head = New_Node_stockposition;
		New_Node_stockposition->book = InsertBook;

		cout << "\nSuccessfully inserted  .!" << "\n\n\n";
	}

	void pop()
	{
		if (head == NULL)
		{
			cout << "Error: Stack is empty " << endl;
		}
		else
			Deletestockposition();
	}
	void Displaystack()
	{
		Displaystockposition();
	}
	void Top()
	{
		stockposition_node* Top = head;
		if (head == NULL)
		{
			cout << "Error: Stack is empty " << endl;
		}
		else
			Top->DisplayInsideFunctionDisplay();
	}
	void ModifyStack()
	{
		int copies;
		bool availablilty;

		string title;
		double edition;
		string publishRef;
		double price;

		stockposition update_stockposition;
		Book update_Book;

		stockposition_node* New_Node_stockposition;
		New_Node_stockposition = head;

		if (New_Node_stockposition == NULL)
			cout << "List is Empty .. \n";
		while (New_Node_stockposition != NULL)
		{
			cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
			cout << "Enter Book Title : ";
			cin >> title;
			cout << "Enter Book Edition : ";
			cin >> edition;
			cout << "Enter Publisher Reference of Book : ";
			cin >> publishRef;
			cout << "Enter Price of Book : ";
			cin >> price;
			update_Book.setTitle(title);
			update_Book.setEidtion(edition);
			update_Book.setPublishRef(publishRef);
			update_Book.setPrice(price);

			cout << "\n\nEnter the new data to update the old data of stockposition\n\n";
			cout << "Enter Stockposition Copies: ";
			cin >> copies;
			cout << "Enter if it's availabl or no:- \nNote:Please Write 1 or 0 just otherwise is not correct : ";
			cin >> availablilty;


			update_stockposition.setAvailability(availablilty);
			update_stockposition.setCopies(copies);


			New_Node_stockposition->data = update_stockposition;
			New_Node_stockposition->book = update_Book;

			cout << "\nSuccessfully Modified ....!" << endl;
			break;
		}
	}

};

class stockposition_Queue
{
private:
	stockposition_node* front;
	stockposition_node* rear;
public:

	stockposition_Queue()
	{
		front = NULL;
		rear = NULL;
	}

	void Enqueue()
	{
		stockposition stockpositionEnqueue;
		Book BookEnqueue;
		string title;
		double edition;
		string publishRef;
		double price;

		int copies;
		bool availablilty;

		cout << "------------------ \n";
		cout << "Insert Menu : \n";
		cout << "------------------ \n";
		cout << "Enter Book Title : ";
		cin >> title;
		cout << "Enter Book Edition : ";
		cin >> edition;
		cout << "Enter Publisher Reference of Book : ";
		cin >> publishRef;
		cout << "Enter Price of Book : ";
		cin >> price;

		BookEnqueue.setTitle(title);
		BookEnqueue.setEidtion(edition);
		BookEnqueue.setPublishRef(publishRef);
		BookEnqueue.setPrice(price);


		cout << "Enter Number of Copies : ";
		cin >> copies;
		cout << "Enter if it's availabl or no:- \nNote:Please Write 1 or 0 just otherwise is not correct : ";
		cin >> availablilty;

		stockpositionEnqueue.setCopies(copies);
		stockpositionEnqueue.setAvailability(availablilty);

		stockposition_node* New_Node_stockposition = new stockposition_node;
		New_Node_stockposition->data = stockpositionEnqueue;
		New_Node_stockposition->book = BookEnqueue;
		if (rear == NULL)
		{
			front = rear = New_Node_stockposition;
		}
		else
		{
			rear->next = New_Node_stockposition;
			rear = New_Node_stockposition;
		}
		cout << "\nSuccessfully Enqueued  .!" << "\n\n\n";




	}

	void DisplayQueue()
	{
		stockposition_node* New_Node_stockposition = front;

		if (front == NULL)
		{
			cout << "\nThe Queue is Empty ..!" << endl;
		}
		else
		{
			while (New_Node_stockposition != NULL)
			{
				New_Node_stockposition->DisplayInsideFunctionDisplay();
				New_Node_stockposition = New_Node_stockposition->next;
			}
			cout << endl << endl;
		}
	}

	void Dequeue()
	{
		stockposition_node* New_Node_stockposition = new stockposition_node;
		if (front == NULL)
			cout << "Queue is Empty .. \n";
		else
		{
			New_Node_stockposition = front;
			front = front->next;
			if (front == NULL)
				rear = NULL;
			delete New_Node_stockposition;
			cout << "\nSuccessfully Dequeued  .!\n";
		}
	}

	void FindQueue()
	{
		string curTitle;
		stockposition_node* Current_Node_stockposition = front;
		cout << "\nEnter the Title of book inside stockposition You want to find  \n"
			<< "Be carefull You have to put it correctly \n";
		cin >> curTitle;
		if (Current_Node_stockposition == NULL)
			cout << "Queue is Empty .. \n";
		while (Current_Node_stockposition != NULL)
		{
			if (Current_Node_stockposition->book.getTitle() == curTitle)
			{
				Current_Node_stockposition->DisplayInsideFunctionDisplay();
				break;
			}
			else if (Current_Node_stockposition->next != NULL)
				Current_Node_stockposition = Current_Node_stockposition->next;
			else
			{
				cout << "\nWe cannot found your Title sorry ....!!\n\n\n";
				break;
			}
		}
	}
	void ModifyQueue()
	{


		int copies;
		bool availablilty;

		string title;
		double edition;
		string publishRef;
		double price;

		string curTitle;

		stockposition update_stockposition;
		Book update_Book;

		stockposition_node* New_Node_stockposition;
		New_Node_stockposition = front;

		cout << "\nEnter the Title of book inside stockposition You want to Modify  \n"
			<< "Be carefull You have to put it correctly \n";
		cin >> curTitle;
		if (New_Node_stockposition == NULL)
			cout << "Queue is Empty .. \n";
		while (New_Node_stockposition != NULL)
		{
			if (New_Node_stockposition->book.getTitle() == curTitle)
			{
				cout << "\n\nEnter the new data to update the old data of Book\n" << endl;
				cout << "Enter Book Title : ";
				cin >> title;
				cout << "Enter Book Edition : ";
				cin >> edition;
				cout << "Enter Publisher Reference of Book : ";
				cin >> publishRef;
				cout << "Enter Price of Book : ";
				cin >> price;
				update_Book.setTitle(title);
				update_Book.setEidtion(edition);
				update_Book.setPublishRef(publishRef);
				update_Book.setPrice(price);

				cout << "\n\nEnter the new data to update the old data of stockposition\n\n";
				cout << "Enter Stockposition Copies: ";
				cin >> copies;
				cout << "Enter if it's availabl or no:- \nNote:Please Write 1 or 0 just otherwise is not correct : ";
				cin >> availablilty;


				update_stockposition.setAvailability(availablilty);
				update_stockposition.setCopies(copies);


				New_Node_stockposition->data = update_stockposition;
				New_Node_stockposition->book = update_Book;

				cout << "\nSuccessfully Modified Queue ....!" << endl;
				break;
			}
			else if (New_Node_stockposition->next != NULL)
				New_Node_stockposition = New_Node_stockposition->next;
			else
			{
				cout << "\nWe cannot found your Titile sorry ....!!\n\n\n";
				break;
			}
		}
	}

};






char Menus();
char Menus2();
char Menus3();
int main() {
	char i;

abc:
	cout << " \t \t  Book company \t\n";
	cout << "Choose what you want : " << endl;
	cout << "L. Linked List " << endl;
	cout << "S. Stack " << endl;
	cout << "Q. Queue " << endl;
	cout << "E. End the Program " << endl;
	cout << "\n\n\nNOTE: you have to choose one of them : " << endl;
	cin >> i;



	char a;
	char ch;
	if (i == 'L')
	{
		Book_List b;
		Author_List u;
		Customer_list c;
		stockposition_list s;
		while (1) {
			cout << "\n\n\nWelcome To Linked List Word \n\n\n" << endl;
			cout << " \t \t  Book company \t\n";
			cout << "\t\t  MAIN MENU \n\n";
			cout << "B. Book " << endl << endl;
			cout << "A. Author " << endl << endl;
			cout << "C. Customer " << endl << endl;
			cout << "S. Stockposition " << endl << endl;
			cout << "E. Exit " << endl;



			cout << "Select your option (B for Book or A for Author or C for Customer or S Stockposition or E for Exit): "; cin >> a;
			if (a == 'E')
			{
				cout << "\n\n\n\nSee You Later  in Linked List ....!" << endl;
				goto abc;
			}
			cout << endl << endl;

			switch (a)
			{
			case 'B':
				ch = Menus();
				if (ch == 'd')
					b.DisplayBook();
				else if (ch == 'i')
					b.insertBook();
				else if (ch == 'r')
					b.DeleteBook();
				else if (ch == 'm')
					b.ModifyBook();
				else if (ch == 'f')
					b.FindBook();
				break;

			case 'A':
				ch = Menus();
				if (ch == 'd')
					u.DisplayAuthor();
				else if (ch == 'i')
					u.insertAuthor();
				else if (ch == 'r')
					u.DeleteAuthor();
				else if (ch == 'm')
					u.ModifyAuthor();
				else if (ch == 'f')
					b.FindBook();
				break;

			case 'C':
				ch = Menus();
				if (ch == 'd')
					c.DisplayCustomer();
				else if (ch == 'i')
					c.insertCustomer();
				else if (ch == 'r')
					c.deleteCustomer();
				else if (ch == 'm')
					c.ModifyCustomer();
				else if (ch == 'f')
					c.FindCustomer();
				break;

			case 'S':
				ch = Menus();
				if (ch == 'd')
					s.Displaystockposition();
				else if (ch == 'i')
					s.Insertstockposition();
				else if (ch == 'r')
					s.Deletestockposition();
				else if (ch == 'm')
					s.Modifystockposition();
				else if (ch == 'f')
					s.Findstockposition();
				break;


			default:
				cout << "Please Enter Letter Form B for Book or A for Author or C for Customer or S Stockposition or E for Exit" << endl <<
					"NOTE: You Have to put Captial Letter " << endl;
				break;
			}
		}


	}
	else if (i == 'S')
	{
		Book_Stack b;
		Author_Stack u;
		StackCustomer c;
		stockposition_Stack s;
		while (1) {
			cout << "\n\nWelcome To Stack Word \n\n\n" << endl;
			cout << " \t \t  Book company \t\n";
			cout << "\t\t  MAIN MENU \n\n";
			cout << "B. Book " << endl << endl;
			cout << "A. Author " << endl << endl;
			cout << "C. Customer " << endl << endl;
			cout << "S. Stockposition " << endl << endl;
			cout << "E. Exit " << endl;



			cout << "Select your option (B for Book or A for Author or C for Customer or S Stockposition or E for Exit): "; cin >> a;
			if (a == 'E')
			{
				cout << "\n\n\n\nSee You Later in Stack ......!" << endl;
				goto abc;
			}
			cout << endl << endl;

			switch (a)
			{
			case 'B':
				ch = Menus2();
				if (ch == 'd')
					b.DisplayStack();
				else if (ch == 'i')
					b.push();
				else if (ch == 'r')
					b.pop();
				else if (ch == 'm')
					b.ModifyStack();
				else if (ch == 'f')
					b.Top();
				break;

			case 'A':
				ch = Menus2();
				if (ch == 'd')
					u.DisplayStack();
				else if (ch == 'i')
					u.push();
				else if (ch == 'r')
					u.pop();
				else if (ch == 'm')
					u.ModifyStack();
				else if (ch == 'f')
					u.Top();
				break;

			case 'C':
				ch = Menus2();
				if (ch == 'd')
					c.displayStackCustomer();
				else if (ch == 'i')
					c.push();
				else if (ch == 'r')
					c.pop();
				else if (ch == 'm')
					c.ModifyStack();
				else if (ch == 'f')
					c.TopCustomer();
				break;

			case 'S':
				ch = Menus2();
				if (ch == 'd')
					s.Displaystack();
				else if (ch == 'i')
					s.push();
				else if (ch == 'r')
					s.pop();
				else if (ch == 'm')
					s.ModifyStack();
				else if (ch == 'f')
					s.Top();
				break;

			default:
				cout << "Please Enter Letter Form B for Book or A for Author or C for Customer or S Stockposition or E for Exit" << endl <<
					"NOTE: You Have to put Captial Letter " << endl;
				break;
			}



		}
	}
	else if (i == 'Q')
	{
		Book_Queue b;
		Author_Queue u;
		Customer_Queue c;
		stockposition_Queue s;
		while (1) {


			cout << "\n\nWelcome To Queue Word \n\n\n" << endl;
			cout << " \t \t  Book company \t\n";
			cout << "\t\t  MAIN MENU \n\n";
			cout << "B. Book " << endl << endl;
			cout << "A. Author " << endl << endl;
			cout << "C. Customer " << endl << endl;
			cout << "S. Stockposition " << endl << endl;
			cout << "E. Exit " << endl;



			cout << "Select your option (B for Book or A for Author or C for Customer or S Stockposition or E for Exit): "; cin >> a;
			if (a == 'E')
			{
				cout << "\n\n\n\nSee You Later in Queue .....!" << endl;
				goto abc;
			}
			cout << endl << endl;

			switch (a)
			{
			case 'B':
				ch = Menus3();
				if (ch == 'd')
					b.DisplayQueue();
				else if (ch == 'i')
					b.Enqueue();
				else if (ch == 'r')
					b.Dequeue();
				else if (ch == 'm')
					b.ModifyQueue();
				else if (ch == 'f')
					b.FindQueue();
				break;

			case 'A':
				ch = Menus3();
				if (ch == 'd')
					u.DisplayQueue();
				else if (ch == 'i')
					u.Enqueue();
				else if (ch == 'r')
					u.Dequeue();
				else if (ch == 'm')
					u.ModifyQueue();
				else if (ch == 'f')
					u.FindQueue();
				break;

			case 'C':
				ch = Menus3();
				if (ch == 'd')
					c.DisplayCustomer();
				else if (ch == 'i')
					c.EnqueueCustomer();
				else if (ch == 'r')
					c.Dequeue();
				else if (ch == 'm')
					c.ModifyCustomer();
				else if (ch == 'f')
					c.FindCustomer();
				break;

			case 'S':
				ch = Menus3();
				if (ch == 'd')
					s.DisplayQueue();
				else if (ch == 'i')
					s.Enqueue();
				else if (ch == 'r')
					s.Dequeue();
				else if (ch == 'm')
					s.ModifyQueue();
				else if (ch == 'f')
					s.FindQueue();
				break;

			default:
				cout << "Please Enter Letter Form B for Book or A for Author or C for Customer or S Stockposition or E for Exit" << endl <<
					"NOTE: You Have to put Captial Letter " << endl;
				break;
			}



		}
	}

	else if (i == 'E')
	{
		cout << "\n\n\nSee u next time ^___^ ..!\n\n\n\n" << endl;
		goto cba;

	}

	else
	{
		cout << "Sorry choose Captial Letter or correct letter " << endl;
		goto abc;
	}


cba:
	return 0;
}


char Menus() {
	char a;
	cout << " \t \t       Book Company \t\n";
	cout << "\t\t\tSub_MENU \n\n";
	cout << "(d) Display" << endl << endl;
	cout << "(i) Insert" << endl << endl;
	cout << "(r) Delete" << endl << endl;
	cout << "(m) Modify" << endl << endl;
	cout << "(f) Find" << endl << endl;

	cout << "Select your option (above): "; cin >> a;
	return a;
}

char Menus2()
{
	char a;
	cout << " \t \t       Book Company \t\n";
	cout << "\t\t\tSub_MENU \n\n";
	cout << "(d) Display _ Stack" << endl << endl;
	cout << "(i) Insert _ Stack'Push'" << endl << endl;
	cout << "(r) Delete _ Stack'Pop'" << endl << endl;
	cout << "(m) Modify _ Stack" << endl << endl;
	cout << "(f) Find _ Stack'Top'" << endl << endl;

	cout << "Select your option (above): "; cin >> a;
	return a;
}

char Menus3()
{
	char a;
	cout << " \t \t       Book Company \t\n";
	cout << "\t\t\tSub_MENU \n\n";
	cout << "(d) Display _ Queue" << endl << endl;
	cout << "(i) Insert _ Queue'Enqueue'" << endl << endl;
	cout << "(r) Delete _ Queue'Dequeue'" << endl << endl;
	cout << "(m) Modify _ Queue" << endl << endl;
	cout << "(f) Find _ Queue" << endl << endl;

	cout << "Select your option (above): "; cin >> a;
	return a;
}
