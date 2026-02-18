# CPP-OOPS-PROGRAMS


#### QUES: create a student class with attributes: name  , roll number, and marks. 
#### Add member functions to input and display student details. 
#### create atleast 3 objects and display their data , cpp program
```
#include <iostream>
using namespace std;

class Student {
private:
    string name;
    int rollNumber;
    float marks;

public:
    // Function to input student details
    void input() {
        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter Roll Number: ";
        cin >> rollNumber;

        cout << "Enter Marks: ";
        cin >> marks;
    }

    // Function to display student details
    void display() {
        cout << "\nStudent Details:" << endl;
        cout << "Name: " << name << endl;
        cout << "Roll Number: " << rollNumber << endl;
        cout << "Marks: " << marks << endl;
    }
};

int main() {
    // Creating 3 objects
    Student s1, s2, s3;

    cout << "Enter details for Student 1" << endl;
    s1.input();

    cout << "\nEnter details for Student 2" << endl;
    s2.input();

    cout << "\nEnter details for Student 3" << endl;
    s3.input();

    // Displaying student data
    cout << "\nDisplaying Student Information";
    s1.display();
    s2.display();
    s3.display();

    return 0;
}
```
<img width="400" height="676" alt="image" src="https://github.com/user-attachments/assets/d09ff82c-566d-4050-8686-bb972ca03ae5" />


#### QUES: create a BankAccount class. 

#### initialize account number and balance using a constructor ,
#### display a message when the destructor is called.  
#### create objects inside a function to observe destructor behvaiour.

```
#include <iostream>
using namespace std;

class BankAccount {
private:
    int accountNumber;
    double balance;

public:
    // Constructor
    BankAccount(int accNo, double bal) {
        accountNumber = accNo;
        balance = bal;
        cout << "Constructor called for Account No: " 
             << accountNumber << endl;
    }

    // Function to display account details
    void display() {
        cout << "Account Number: " << accountNumber << endl;
        cout << "Balance: " << balance << endl;
    }

    // Destructor
    ~BankAccount() {
        cout << "Destructor called for Account No: " 
             << accountNumber << endl;
    }
};

// Function to create objects
void createAccounts() {
    BankAccount acc1(101, 5000.50);
    BankAccount acc2(102, 10000.75);

    cout << "\nInside createAccounts() function\n";
    acc1.display();
    acc2.display();

    // Destructor will be called automatically 
    // when function ends
}

int main() {
    cout << "Program Started\n";

    createAccounts();

    cout << "\nBack in main() function\n";

    return 0;
}
```



<img width="421" height="286" alt="image" src="https://github.com/user-attachments/assets/6d206c5f-ed7b-4bf7-b6d3-c11a8b7b0dd3" />


#### QUES: create an Employee class .
#### make salary private
#### provide getter and setter functions
#### add validation : salary cannot be negative.

```
#include <iostream>
using namespace std;

class Employee {
private:
    double salary;   // Private data member

public:
    // Setter function with validation
    void setSalary(double s) {
        if (s >= 0) {
            salary = s;
        } else {
            cout << "Invalid salary! Salary cannot be negative." << endl;
        }
    }

    // Getter function
    double getSalary() {
        return salary;
    }
};

int main() {
    Employee emp;

    // Setting salary
    emp.setSalary(50000);
    cout << "Employee Salary: " << emp.getSalary() << endl;

    // Trying to set negative salary
    emp.setSalary(-1000);
    cout << "Employee Salary: " << emp.getSalary() << endl;

    return 0;
}
```


<img width="387" height="98" alt="image" src="https://github.com/user-attachments/assets/10622dfb-3bfd-4583-8701-94d39bd95fa2" />


#### QUES: create a class calculator 
#### overload a function add() for:
#### int
#### double
#### three parameters

```
#include <iostream>
using namespace std;

class Calculator {
public:

    // Add two integers
    int add(int a, int b) {
        return a + b;
    }

    // Add two double values
    double add(double a, double b) {
        return a + b;
    }

    // Add three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }
};

int main() {
    Calculator calc;

    cout << "Addition of two integers: "
         << calc.add(10, 20) << endl;

    cout << "Addition of two doubles: "
         << calc.add(5.5, 4.5) << endl;

    cout << "Addition of three integers: "
         << calc.add(1, 2, 3) << endl;

    return 0;
}
```

<img width="337" height="86" alt="image" src="https://github.com/user-attachments/assets/cfe2a096-a57f-42ca-96c5-86024cbcf1af" />


#### QUES: create a struct subject { string name ; int marks:} 

#### create a class student with:
#### private : int roll ; string name; 
#### subject* subjects ; int n ;
#### contructor allocates dynamic  memory for  n subjects 
#### member functions: input() , display () , total() , grade () 
#### store N students using pointer to object array , find topper , and free all memory properly , and explain this code

```
#include <iostream>
using namespace std;

// Structure for Subject
struct Subject {
    string name;
    int marks;
};

class Student {
private:
    int roll;
    string name;
    Subject* subjects;   // Dynamic array of subjects
    int n;               // Number of subjects

public:
    // Constructor
    Student(int numSubjects) {
        n = numSubjects;
        subjects = new Subject[n];   // Dynamic memory allocation
    }

    // Destructor
    ~Student() {
        delete[] subjects;   // Free allocated memory
    }

    // Input function
    void input() {
        cout << "\nEnter Roll Number: ";
        cin >> roll;

        cout << "Enter Name: ";
        cin >> name;

        for (int i = 0; i < n; i++) {
            cout << "\nEnter Subject " << i + 1 << " Name: ";
            cin >> subjects[i].name;

            cout << "Enter Marks: ";
            cin >> subjects[i].marks;
        }
    }

    // Display function
    void display() {
        cout << "\nRoll: " << roll;
        cout << "\nName: " << name;

        for (int i = 0; i < n; i++) {
            cout << "\nSubject: " << subjects[i].name
                 << " Marks: " << subjects[i].marks;
        }

        cout << "\nTotal: " << total();
        cout << "\nGrade: " << grade() << endl;
    }

    // Calculate total marks
    int total() {
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += subjects[i].marks;
        }
        return sum;
    }

    // Calculate grade
    char grade() {
        double avg = total() / (double)n;

        if (avg >= 90) return 'A';
        else if (avg >= 75) return 'B';
        else if (avg >= 50) return 'C';
        else return 'F';
    }

    // Getter for total (used to find topper)
    int getTotal() {
        return total();
    }
};

int main() {
    int N, subjectsCount;

    cout << "Enter number of students: ";
    cin >> N;

    cout << "Enter number of subjects: ";
    cin >> subjectsCount;

    // Dynamic array of Student objects
    Student* students = new Student[N]{ Student(subjectsCount) };

    // Input data
    for (int i = 0; i < N; i++) {
        cout << "\nEnter details for Student " << i + 1;
        students[i].input();
    }

    // Display data
    cout << "\n--- Student Details ---\n";
    for (int i = 0; i < N; i++) {
        students[i].display();
    }

    // Find Topper
    int topperIndex = 0;
    for (int i = 1; i < N; i++) {
        if (students[i].getTotal() > students[topperIndex].getTotal()) {
            topperIndex = i;
        }
    }

    cout << "\nTopper is Student " << topperIndex + 1
         << " with Total Marks: "
         << students[topperIndex].getTotal() << endl;

    // Free memory
    delete[] students;

    return 0;
}
```


<img width="406" height="619" alt="image" src="https://github.com/user-attachments/assets/48036469-ee7b-4b01-920c-1039e1820163" />

<img width="363" height="553" alt="image" src="https://github.com/user-attachments/assets/131e4f8d-f0cb-4c64-bde0-80025bc59ae6" />

#### QUES:Create a struct Node containing :
#### patient data (id , name , severity)
#### node* next 
#### create a class PatientQueue implementing :
#### enqueue (based on severity priority )
#### dequeue
#### display 
#### Use dynamic memory (new/ delete) and demonstrate queue operations

```
#include <iostream>
using namespace std;

// Structure for a Node
struct Node {
    int id;
    string name;
    int severity;   // Higher number = more severe
    Node* next;
};

class PatientQueue {
private:
    Node* front;

public:
    // Constructor
    PatientQueue() {
        front = nullptr;
    }

    // Destructor
    ~PatientQueue() {
        while (front != nullptr) {
            dequeue();
        }
    }

    // Enqueue: Add patient based on severity (priority)
    void enqueue(int id, string name, int severity) {
        Node* newNode = new Node;
        newNode->id = id;
        newNode->name = name;
        newNode->severity = severity;
        newNode->next = nullptr;

        // If queue is empty or new node has higher severity than front
        if (front == nullptr || severity > front->severity) {
            newNode->next = front;
            front = newNode;
        } else {
            // Find proper position
            Node* temp = front;
            while (temp->next != nullptr && temp->next->severity >= severity) {
                temp = temp->next;
            }
            newNode->next = temp->next;
            temp->next = newNode;
        }

        cout << "Patient " << name << " enqueued with severity " << severity << endl;
    }

    // Dequeue: Remove patient from front (highest priority)
    void dequeue() {
        if (front == nullptr) {
            cout << "Queue is empty, cannot dequeue." << endl;
            return;
        }

        Node* temp = front;
        front = front->next;

        cout << "Patient " << temp->name << " dequeued." << endl;
        delete temp;
    }

    // Display all patients
    void display() {
        if (front == nullptr) {
            cout << "Queue is empty." << endl;
            return;
        }

        cout << "\nPatient Queue (High severity → Low severity):\n";
        Node* temp = front;
        while (temp != nullptr) {
            cout << "ID: " << temp->id
                 << " | Name: " << temp->name
                 << " | Severity: " << temp->severity << endl;
            temp = temp->next;
        }
    }
};

int main() {
    PatientQueue pq;

    // Enqueue patients
    pq.enqueue(101, "Alice", 5);
    pq.enqueue(102, "Bob", 8);
    pq.enqueue(103, "Charlie", 3);
    pq.enqueue(104, "Diana", 7);

    // Display queue
    pq.display();

    // Dequeue two patients
    pq.dequeue();
    pq.dequeue();

    // Display queue after dequeue
    pq.display();

    return 0;
}

```
<img width="582" height="547" alt="image" src="https://github.com/user-attachments/assets/bdb74576-804b-469c-99a7-f86d1dd18935" />


#### create a struct BookNode:
#### int id ; string title ; string author ; book issued;
#### BookNode* next
#### create class Library with:
#### BookNode* head

#### addBook() , issueBook(id) , returnBook (id) , searchBook (title) , displayAll()


#### Use pointers to traverse linked list and manage memory safely

```
#include <iostream>
#include <string>
using namespace std;

// Structure for each book
struct BookNode {
    int id;
    string title;
    string author;
    bool issued;       // true = book issued, false = available
    BookNode* next;    // pointer to next book
};

class Library {
private:
    BookNode* head;    // points to first book

public:
    // Constructor
    Library() {
        head = nullptr;
    }

    // Destructor
    ~Library() {
        BookNode* temp;
        while (head != nullptr) {
            temp = head;
            head = head->next;
            delete temp;   // safely delete each node
        }
    }

    // Add a new book at the end
    void addBook(int id, string title, string author) {
        BookNode* newBook = new BookNode;
        newBook->id = id;
        newBook->title = title;
        newBook->author = author;
        newBook->issued = false;
        newBook->next = nullptr;

        if (head == nullptr) {
            head = newBook;
        } else {
            BookNode* temp = head;
            while (temp->next != nullptr)
                temp = temp->next;
            temp->next = newBook;
        }

        cout << "Book \"" << title << "\" added successfully.\n";
    }

    // Issue a book by ID
    void issueBook(int id) {
        BookNode* temp = head;
        while (temp != nullptr) {
            if (temp->id == id) {
                if (!temp->issued) {
                    temp->issued = true;
                    cout << "Book \"" << temp->title << "\" issued successfully.\n";
                } else {
                    cout << "Book \"" << temp->title << "\" is already issued.\n";
                }
                return;
            }
            temp = temp->next;
        }
        cout << "Book with ID " << id << " not found.\n";
    }

    // Return a book by ID
    void returnBook(int id) {
        BookNode* temp = head;
        while (temp != nullptr) {
            if (temp->id == id) {
                if (temp->issued) {
                    temp->issued = false;
                    cout << "Book \"" << temp->title << "\" returned successfully.\n";
                } else {
                    cout << "Book \"" << temp->title << "\" was not issued.\n";
                }
                return;
            }
            temp = temp->next;
        }
        cout << "Book with ID " << id << " not found.\n";
    }

    // Search book by title
    void searchBook(string title) {
        BookNode* temp = head;
        while (temp != nullptr) {
            if (temp->title == title) {
                cout << "Book Found: ID: " << temp->id
                     << " | Author: " << temp->author
                     << " | Status: " << (temp->issued ? "Issued" : "Available") << endl;
                return;
            }
            temp = temp->next;
        }
        cout << "Book \"" << title << "\" not found in library.\n";
    }

    // Display all books
    void displayAll() {
        if (head == nullptr) {
            cout << "Library is empty.\n";
            return;
        }

        BookNode* temp = head;
        cout << "\n--- Library Books ---\n";
        while (temp != nullptr) {
            cout << "ID: " << temp->id
                 << " | Title: " << temp->title
                 << " | Author: " << temp->author
                 << " | Status: " << (temp->issued ? "Issued" : "Available") << endl;
            temp = temp->next;
        }
    }
};

int main() {
    Library lib;

    // Add books
    lib.addBook(101, "The Alchemist", "Paulo Coelho");
    lib.addBook(102, "1984", "George Orwell");
    lib.addBook(103, "To Kill a Mockingbird", "Harper Lee");

    // Display all books
    lib.displayAll();

    // Issue a book
    lib.issueBook(102);

    // Try to issue again
    lib.issueBook(102);

    // Search a book
    lib.searchBook("1984");
    lib.searchBook("The Great Gatsby");

    // Return a book
    lib.returnBook(102);

    // Display all books after return
    lib.displayAll();

    return 0;
}
```

<img width="824" height="433" alt="image" src="https://github.com/user-attachments/assets/eadc0b39-e929-4c4e-9a33-7882f745f527" />




