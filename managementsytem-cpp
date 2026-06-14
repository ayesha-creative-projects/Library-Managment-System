#include <iostream>
#include <string>
using namespace std;

const int MAX_RESOURCES = 50;
const int MAX_MEMBERS = 50;
const int MAX_BORROWED = 20;

class Library;
class LibraryMember;

// ============================================================
//  Base Class: LibraryResource
// ============================================================
class LibraryResource
{
    friend void adminView(const Library &lib, const LibraryMember members[], int memberCount);

protected:
    int resourceID;
    string title;
    string author;
    bool isAvailable;

public:
    LibraryResource()
        : resourceID(0), title(""), author(""), isAvailable(true) {}

    LibraryResource(int id, string t, string a, bool avail = true)
        : resourceID(id), title(t), author(a), isAvailable(avail) {}

    int getResourceID() const { return resourceID; }
    string getTitle() const { return title; }
    string getAuthor() const { return author; }
    bool getIsAvailable() const { return isAvailable; }

    // this pointer usage #1: setter distinguishes parameter from member variable
    void setResourceID(int resourceID) { this->resourceID = resourceID; }
    void setTitle(string title) { this->title = title; }
    void setAuthor(string author) { this->author = author; }
    void setIsAvailable(bool isAvailable) { this->isAvailable = isAvailable; }

    void displayDetails() const
    {
        cout << "  ID     : " << resourceID << "\n"
             << "  Title  : " << title << "\n"
             << "  Author : " << author << "\n"
             << "  Status : " << (isAvailable ? "Available" : "Borrowed") << "\n";
    }

    double calculateLateFee(int daysLate) const
    {
        return daysLate * 1.0; // base rate: Rs. 1/day
    }
};

// ============================================================
//  Derived Class: Book
//  Function hiding: re-declares calculateLateFee & displayDetails
//  without virtual/override — hides the base class versions
// ============================================================
class Book : public LibraryResource
{
private:
    string ISBN;
    int pageCount;

public:
    Book() : LibraryResource(), ISBN(""), pageCount(0) {}
    Book(int id, string t, string a, string isbn, int pages)
        : LibraryResource(id, t, a, true), ISBN(isbn), pageCount(pages) {}

    string getISBN() const { return ISBN; }
    int getPageCount() const { return pageCount; }

    // this pointer usage #2: setter returns *this for method chaining
    Book &setISBN(string isbn)
    {
        this->ISBN = isbn; // 'this' distinguishes member from parameter
        return *this;      // returns current object for chaining
    }
    void setPageCount(int pageCount) { this->pageCount = pageCount; }

    // Function hiding (no override keyword) — hides LibraryResource::calculateLateFee
    double calculateLateFee(int daysLate) const
    {
        return daysLate * 5.0; // Rs. 5/day for books
    }

    // Function hiding — hides LibraryResource::displayDetails
    void displayDetails() const
    {
        cout << "  [Book]\n";
        LibraryResource::displayDetails(); // explicitly call base version
        cout << "  ISBN   : " << ISBN << "\n"
             << "  Pages  : " << pageCount << "\n";
    }
};

// ============================================================
//  Derived Class: Magazine
//  Function hiding: hides base calculateLateFee & displayDetails
// ============================================================
class Magazine : public LibraryResource
{
private:
    int issueNumber;

public:
    Magazine() : LibraryResource(), issueNumber(0) {}
    Magazine(int id, string t, string a, int issue)
        : LibraryResource(id, t, a, true), issueNumber(issue) {}

    int getIssueNumber() const { return issueNumber; }
    void setIssueNumber(int issueNumber) { this->issueNumber = issueNumber; }

    // Function hiding — hides LibraryResource::calculateLateFee
    double calculateLateFee(int daysLate) const
    {
        return daysLate * 3.0; // Rs. 3/day for magazines
    }

    // Function hiding — hides LibraryResource::displayDetails
    void displayDetails() const
    {
        cout << "  [Magazine]\n";
        LibraryResource::displayDetails();
        cout << "  Issue  : " << issueNumber << "\n";
    }
};

// ============================================================
//  Derived Class: DVD
//  Function hiding: hides base calculateLateFee & displayDetails
// ============================================================
class DVD : public LibraryResource
{
private:
    int duration;

public:
    DVD() : LibraryResource(), duration(0) {}
    DVD(int id, string t, string a, int dur)
        : LibraryResource(id, t, a, true), duration(dur) {}

    int getDuration() const { return duration; }
    void setDuration(int duration) { this->duration = duration; }

    // Function hiding — hides LibraryResource::calculateLateFee
    double calculateLateFee(int daysLate) const
    {
        return daysLate * 10.0; // Rs. 10/day for DVDs
    }

    // Function hiding — hides LibraryResource::displayDetails
    void displayDetails() const
    {
        cout << "  [DVD]\n";
        LibraryResource::displayDetails();
        cout << "  Dur(m) : " << duration << "\n";
    }
};

// ============================================================
//  LibraryMember  (Composition with LibraryResource)
// ============================================================
class LibraryMember
{
    friend void adminView(const Library &lib, const LibraryMember members[], int memberCount);

private:
    int memberID;
    string name;
    LibraryResource borrowedItems[MAX_BORROWED]; // by value = composition
    int borrowCount;

public:
    LibraryMember() : memberID(0), name(""), borrowCount(0) {}
    LibraryMember(int id, string n) : memberID(id), name(n), borrowCount(0) {}

    int getMemberID() const { return memberID; }
    string getName() const { return name; }
    int getBorrowCount() const { return borrowCount; }

    // this pointer: returns *this for method chaining
    LibraryMember &setName(string name)
    {
        this->name = name; // 'this' distinguishes member from parameter
        return *this;
    }
    LibraryMember &setMemberID(int memberID)
    {
        this->memberID = memberID;
        return *this;
    }

    bool borrowResource(LibraryResource res)
    {
        if (borrowCount >= MAX_BORROWED)
        {
            cout << "  Error: Borrow limit (" << MAX_BORROWED << ") reached.\n";
            return false;
        }
        res.setIsAvailable(false);
        borrowedItems[borrowCount] = res;
        borrowCount++;
        return true;
    }

    bool returnResource(int resourceID)
    {
        for (int i = 0; i < borrowCount; i++)
        {
            if (borrowedItems[i].getResourceID() == resourceID)
            {
                for (int j = i; j < borrowCount - 1; j++)
                    borrowedItems[j] = borrowedItems[j + 1];
                borrowCount--;
                return true;
            }
        }
        cout << "  Error: Resource ID " << resourceID
             << " not found in your borrowed list.\n";
        return false;
    }

    void displayBorrowedItems() const
    {
        if (borrowCount == 0)
        {
            cout << "  No borrowed items.\n";
            return;
        }
        for (int i = 0; i < borrowCount; i++)
        {
            borrowedItems[i].displayDetails();
            cout << "  -------------------\n";
        }
    }

     // Loops through all borrowed items and sums up their individual late fees.
    // Calls calculateLateFee() on each LibraryResource object in the array.

    double calculateTotalLateFee(int daysLate) const
    {
        double total = 0;
        for (int i = 0; i < borrowCount; i++)
            total += borrowedItems[i].calculateLateFee(daysLate);
        return total;
    }

    bool hasBorrowed(int resourceID) const
    {
        for (int i = 0; i < borrowCount; i++)
            if (borrowedItems[i].getResourceID() == resourceID)
                return true;
        return false;
    }
};

// ============================================================
//  Library
// ============================================================
class Library
{
    friend void adminView(const Library &lib, const LibraryMember members[], int memberCount);

private:
    LibraryResource resources[MAX_RESOURCES];
    int resourceCount;

public:
    Library() : resourceCount(0) {}

    bool addResource(const LibraryResource &res)
    {
        if (resourceCount >= MAX_RESOURCES)
        {
            cout << "  Error: Library is full.\n";
            return false;
        }
        resources[resourceCount++] = res;
        return true;
    }

    int findResourceIndex(int id) const
    {
        for (int i = 0; i < resourceCount; i++)
            if (resources[i].getResourceID() == id)
                return i;
        return -1;
    }

        // Returns a pointer to the resource with the given ID, or nullptr if not found
    LibraryResource *getResource(int id)
    {
        int idx = findResourceIndex(id);
        return (idx == -1) ? nullptr : &resources[idx];
    }

    bool setAvailability(int id, bool avail)
    {
        int idx = findResourceIndex(id);
        if (idx == -1)
            return false;
        resources[idx].setIsAvailable(avail);
        return true;
    }

    void displayAllResources() const
    {
        if (resourceCount == 0)
        {
            cout << "  No resources in library.\n";
            return;
        }
        for (int i = 0; i < resourceCount; i++)
        {
            resources[i].displayDetails();
            cout << "  -------------------\n";
        }
    }
};

// ============================================================
//  Friend Function: adminView
// ============================================================
void adminView(const Library &lib, const LibraryMember members[], int memberCount)
{
    cout << "\n========== ADMIN VIEW ==========\n";

    cout << "\n--- All Library Resources ---\n";
    if (lib.resourceCount == 0)
        cout << "  (none)\n";
    else
        for (int i = 0; i < lib.resourceCount; i++)
            cout << "  ID: " << lib.resources[i].resourceID
                 << "  Title: " << lib.resources[i].title
                 << "  Avail: " << (lib.resources[i].isAvailable ? "Yes" : "No") << "\n";
    // Directly access members[i].memberID, .name, .borrowedItems, .borrowCount
    // — allowed because LibraryMember declared adminView as a friend
    cout << "\n--- All Registered Members ---\n";
    if (memberCount == 0)
        cout << "  (none)\n";
    else
        for (int i = 0; i < memberCount; i++)
        {
            cout << "  MemberID: " << members[i].memberID
                 << "  Name: " << members[i].name << "\n"
                 << "  Borrowed:\n";
            if (members[i].borrowCount == 0)
                cout << "    (none)\n";
            else
                for (int j = 0; j < members[i].borrowCount; j++)     // Accessing private fields of borrowedItems directly
                    cout << "    - [" << members[i].borrowedItems[j].resourceID
                         << "] " << members[i].borrowedItems[j].title << "\n";
        }
    cout << "================================\n";
}

int findMemberIndex(const LibraryMember members[], int count, int id)
{
    for (int i = 0; i < count; i++)
        if (members[i].getMemberID() == id)
            return i;
    return -1;
}
// ============================================================
//  main() — Menu-driven interface for the Library System
// ============================================================
int main() 
{
    Library library;
    LibraryMember members[MAX_MEMBERS];
    int memberCount = 0;
    int choice;

    cout << "===================================\n"
         << "   Library Management System\n"
         << "===================================\n";

    do
    {
        cout << "\n--- MAIN MENU ---\n"
             << "1. Add a new Resource\n"
             << "2. Register a new Member\n"
             << "3. Borrow a Resource\n"
             << "4. Return a Resource\n"
             << "5. Display all Resources\n"
             << "6. Display Member's Borrowed Items\n"
             << "7. Calculate Late Fee\n"
             << "8. Admin View\n"
             << "9. Exit\n"
             << "Enter choice: ";
        cin >> choice;
        cin.ignore();

        // ---- Option 1: Add a Resource ----
        if (choice == 1)
        {
            int type;
            cout << "Resource type (1=Book  2=Magazine  3=DVD): ";
            cin >> type;
            cin.ignore();

            // Validate type FIRST before asking anything else
            if (type != 1 && type != 2 && type != 3)
            {
                cout << "  Error: Invalid resource type. Please enter 1, 2, or 3.\n";
                continue;
            }

            int id;
            string title, author;
            cout << "Resource ID  : ";
            cin >> id;
            cin.ignore();
            if (library.findResourceIndex(id) != -1)
            {
                cout << "  Error: Resource ID already exists.\n";
                continue;
            }

            cout << "Title        : ";
            getline(cin, title);
            cout << "Author/Studio: ";
            getline(cin, author);

            if (type == 1)
            {
                string isbn;
                int pages;
                cout << "ISBN         : ";
                getline(cin, isbn);
                cout << "Page Count   : ";
                cin >> pages;
                cin.ignore();
                 // Book(...) creates a temporary Book object (derived from LibraryResource)
                // addResource() copies it into the library's resources[] array
                library.addResource(Book(id, title, author, isbn, pages));
                cout << "  Book added.\n";
            }
            else if (type == 2)
            {
                int issue;
                cout << "Issue Number : ";
                cin >> issue;
                cin.ignore();
                library.addResource(Magazine(id, title, author, issue));
                cout << "  Magazine added.\n";
            }
            else if (type == 3)
            {
                int dur;
                cout << "Duration(min): ";
                cin >> dur;
                cin.ignore();
                library.addResource(DVD(id, title, author, dur));
                cout << "  DVD added.\n";
            }
            else
                cout << "  Error: Invalid resource type.\n";
        }

        // ---- Option 2: Register a Member ----
        else if (choice == 2)
        {
            if (memberCount >= MAX_MEMBERS)
            {
                cout << "  Error: Member limit reached.\n";
                continue;
            }
            int mid;
            string mname;
            cout << "Member ID  : ";
            cin >> mid;
            cin.ignore();
            if (findMemberIndex(members, memberCount, mid) != -1)
            {
                cout << "  Error: Member ID already exists.\n";
                continue;
            }
            cout << "Member Name: ";
            getline(cin, mname);
            members[memberCount++] = LibraryMember(mid, mname);
            cout << "  Member registered.\n";
        }
           // ---- Option 3: Borrow a Resource ----
        else if (choice == 3)
        {
            int mid, rid;
            cout << "Member ID  : ";
            cin >> mid;
            cin.ignore();
            cout << "Resource ID: ";
            cin >> rid;
            cin.ignore();
            int mIdx = findMemberIndex(members, memberCount, mid);
            if (mIdx == -1)
            {
                cout << "  Error: Member not found.\n";
                continue;
            }
            LibraryResource *res = library.getResource(rid);
            if (!res)
            {
                cout << "  Error: Resource not found.\n";
                continue;
            }
            if (!res->getIsAvailable())
            {
                cout << "  Error: Resource is already borrowed.\n";
                continue;
            }
             // Mark unavailable in the library so no one else can borrow it,
            // then give a copy to the member's borrowedItems[] (composition)
            library.setAvailability(rid, false);
            members[mIdx].borrowResource(*res);
            // *res dereferences pointer to get object
            cout << "  Resource borrowed successfully.\n";
        }

          // ---- Option 4: Return a Resource ----
        else if (choice == 4)
        {
            int mid, rid;
            cout << "Member ID  : ";
            cin >> mid;
            cin.ignore();
            cout << "Resource ID: ";
            cin >> rid;
            cin.ignore();
            int mIdx = findMemberIndex(members, memberCount, mid);
            if (mIdx == -1)
            {
                cout << "  Error: Member not found.\n";
                continue;
            }

             // Make sure this member actually borrowed this resource
            if (!members[mIdx].hasBorrowed(rid))
            {
                cout << "  Error: Member has not borrowed resource " << rid << ".\n";
                continue;
            }
            members[mIdx].returnResource(rid);
            library.setAvailability(rid, true);
            cout << "  Resource returned successfully.\n";
        }

        // ---- Option 5: Display All Resources ----
        else if (choice == 5)
        {
            cout << "\n--- All Resources ---\n";
            library.displayAllResources();

        }
        // ---- Option 6: Display a Member's Borrowed Items ----
        else if (choice == 6)
        {
            int mid;
            cout << "Member ID: ";
            cin >> mid;
            cin.ignore();
            int mIdx = findMemberIndex(members, memberCount, mid);
            if (mIdx == -1)
            {
                cout << "  Error: Member not found.\n";
                continue;
            }
            cout << "\n--- Borrowed by " << members[mIdx].getName() << " ---\n";
            members[mIdx].displayBorrowedItems();
        }
        // ---- Option 7: Calculate Late Fee ----
        else if (choice == 7)
        {
            int mid, days;
            cout << "Member ID  : ";
            cin >> mid;
            cin.ignore();
            cout << "Days Late  : ";
            cin >> days;
            cin.ignore();
            int mIdx = findMemberIndex(members, memberCount, mid);
            if (mIdx == -1)
            {
                cout << "  Error: Member not found.\n";
                continue;
            }
            
            cout << "  Total Late Fee for " << members[mIdx].getName()
                 << ": Rs. " << members[mIdx].calculateTotalLateFee(days) << "\n";
        }
         // ---- Option 8: Admin View (Friend Function) ----
        else if (choice == 8)
        {
            // Calls the friend function — bypasses encapsulation to show
            // all private data from Library and LibraryMember directly
            adminView(library, members, memberCount);
        }
        else if (choice == 9)
        {
            cout << "  Goodbye!\n"; // Loop condition (choice != 9) becomes false — program ends
        }
        else
        {
            cout << "  Error: Invalid menu choice.\n";
        }

    } while (choice != 9);
    // keep looping until user selects Exit
    return 0;
}
