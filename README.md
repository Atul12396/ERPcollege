# 🎓 College ERP Management System

A comprehensive **College Enterprise Resource Planning (ERP) Management System** developed using **Django** to digitize and centralize academic, administrative, student, faculty, finance, hostel, transportation, and institutional operations.

The system provides a structured platform for managing students, teachers, departments, courses, branches, semesters, subjects, attendance, examinations, fees, scholarships, hostels, transportation, certificates, announcements, and staff information.

---

## 📌 Overview

The College ERP is designed to provide a centralized management system for educational institutions.

Instead of maintaining academic and administrative information across separate systems or manual records, the ERP connects different college operations through a common database and role-based application.

The system maintains relationships between:

**School → Department → Program/Course → Branch → Semester → Subject → Student/Teacher**

The Django data models implement these academic relationships directly.

---

## ✨ Key Features

### 👨‍🎓 Student Management

The system maintains comprehensive student information including:

* Student profile
* Student ID
* Roll number
* Contact information
* Address
* Profile picture
* School
* Course/Program
* Branch
* Semester
* Subjects
* Fee structure
* Payment status
* Hostel allocation
* Transport information
* Scholarships
* Student certificates

The `Student` model connects academic, financial, hostel, transportation, and subject information in one student record.

---

### 👨‍🏫 Faculty & Teacher Management

The ERP provides faculty management functionality including:

* Teacher profiles
* Designation
* School
* Department
* Course/Program
* Branch
* Semester
* Subject assignment
* Contact information
* Address
* Assignment status
* Leave information

Teachers can also have different leave categories such as casual, medical, official-duty, compass, and special leave.

---

### 🏫 Academic Management

The system supports hierarchical academic organization:

* Schools
* Departments
* Programs/Courses
* Branches
* Semesters
* Subjects

Courses are associated with departments, branches are associated with departments and courses, and semesters are associated with courses and branches.

---

### 📚 Subject Management

Subjects can be associated with:

* Courses
* Teachers
* Semesters
* Multiple branches
* Subject IDs
* Total number of classes

The system also supports many-to-many relationships between students, teachers, branches, and subjects.

---

### 📝 Attendance Management

The ERP provides attendance management through:

* Attendance records
* Subject-wise attendance
* Date-wise attendance
* Student attendance reports
* Attendance submission tracking
* Teacher/user submission information

Attendance is implemented using an `Attendance` model and an intermediate `AttendanceReport` model connecting students with attendance records.

---

### 🗓️ Timetable Management

The timetable module stores:

* Course
* Branch
* Semester
* Subject
* Day
* Start time
* End time
* Venue

This allows academic schedules to be organized around specific courses, branches, semesters, and subjects.

---

### 📊 Examination & Marks Management

The system provides a marks management structure containing:

* Student ID
* Roll number
* Student name
* Subject
* Semester
* Branch
* Examination type
* Marks obtained

This provides a centralized structure for storing academic examination results.

---

## 💰 Fee Management

The ERP contains a structured financial management system.

### Fee Structure

Fee structures can include:

* Registration fees
* Academic fees
* Hostel fees
* Transport fees
* Miscellaneous fees
* Fines
* Scholarships/discounts

The student fee system calculates total fees, paid amounts, and outstanding amounts.

### Payment Management

Payments maintain:

* Student
* Amount
* Payment method
* Transaction ID
* Payment status
* Payment date

Supported payment methods include:

* Online
* Cash
* Bank Transfer

Payment statuses include:

* Pending
* Completed
* Failed

---

## 🎓 Scholarship Management

The ERP supports scholarship records containing:

* Student
* Scholarship name
* Discount amount
* Granting authority
* Date granted

## Scholarship discounts are incorporated into the student's total fee calculation.

## 🏠 Hostel Management

The hostel module supports:

* Hostel creation
* Hostel capacity
* Floor management
* Room numbers
* AC / Non-AC rooms
* Room sharing capacity
* Current occupancy
* Room availability
* Hostel fee management
* Student-room allocation

## The system calculates room occupancy and remaining hostel capacity dynamically.

## 🚌 Transport Management

The transportation module maintains:

* Transport routes
* Bus numbers
* Transport fee structures
* Student transport associations

---

## 📢 Announcement Management

The announcement module allows institutional announcements to contain:

* Title
* Content
* Attached files
* Posted by
* Posting date

This provides a centralized mechanism for publishing college announcements.

---

## 🧑‍💼 Staff Management

The system also supports non-teaching staff records including:

* Staff profile
* Role
* Department
* Contact information
* Address
* Profile avatar
* Salary

Examples of roles can include administrative or accounting staff.

---

## 📄 Student Certificate Management

Student certificates can be stored and associated with individual students.

The certificate module contains:

* Student
* Certificate type
* Certificate file

---

## 👥 User & Role Management

The application uses Django's authentication system with a customized user model.

The `CustomUser` model extends Django's `AbstractUser` and adds:

* Role
* Roll number
* Department
* Course

The system identifies roles such as:

* Student
* Teacher
* HOD
* SS
* AS

based on the configured user information.

The system also maintains dedicated HOD and SS entities connected to users.

---

## 🏗️ System Architecture

The application follows the **Django MVT (Model-View-Template)** architecture.

### High-Level Architecture

```text
                    ┌──────────────────────┐
                    │      Web Browser     │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Django Application │
                    │      / Views         │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐        ┌─────────────────┐
        │     Templates   │        │      Models     │
        │      / UI       │        │   / Database    │
        └─────────────────┘        └────────┬────────┘
                                            │
                                            ▼
                                   ┌─────────────────┐
                                   │     Database    │
                                   └─────────────────┘
```

---

## 🛠️ Technology Stack

### Backend

* Python
* Django

### Database

* Relational Database supported by Django ORM

### Frontend

* HTML
* CSS
* JavaScript
* Django Templates

### Authentication

* Django Authentication Framework
* Custom User Model

### File Management

Django file/image fields are used for:

* Announcements
* Student profile pictures
* Staff avatars
* Student certificates

---

## 🗃️ Major Database Entities

The core database contains entities such as:

```text
Announcement
Schools
Department
Course
Branch
Semester
CustomUser
HOD
SS
Teacher
Student
Subject
Attendance
AttendanceReport
Timetable
Marks
FeeStructure
FinancialFees
Payment
Scholarship
Hostel
HostelDetails
HostelFees
Transport
TransportFees
StudentCertificate
NonTeachingStaff
Leave
```

These models form the foundation of the College ERP's academic and administrative data structure.

---

## 🔗 Academic Relationship Structure

```text
School
   │
   └── Department
          │
          └── Course / Program
                 │
                 ├── Branch
                 │
                 └── Semester
                        │
                        └── Subject
                               │
                               ├── Teacher
                               │
                               └── Student
```

---

## 💳 Student Financial Flow

```text
Student
   │
   ├── Fee Structure
   │      ├── Registration Fees
   │      ├── Academic Fees
   │      ├── Hostel Fees
   │      └── Transport Fees
   │
   ├── Scholarship / Discount
   │
   ├── Payments
   │
   └── Outstanding / Due Amount
```

The student model includes methods for calculating total fees, completed payments, and remaining dues.

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <PROJECT_DIRECTORY>
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

### 3. Activate the virtual environment

#### Windows

```bash
venv\Scripts\activate
```

#### Linux / macOS

```bash
source venv/bin/activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure environment variables

Create a `.env` file if the project uses environment variables and configure the required settings.

> Never commit passwords, secret keys, API keys, or other credentials to GitHub.

### 6. Apply database migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 7. Create an administrator

```bash
python manage.py createsuperuser
```

### 8. Start the development server

```bash
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/
```

---

## 📸 Screenshots

Add screenshots of the major ERP modules here.

Suggested screenshots:

* Login page
* Dashboard
* Student management
* Teacher management
* Attendance
* Timetable
* Marks/results
* Fee management
* Hostel management
* Transport management
* Announcements

Example:

```markdown
![Dashboard](screenshots/dashboard.png)
```

---

## 🔐 Security Considerations

The application uses Django's authentication framework and a customized user model for managing different types of users.

For production deployment, additional security practices should be followed, including:

* Secure environment variables
* Strong passwords
* HTTPS
* Production database configuration
* Proper permission management
* Secure file uploads
* Debug mode disabled

---



## 📄 License

This project is developed for educational and institutional use.

Add an appropriate open-source license if you intend to make the project publicly available for reuse.

---

⭐ If you find this project useful, consider giving the repository a star.
