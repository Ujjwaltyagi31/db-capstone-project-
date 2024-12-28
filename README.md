# Little Lemon Database Capstone Project

This README provides detailed documentation for the Little Lemon database project. It includes an overview of the database model and schema design and essential information for understanding and managing the database.

---

## **Project Overview**
The Little Lemon Database is designed to manage a restaurant's booking system. It organizes and maintains data related to customer bookings, staff assignments, and table management, ensuring seamless operations and easy information retrieval.

---

## **Database Schema**
The database consists of the following tables:

### 1. **Bookings Table**
| Field         | Type   | Null | Key | Default | Extra          |
|---------------|--------|------|-----|---------|----------------|
| BookingID     | INT    | NO   | PRI | NULL    | AUTO_INCREMENT |
| BookingDate   | DATE   | NO   |     | NULL    |                |
| BookingTime   | TIME   | NO   |     | NULL    |                |
| CustomerID    | INT    | NO   | MUL | NULL    |                |
| TableNo       | INT    | NO   |     | NULL    |                |
| StaffID       | INT    | YES  | MUL | NULL    |                |

#### Description:
- **BookingID**: A unique identifier for each booking (Primary Key).
- **BookingDate**: The date of the booking.
- **BookingTime**: The time of the booking.
- **CustomerID**: Foreign key referencing the `CustomerDetails` table.
- **TableNo**: The table number assigned for the booking.
- **StaffID**: Foreign key referencing the `StaffDetails` table (nullable).

---

### 2. **CustomerDetails Table**
| Field        | Type   | Null | Key | Default | Extra |
|--------------|--------|------|-----|---------|-------|
| CustomerID   | INT    | NO   | PRI | NULL    |       |
| CustomerName | VARCHAR(100) | NO |     | NULL    |       |
| ContactInfo  | VARCHAR(50)  | YES|     | NULL    |       |

#### Description:
- **CustomerID**: A unique identifier for each customer (Primary Key).
- **CustomerName**: The name of the customer.
- **ContactInfo**: Contact information such as phone or email.

---

### 3. **StaffDetails Table**
| Field       | Type   | Null | Key | Default | Extra |
|-------------|--------|------|-----|---------|-------|
| StaffID     | INT    | NO   | PRI | NULL    |       |
| StaffName   | VARCHAR(100) | NO |     | NULL    |       |
| Role        | VARCHAR(50)  | NO |     | NULL    |       |

#### Description:
- **StaffID**: A unique identifier for each staff member (Primary Key).
- **StaffName**: The name of the staff member.
- **Role**: The role of the staff member (e.g., Manager, Waiter).

---

### 4. **TableDetails Table**
| Field       | Type   | Null | Key | Default | Extra |
|-------------|--------|------|-----|---------|-------|
| TableNo     | INT    | NO   | PRI | NULL    |       |
| Capacity    | INT    | NO   |     | NULL    |       |
| Location    | VARCHAR(50) | YES | NULL    |       |

#### Description:
- **TableNo**: A unique identifier for each table (Primary Key).
- **Capacity**: Number of seats at the table.
- **Location**: Location of the table within the restaurant (e.g., Indoor, Outdoor).

---

## **Relationships Between Tables**
1. **CustomerDetails** and **Bookings**:
   - `CustomerID` in `Bookings` references `CustomerID` in `CustomerDetails` (Foreign Key).
2. **StaffDetails** and **Bookings**:
   - `StaffID` in `Bookings` references `StaffID` in `StaffDetails` (Foreign Key).
3. **TableDetails** and **Bookings**:
   - `TableNo` in `Bookings` references `TableNo` in `TableDetails` (Foreign Key).

---

## **Sample Data**

### **CustomerDetails**
| CustomerID | CustomerName | ContactInfo     |
|------------|--------------|-----------------|
| 101        | John Doe     | 123-456-7890    |
| 102        | Jane Smith   | 987-654-3210    |

### **StaffDetails**
| StaffID | StaffName   | Role     |
|---------|-------------|----------|
| 201     | Alice Green | Manager  |
| 202     | Bob Brown   | Waiter   |

### **TableDetails**
| TableNo | Capacity | Location |
|---------|----------|----------|
| 1       | 4        | Indoor   |
| 2       | 6        | Outdoor  |

### **Bookings**
| BookingID | BookingDate | BookingTime | CustomerID | TableNo | StaffID |
|-----------|-------------|-------------|------------|---------|---------|
| 1         | 2024-01-01  | 18:30:00    | 101        | 1       | 201     |
| 2         | 2024-01-02  | 19:00:00    | 102        | 2       | 202     |

---

## **Essential SQL Queries**

### **1. Create the Tables**
```SQL
CREATE TABLE CustomerDetails (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL,
    ContactInfo VARCHAR(50)
);

CREATE TABLE StaffDetails (
    StaffID INT PRIMARY KEY,
    StaffName VARCHAR(100) NOT NULL,
    Role VARCHAR(50) NOT NULL
);

CREATE TABLE TableDetails (
    TableNo INT PRIMARY KEY,
    Capacity INT NOT NULL,
    Location VARCHAR(50)
);

CREATE TABLE Bookings (
    BookingID INT AUTO_INCREMENT PRIMARY KEY,
    BookingDate DATE NOT NULL,
    BookingTime TIME NOT NULL,
    CustomerID INT NOT NULL,
    TableNo INT NOT NULL,
    StaffID INT,
    FOREIGN KEY (CustomerID) REFERENCES CustomerDetails(CustomerID) ON DELETE CASCADE,
    FOREIGN KEY (TableNo) REFERENCES TableDetails(TableNo),
    FOREIGN KEY (StaffID) REFERENCES StaffDetails(StaffID)
);
```

### **2. Insert Sample Data**
Refer to the sample data section for sample `INSERT` queries.

### **3. Retrieve All Bookings**
```SQL
SELECT b.BookingID, b.BookingDate, b.BookingTime, c.CustomerName, t.TableNo, s.StaffName
FROM Bookings b
JOIN CustomerDetails c ON b.CustomerID = c.CustomerID
JOIN TableDetails t ON b.TableNo = t.TableNo
LEFT JOIN StaffDetails s ON b.StaffID = s.StaffID;
```

---

## **Usage Instructions**
1. **Database Setup**:
   - Execute the `CREATE TABLE` queries to set up the schema.
   - Populate tables with sample data or real data.

2. **Foreign Key Considerations**:
   - Ensure foreign key constraints are maintained when inserting or deleting data.

3. **Common Tasks**:
   - Use the provided SQL queries to manage and query the database.

---

## **Acknowledgments**
This database project was developed as part of the Little Lemon Capstone Project to demonstrate SQL proficiency and relational database design skills.


