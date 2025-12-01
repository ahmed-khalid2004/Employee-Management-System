# Employee Management System

A desktop application built with Java Swing for managing employee records with full CRUD operations, featuring a MySQL database backend and an intuitive GUI interface.

## Project Overview

The Employee Management System is a comprehensive desktop application designed to streamline employee data management for small to medium-sized organizations. Built using Java Swing for the graphical user interface and MySQL for data persistence, this system provides a user-friendly platform for HR departments and administrators to efficiently handle employee information.

**Key Goals:**
- Simplify employee record management with an intuitive desktop interface
- Provide secure authentication for system access
- Enable quick CRUD (Create, Read, Update, Delete) operations on employee data
- Maintain structured employee information including personal details, education, designation, and salary
- Generate printable employee reports for documentation purposes

**Use Cases:**
- HR departments managing employee databases
- Small business employee record keeping
- Educational institutions for staff management
- Administrative offices requiring centralized employee data
- Organizations transitioning from paper-based to digital record systems

## Tech Stack

**Languages:**
- Java (assumed version: Java 8 or higher based on Swing usage)

**Frameworks & Libraries:**
- **Java Swing** - GUI framework for desktop interface
- **JDBC (Java Database Connectivity)** - Database connectivity layer
- **MySQL Connector/J** - MySQL JDBC driver (`com.mysql.cj.jdbc.Driver`)
- **JCalendar (Toedter)** - Date picker component (`com.toedter.calendar.JDateChooser`)
- **rs2xml.jar** - ResultSet to JTable conversion (`net.proteanit.sql.DbUtils`)

**Database:**
- **MySQL** - Relational database management system

**Development Tools:**
- IDE: NetBeans, Eclipse, or IntelliJ IDEA (inferred)
- Java Development Kit (JDK) 8+

**Runtime:**
- Java Runtime Environment (JRE) 8 or higher

## Architecture

**High-Level Design:**
The application follows a simple three-tier architecture pattern:

```
Presentation Layer (Java Swing GUI)
         ↓
Business Logic Layer (Java Classes)
         ↓
Data Access Layer (JDBC + Conn.java)
         ↓
Database Layer (MySQL)
```

**Major Components:**

1. **Splash Screen (Splash.java)**
   - Application entry point with animated welcome screen
   - Transitions to login interface

2. **Authentication Module (Login.java)**
   - User credential validation against database
   - Security gateway to main application

3. **Home Dashboard (Home.java)**
   - Central navigation hub
   - Provides access to all major functions (Add, View, Update, Remove)

4. **Employee Management Modules**
   - **AddEmployee.java** - Employee registration with auto-generated ID
   - **ViewEmployee.java** - Employee data display with search and print
   - **UpdateEmployee.java** - Employee information modification
   - **RemoveEmployee.java** - Employee record deletion

5. **Database Connectivity (Conn.java)**
   - Singleton-pattern database connection handler
   - Manages MySQL connection and statement execution

**Data Flow:**
1. User launches application → Splash screen displays
2. User clicks continue → Login screen appears
3. User enters credentials → Validated against `login` table in database
4. Successful login → Home dashboard loads with background image
5. User selects operation (Add/View/Update/Remove)
6. Appropriate module opens with form/table interface
7. User performs action → SQL query executed via Conn.java
8. Database updated → Confirmation message displayed
9. User returns to Home dashboard

**Database Schema (Inferred):**
- **login** table: `username`, `password`
- **employee** table: `name`, `fname`, `dob`, `salary`, `address`, `phone`, `email`, `education`, `designation`, `National_ID`, `empId`

## Features

**Core Features:**
- ✅ User authentication with login system
- ✅ Add new employee records with auto-generated unique employee ID
- ✅ View all employees in tabular format
- ✅ Search employees by employee ID
- ✅ Update employee information (editable fields: father's name, salary, address, phone, email, education, designation, national ID)
- ✅ Delete employee records with confirmation
- ✅ Print employee reports directly from the application
- ✅ Date picker integration for date of birth selection
- ✅ Education level dropdown with predefined options (BBA, BCA, BA, BSC, B.COM, BTech, MBA, MCA, MA, MTech, MSC, PHD)
- ✅ Real-time employee details preview when selecting for deletion

**Additional Features:**
- Animated splash screen with blinking heading text
- Custom styled GUI with black buttons and white text
- Image backgrounds for enhanced visual appeal
- Dropdown selection for efficient employee ID lookup
- Form validation and error handling with try-catch blocks
- Immediate database synchronization for all operations

## Setup & How to Run

**Prerequisites:**
- Java Development Kit (JDK) 8 or higher ([Download here](https://www.oracle.com/java/technologies/downloads/))
- MySQL Server 5.7+ or 8.0+ ([Download here](https://dev.mysql.com/downloads/mysql/))
- MySQL Workbench (optional, for database management)
- Required JAR files:
  - MySQL Connector/J (`mysql-connector-java-8.x.x.jar`)
  - JCalendar (`jcalendar-1.4.jar`)
  - rs2xml (`rs2xml.jar`)

**Installation Steps:**

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd Employee-Management-System
   ```

2. **Set up MySQL database:**
   ```bash
   # Login to MySQL
   mysql -u root -p
   ```

   ```sql
   -- Create database
   CREATE DATABASE employeemanagementsystem;
   
   -- Use the database
   USE employeemanagementsystem;
   
   -- Create login table
   CREATE TABLE login (
       username VARCHAR(50) PRIMARY KEY,
       password VARCHAR(50) NOT NULL
   );
   
   -- Insert default admin user
   INSERT INTO login VALUES ('admin', 'admin123');
   
   -- Create employee table
   CREATE TABLE employee (
       name VARCHAR(100),
       fname VARCHAR(100),
       dob VARCHAR(20),
       salary VARCHAR(20),
       address VARCHAR(200),
       phone VARCHAR(20),
       email VARCHAR(100),
       education VARCHAR(50),
       designation VARCHAR(100),
       National_ID VARCHAR(50),
       empId VARCHAR(20) PRIMARY KEY
   );
   ```

3. **Configure database connection:**
   
   Edit `Conn.java` and update the database credentials:
   ```java
   // Line 13 in Conn.java
   c = DriverManager.getConnection("jdbc:mysql:///employeemanagementsystem", "YOUR_MYSQL_USERNAME", "YOUR_MYSQL_PASSWORD");
   ```

4. **Add required JAR files to project:**
   
   **For command-line compilation:**
   ```bash
   # Create lib directory
   mkdir lib
   
   # Download and place the following JAR files in lib/:
   # - mysql-connector-java-8.0.x.jar
   # - jcalendar-1.4.jar
   # - rs2xml.jar
   ```

   **For IDE (NetBeans/Eclipse/IntelliJ):**
   - Right-click project → Properties/Build Path
   - Add External JARs → Select all three JAR files
   - Apply changes

5. **Create icons directory and add images:**
   ```bash
   # Create icons folder in src directory
   mkdir -p src/icons
   
   # Add the following image files:
   # - front.jpg (splash screen background)
   # - second.jpg (login screen image)
   # - home.jpg (home dashboard background)
   # - delete.png (remove employee screen image)
   ```

6. **Compile the project:**
   
   **Using command line:**
   ```bash
   javac -cp ".:lib/*" -d bin src/employee/management/system/*.java
   ```

   **Using IDE:**
   - Click "Build Project" or press Ctrl+B

7. **Run the application:**
   
   **Using command line:**
   ```bash
   java -cp "bin:lib/*" employee.management.system.Splash
   ```

   **Using IDE:**
   - Right-click `Splash.java` → Run File
   - Or set `Splash.java` as main class and click Run

**Default Login Credentials:**
- Username: `admin`
- Password: `admin123`

**Common Commands:**
```bash
# Compile all Java files
javac -cp ".:lib/*" src/employee/management/system/*.java -d bin

# Run the application
java -cp "bin:lib/*" employee.management.system.Splash

# Run specific module (for testing)
java -cp "bin:lib/*" employee.management.system.Login
java -cp "bin:lib/*" employee.management.system.Home

# Clean compiled files
rm -rf bin/*
```

## Testing

**Manual Testing:**

This project does not include automated tests. All testing should be performed manually through the GUI:

1. **Authentication Testing:**
   - Test valid login credentials
   - Test invalid username/password
   - Test empty field validation

2. **Add Employee Testing:**
   - Add employee with all fields filled
   - Verify auto-generated employee ID is unique
   - Test date picker functionality
   - Verify database insertion

3. **View Employee Testing:**
   - View all employees in table
   - Search by specific employee ID
   - Test print functionality
   - Verify table data accuracy

4. **Update Employee Testing:**
   - Select employee to update
   - Modify editable fields
   - Verify non-editable fields (name, DOB, empId) are locked
   - Confirm database update

5. **Delete Employee Testing:**
   - Select employee from dropdown
   - Verify employee details display correctly
   - Test deletion with confirmation
   - Verify removal from database

**Test Coverage:**
- No automated test coverage available
- Recommended: Add JUnit tests for business logic
- Recommended: Add integration tests for database operations

**Testing Checklist:**
```
[ ] Login with valid credentials works
[ ] Login with invalid credentials shows error
[ ] Employee ID auto-generation is unique
[ ] All form fields save correctly to database
[ ] Date picker calendar displays and saves dates
[ ] View displays all employees
[ ] Search filters employee by ID
[ ] Print generates correct output
[ ] Update saves changes to database
[ ] Delete removes employee from database
[ ] Navigation between screens works properly
[ ] All images load correctly
```

## Folder Structure

```
Employee-Management-System/
├── src/
│   ├── employee/
│   │   └── management/
│   │       └── system/
│   │           ├── Splash.java           # Entry point with animated splash screen
│   │           ├── Login.java            # User authentication module
│   │           ├── Home.java             # Main dashboard navigation
│   │           ├── AddEmployee.java      # Employee registration form
│   │           ├── ViewEmployee.java     # Employee listing and search
│   │           ├── UpdateEmployee.java   # Employee information update
│   │           ├── RemoveEmployee.java   # Employee deletion module
│   │           └── Conn.java             # Database connection handler
│   └── icons/                            # Image resources directory
│       ├── front.jpg                     # Splash screen background
│       ├── second.jpg                    # Login screen image
│       ├── home.jpg                      # Home dashboard background
│       └── delete.png                    # Remove employee image
├── lib/                                  # External JAR dependencies
│   ├── mysql-connector-java-8.x.x.jar   # MySQL JDBC driver
│   ├── jcalendar-1.4.jar                # Date picker component
│   └── rs2xml.jar                        # ResultSet to JTable utility
├── bin/                                  # Compiled .class files (generated)
└── README.md                             # Project documentation
```

**Key Files Explained:**
- `Splash.java` - Application entry point with animated welcome screen and "CLICK HERE TO CONTINUE" button
- `Login.java` - Handles user authentication by querying the `login` table
- `Conn.java` - Manages database connection setup and statement creation (singleton pattern)
- `Home.java` - Central navigation hub with buttons for Add, View, Update, and Remove operations
- `AddEmployee.java` - Form for adding new employees with random ID generation
- `ViewEmployee.java` - Displays all employees in JTable with search, print, and update capabilities
- `UpdateEmployee.java` - Pre-filled form for modifying existing employee data
- `RemoveEmployee.java` - Interface for selecting and deleting employees with preview

## Configuration & Secrets

**Database Configuration:**

The database connection is configured in `Conn.java`. Update the following parameters:

```java
// Conn.java - Line 13
c = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/employeemanagementsystem",  // Database URL
    "YOUR_MYSQL_USERNAME",                                    // Username
    "YOUR_MYSQL_PASSWORD"                                     // Password
);
```

**Configuration Parameters:**

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| Database Host | MySQL server address | `localhost` or `127.0.0.1` |
| Database Port | MySQL server port | `3306` (default) |
| Database Name | Name of the database | `employeemanagementsystem` |
| Username | MySQL user | `root` or custom user |
| Password | MySQL password | `YOUR_PASSWORD_HERE` |

**Security Notes:**
- ⚠️ **Current Implementation**: Database credentials are hardcoded in `Conn.java`
- ⚠️ **SQL Injection Risk**: The application uses string concatenation for SQL queries, making it vulnerable to SQL injection attacks
- ⚠️ **Plain Text Passwords**: User passwords in the `login` table are stored in plain text

**Recommended Configuration (For Production):**

Create a `config.properties` file:
```properties
# Database Configuration
db.host=localhost
db.port=3306
db.name=employeemanagementsystem
db.username=YOUR_DB_USERNAME
db.password=YOUR_DB_PASSWORD

# Application Settings
app.title=Employee Management System
app.version=1.0
```

**Environment Variables Alternative:**
```bash
# Set environment variables (Linux/Mac)
export DB_HOST=localhost
export DB_PORT=3306
export DB_NAME=employeemanagementsystem
export DB_USER=your_username
export DB_PASS=your_password

# Set environment variables (Windows)
set DB_HOST=localhost
set DB_PORT=3306
set DB_NAME=employeemanagementsystem
set DB_USER=your_username
set DB_PASS=your_password
```

**Demo Workflow:**
1. Launch application → Splash screen with blinking heading
2. Click "CLICK HERE TO CONTINUE" → Login screen
3. Enter credentials (admin/admin123) → Click LOGIN
4. Home dashboard displays → Click "Add Employee"
5. Fill employee form → Click "Add Details"
6. Success message → Return to Home
7. Click "View Employees" → See employee table
8. Select employee ID → Click "Update"
9. Modify details → Click "Update Details"
10. Navigate to "Remove Employee" → Select and delete

## Future Improvements

**High Priority:**
- [ ] **Security Enhancements**
  - Implement PreparedStatement to prevent SQL injection
  - Add password hashing (BCrypt, SHA-256) for secure storage
  - Create role-based access control (Admin, HR, Viewer)
  - Add session management and timeout features
- [ ] **Data Validation**
  - Add email format validation
  - Implement phone number format checking
  - Add salary range validation
  - Prevent duplicate national ID entries
- [ ] **Database Design**
  - Create proper foreign key relationships
  - Add timestamps (created_at, updated_at)
  - Implement soft delete instead of hard delete
  - Add audit trail for all modifications

**Medium Priority:**
- [ ] Add employee photo upload functionality
- [ ] Implement advanced search with multiple filters (name, designation, department)
- [ ] Create department management module
- [ ] Add salary history tracking
- [ ] Generate detailed reports (PDF, Excel export)
- [ ] Implement data backup and restore features
- [ ] Add employee performance tracking
- [ ] Create attendance management module
- [ ] Implement leave management system
- [ ] Add dashboard with statistics and charts

**Nice to Have:**
- [ ] Migrate to modern UI framework (JavaFX)
- [ ] Add dark mode theme option
- [ ] Implement notification system
- [ ] Create RESTful API for web/mobile access
- [ ] Add email notifications for employee updates
- [ ] Implement document management (contracts, certificates)
- [ ] Add bulk employee import from CSV/Excel
- [ ] Create mobile application version
- [ ] Add multi-language support
- [ ] Implement automated backups
- [ ] Add encryption for sensitive data
- [ ] Create user activity logs

**Technical Debt:**
- [ ] Add comprehensive unit tests (JUnit)
- [ ] Implement logging framework (Log4j, SLF4J)
- [ ] Add exception handling framework
- [ ] Refactor code to follow MVC pattern strictly
- [ ] Add configuration file support
- [ ] Implement connection pooling for better performance
- [ ] Add CI/CD pipeline setup

## Contribution Guidelines

We welcome contributions to improve the Employee Management System! Here's how you can help:

**How to Contribute:**

1. **Fork the repository**
   ```bash
   git clone <your-fork-url>
   cd Employee-Management-System
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b bugfix/issue-description
   ```

3. **Make your changes**
   - Follow Java naming conventions (camelCase for methods, PascalCase for classes)
   - Add comments for complex logic
   - Ensure code is properly formatted
   - Test thoroughly before committing

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "Add: Brief description of changes"
   # Use prefixes: Add, Fix, Update, Remove, Refactor
   ```

5. **Push and create a Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```

**PR Standards:**
- Provide clear description of changes and motivation
- Reference related issues (e.g., "Fixes #123")
- Include screenshots for UI changes
- Ensure code compiles without errors
- Test all affected functionality
- Update documentation if needed

**Code Style Guidelines:**
- Use 4 spaces for indentation
- Follow standard Java naming conventions
- Add JavaDoc comments for public methods
- Keep methods focused and under 50 lines
- Use meaningful variable names
- Avoid magic numbers - use constants

**Contribution Areas:**
- Bug fixes and error handling improvements
- Security enhancements (SQL injection prevention, password hashing)
- UI/UX improvements
- New features (reports, analytics, etc.)
- Documentation improvements
- Test coverage additions
- Performance optimizations

**Reporting Issues:**
- Use GitHub Issues to report bugs
- Include detailed steps to reproduce
- Provide screenshots if applicable
- Mention your Java version and OS

## License

**MIT License** - This project is licensed under the MIT License, making it free to use, modify, and distribute. This permissive license is ideal for educational projects and allows organizations to adapt the system to their specific needs while limiting liability.


## Social Links / Author Contact

**Project Maintainer:** [Ahmed Khaled]

**Contact Information:**
- GitHub: [@Ahmed-Khalid2004](https://github.com/ahmed-khalid2004)
- LinkedIn: [Ahmed Khaled](https://linkedin.com/in/ahmed-khalid-5b6349259)
- Email: engahmedkhalid3s@gmail.com
- Project Issues: [GitHub Issues](https://github.com/ahmed-khalid2004/Employee-Management-System/issues)

**Contributing:**
Feel free to reach out for questions, suggestions, or collaboration opportunities!

---

## Notes / Known Issues

**Security Vulnerabilities:**
- ⚠️ **SQL Injection**: All database queries use string concatenation, making the application vulnerable to SQL injection attacks
- ⚠️ **Plain Text Passwords**: User passwords are stored without hashing in the database
- ⚠️ **Hardcoded Credentials**: Database credentials are hardcoded in `Conn.java`

**Known Bugs:**
- Splash screen animation runs infinitely in while(true) loop (blocks thread)
- No validation for empty fields before database operations
- No duplicate employee ID checking (relies on random number generation)
- Missing proper connection closing (potential memory leaks)
- No error handling for missing image files

**Recommendations:**
- Replace string concatenation with PreparedStatement
- Implement password hashing (BCrypt)
- Move database credentials to configuration file
- Add comprehensive input validation
- Implement proper exception handling
- Use connection pooling for better resource management

---

**What I looked at:** Analyzed all Java source files (Splash.java, Login.java, Home.java, AddEmployee.java, ViewEmployee.java, UpdateEmployee.java, RemoveEmployee.java, Conn.java) to understand the application flow, database schema, dependencies (JCalendar, rs2xml, MySQL Connector), GUI structure using Java Swing, and the overall CRUD operations implementation for employee management.
