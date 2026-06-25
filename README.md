# Campus Placement Management Portal

Simple Java web application for a final-year / college project.

## Technology Stack

- Java 17
- Spring Boot 3.5.15
- Spring MVC
- Spring Data JPA
- Hibernate
- MySQL
- Thymeleaf
- No Spring Security, only simple session-based login for project demo

## Main Modules

### Student
- Register / Login
- Update profile
- Upload resume
- Search job openings
- Apply only when eligible
- Track application status

### Company
- Register / Login
- Post job opportunities / placement drives
- View eligible candidates
- View applications
- Shortlist students
- Update recruitment result

### Admin / Placement Officer
- View students
- View companies
- Verify companies
- View placement drives
- Monitor all applications
- Generate reports and analytics

## How to Run

### 1. Create MySQL database

You can create the database manually:

```sql
CREATE DATABASE campus_placement_db;
```

Or let Spring Boot create it automatically using the `createDatabaseIfNotExist=true` setting.

### 2. Add your DB credentials

Open:

```text
src/main/resources/application.properties
```

Replace:

```properties
spring.datasource.username=YOUR_MYSQL_USERNAME
spring.datasource.password=YOUR_MYSQL_PASSWORD
```

### 3. Run the application

```bash
mvn spring-boot:run
```

Open:

```text
http://localhost:8080
```

## Sample Login Data

The app automatically inserts sample records when the database is empty.

### Students
| Email | Password |
|---|---|
| rahul@example.com | 1234 |
| priya@example.com | 1234 |
| amit@example.com | 1234 |

### Companies
| Email | Password |
|---|---|
| hr@techsoft.com | 1234 |
| hr@cloudnova.com | 1234 |

Admin does not require login. Open:

```text
http://localhost:8080/admin
```

## Project Flow

```mermaid
flowchart TD
  A[Student Registration] --> B[Student Profile + Resume]
  C[Company Registration] --> D[Post Placement Drive]
  D --> E[Eligibility Criteria]
  B --> F[Eligibility Verification]
  E --> F
  F --> G[Eligible Student Applies]
  G --> H[Company Reviews Applications]
  H --> I[Shortlist / Interview]
  I --> J[Selected / Rejected / Waiting List / Offer Released]
  J --> K[Admin Reports]
```

## System Context

```mermaid
flowchart LR
  Student --> Portal[Campus Placement Portal]
  Company --> Portal
  Admin[Placement Officer / Admin] --> Portal
  Portal --> MySQL[(MySQL Database)]
  Portal --> Notifications[Status Messages / Notifications]
```

## Use Case Summary

```mermaid
flowchart LR
  S[Student] --> S1[Register/Login]
  S --> S2[Update Profile]
  S --> S3[Upload Resume]
  S --> S4[Search Jobs]
  S --> S5[Apply]
  S --> S6[Track Status]

  C[Company] --> C1[Register/Login]
  C --> C2[Post Jobs]
  C --> C3[View Applications]
  C --> C4[Shortlist]
  C --> C5[Update Results]

  A[Admin] --> A1[Manage Students]
  A --> A2[Manage Companies]
  A --> A3[Manage Drives]
  A --> A4[Generate Reports]
```

## Notes for Students

- Passwords are stored as plain text only because this is a simple academic project.
- In a real project, use Spring Security and encrypted passwords.
- Resume files are saved in the local folder `uploads/resumes`.
- Hibernate creates and updates tables automatically using `spring.jpa.hibernate.ddl-auto=update`.

## Troubleshooting Note

If you see `LazyInitializationException` while opening the student dashboard, make sure `JobOpportunity.company`, `JobApplication.student`, and `JobApplication.jobOpportunity` use `FetchType.EAGER` in this simple project version. This project intentionally uses eager loading for these small relationships so Thymeleaf pages can display company, job, and student details easily.
