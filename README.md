# Student Management System

> A console-based Student Management System built in C with MySQL database support for the CS102.3 Programming in C group assignment.

![Language](https://img.shields.io/badge/Language-C-blue)
![Database](https://img.shields.io/badge/Database-MySQL-orange)
![IDE](https://img.shields.io/badge/IDE-Code::Blocks-green)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey)

## Quick Navigation

- [Project Snapshot](#project-snapshot)
- [What This System Does](#what-this-system-does)
- [User Roles](#user-roles)
- [Project Structure](#project-structure)
- [Installation Checklist](#installation-checklist)
- [First-Time Setup](#first-time-setup)
- [How to Run](#how-to-run)
- [Important Notes](#important-notes)
- [Contribution Note](#contribution-note)

## Project Snapshot

| Item | Details |
| --- | --- |
| Module | CS102.3 Programming in C |
| Assignment | C Language Group Project |
| Batch | 23.2 Batch - Group C |
| Group | Group 32 |
| Project Type | Console application |
| Main Language | C |
| Database | MySQL |
| Main Responsibility | Development and group coordination handled by the repository owner |

## What This System Does

This project is a simple academic management system for handling student records, course details, marks, and attendance. It runs in the Windows console and connects to a MySQL database.

The system starts with a login screen. If there are no users in the database, it guides the user through creating the first administrator account.

### Main Features

| Feature | Description |
| --- | --- |
| Login | Users log in using generated numeric IDs and passwords |
| First Admin Setup | The first user becomes the administrator |
| User Management | Create, modify, delete, and view users |
| Student Management | Add, update, delete, and view student records |
| Course Management | Create, modify, delete, and list courses |
| Marks Management | Add, update, delete, and view marksheets |
| Grade Generation | Grades are generated based on entered marks |
| Attendance | Mark current-day or previous-day attendance |
| Student View | Students can view marks, grades, attendance, and subject references |

## User Roles

### Super User / Administrator

The administrator has the highest access level.

| Can Do | Examples |
| --- | --- |
| Manage users | Create academic users, students, and other administrators |
| Manage courses | Add, modify, delete, and view course details |
| Manage student records | Create, update, remove, and view students |
| Manage passwords | Update user passwords after confirmation |

### Academic User

Academic users handle student academic records.

| Can Do | Examples |
| --- | --- |
| View students | Search and view student information |
| Manage marks | Add, modify, and delete marks |
| Manage attendance | Mark attendance and remove incorrect attendance records |

### Student

Students have view-only access to their own academic details.

| Can View | Examples |
| --- | --- |
| Personal details | Name, NIC, date of birth, contact details |
| Marks and grades | Subject-wise marks and generated grades |
| Attendance | Attendance percentage and attendance dates |
| Subject references | Course code and course name list |

## Technology Stack

| Technology | Purpose |
| --- | --- |
| C | Main application development |
| GCC | Compilation |
| Code::Blocks | Project setup and build environment |
| MySQL Server | Database storage |
| MySQL Workbench | Database model restoration and forward engineering |
| MySQL C API | C application to database connection |

## Project Structure

```text
.
|-- main.c
|-- New stsd.cbp
|-- README.txt
|-- README.md
|-- headers/
|   |-- datcmd.h
|   |-- datr.h
|   |-- dbm.h
|   |-- genm.h
|   |-- logio.h
|   |-- msgs.h
|   |-- uicmd.h
|   |-- uimenu.h
|   `-- uiview.h
|-- database model/
|   |-- stsd.mwb
|   `-- stsd.mwb.bak
|-- txt/
|   `-- server.txt
|-- lib/
|   `-- libmysql.dll
|-- bin/
|   |-- Debug/
|   `-- Release/
|-- obj/
`-- Doc/
```

<details>
<summary><strong>Click to view important file descriptions</strong></summary>

| File | Purpose |
| --- | --- |
| `main.c` | Application entry point. Starts the login interface. |
| `headers/dbm.h` | Handles MySQL connection and query execution. |
| `headers/datcmd.h` | Contains create, update, and delete operations. |
| `headers/datr.h` | Contains data reading helper functions. |
| `headers/genm.h` | Contains helper functions for dates, IDs, passwords, colors, and navigation. |
| `headers/uimenu.h` | Contains role-based menu navigation. |
| `headers/uicmd.h` | Contains console UI commands for record operations. |
| `headers/uiview.h` | Contains display functions for users, students, marks, courses, and attendance. |
| `database model/stsd.mwb` | MySQL Workbench database model. |
| `txt/server.txt` | Stores the MySQL server IP address. |

</details>

## Installation Checklist

Use this checklist before running the application.

- [ ] Install MySQL Server.
- [ ] Install MySQL Workbench.
- [ ] Create a MySQL user named `stsd`.
- [ ] Set the MySQL user password to `Stsd@123`.
- [ ] Give the user required database permissions.
- [ ] Open `database model/stsd.mwb` in MySQL Workbench.
- [ ] Forward engineer the database model.
- [ ] Update `txt/server.txt` with the MySQL server IP address.
- [ ] Copy `server.txt` to `C:\server.txt`.
- [ ] Build or run the executable.

## Database Setup

Create the MySQL user with these credentials:

```text
Username: stsd
Password: Stsd@123
Database: stsd
```

Then restore the database using:

```text
database model/stsd.mwb
```

The server address is loaded from:

```text
C:\server.txt
```

Example `server.txt` content:

```text
127.0.0.1
```

<details>
<summary><strong>Why does server.txt need to be copied to C:\?</strong></summary>

The database connection function in `headers/dbm.h` reads the server IP address from this fixed path:

```c
FILE *fptr = fopen("C:\\server.txt","r");
```

Because of this, the program expects the file to exist at:

```text
C:\server.txt
```

</details>

## First-Time Setup

When the application runs for the first time:

1. It checks whether users already exist in the database.
2. If no users exist, it starts first-user creation.
3. The first created user becomes the administrator.
4. Enter the requested name, telephone number, email, and password.
5. If the program asks for a super user password during initial setup, keep it blank.

## How to Run

### Option 1: Run Existing Executable

Release build:

```text
bin\Release\New stsd.exe
```

Debug build:

```text
bin\Debug\New stsd.exe
```

### Option 2: Build With Code::Blocks

1. Open the project file:

```text
New stsd.cbp
```

2. Select either `Debug` or `Release`.
3. Build the project.
4. Run the generated executable.

## Login and ID Format

The system displays user IDs with prefixes:

| Prefix | User Type |
| --- | --- |
| `SU` | Super User / Administrator |
| `U` | Academic User |
| `ST` | Student |

Example displayed ID:

```text
ST12345
```

When logging in or entering an ID, use only the numeric part:

```text
12345
```

Keep generated IDs safely. The application displays new IDs only once.

## Application Flow

```text
Start Application
       |
       v
Check Existing Users
       |
       +-- No Users --> Create First Admin
       |
       +-- Users Exist --> Login
                            |
                            +-- Super User --> Manage Users / Courses
                            |
                            +-- Academic User --> Manage Students / Marks / Attendance
                            |
                            +-- Student --> View Marks / Attendance / Subjects
```

## Important Notes

- This is an academic/test version of the application.
- The project is mainly designed for Windows console execution.
- MySQL must be running before the application starts.
- `C:\server.txt` must exist before database connection.
- User input uses simple console input, so spaces in names or addresses may not work correctly.
- Generated user IDs should be written down immediately.

<details>
<summary><strong>Known Limitations</strong></summary>

- Some validation and error handling are limited.
- The database configuration is hardcoded except for the server IP address.
- Password handling is basic and suitable only for an academic project.
- Several functions are implemented inside header files, which works for this project but is not the usual structure for larger C projects.
- The program depends on Windows console commands such as `cls`, `pause`, and `color`.

</details>

## Original README Reference

The original `README.txt` included the installation instructions, first-run setup, and user ID notes. This `README.md` expands those instructions and adds a clearer project overview based on the source code.

## Contribution Note

The development work and group coordination for this project were handled by the repository owner. This included implementing the C application logic, organizing project files, coordinating group progress, and preparing the project for submission.
