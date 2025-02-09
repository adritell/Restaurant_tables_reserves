# Restaurant Table Reservation System

A full-stack web application that allows for managing table reservations at restaurants. The system is designed so that both customers and administrators can interact securely and easily, using **Spring Boot** for the backend, **Angular** for the frontend, **MySQL** for data storage, and **Tailwind CSS** for a modern, responsive design.

---

## Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Entity-Relationship Model](#entity-relationship-model)
- [Project Structure](#project-structure)
- [Installation and Setup](#installation-and-setup)
- [License](#license)
- [Contact](#contact)

---

## Features

- **User Management**
  - Registration, authentication, and profile management.
  - Password recovery.
  - User roles (e.g., CUSTOMER and ADMIN).

- **Restaurant Management**
  - Creation, editing, and viewing of restaurant information.
  - Table allocation and definition of operating hours.

- **Table Management**
  - Table setup with attributes like number and capacity.
  - Association of tables to restaurants.

- **Schedule Management**
  - Definition of time slots when the restaurant is operational.
  - Configuration of available reservations by time slot.

- **Reservation System**
  - Creation, modification, and cancellation of reservations.
  - Real-time availability check.
  - Notifications and reservation confirmation.

- **Security**
  - JSON Web Token (JWT) based authentication.
  - Role-based access control.
  - Endpoint protection and encryption of sensitive data.

- **User Interface**
  - Responsive application developed with Angular.
  - Modern, adaptive design using Tailwind CSS.

---

## Technologies Used

- **Backend:**
  - **Java 11+**
  - **Spring Boot:** Facilitates the creation of enterprise applications with minimal configuration.
  - **Spring Data JPA:** Manages persistence and data access in MySQL.
  - **Spring Security:** Handles and controls security in the application.
  - **JWT (JSON Web Tokens):** Authentication and session management.

- **Frontend:**
  - **Angular:** Framework for developing dynamic web interfaces.
  - **Tailwind CSS:** CSS framework for a modern, responsive design.

- **Database:**
  - **MySQL:** Relational database for persistent storage.

- **Utilities:**
  - **Maven:** Dependency management and project lifecycle for the backend.
  - **Node.js & npm:** Dependency and script management for the Angular project.
  - **Docker (Optional):** For containerization and deployment of the application.

---

## Entity-Relationship Model

Here is a simplified entity-relationship model that defines the main structure of the database:

```mermaid
erDiagram
    USER {
        int id PK "Primary key"
        string name
        string email
        string password
        string role "e.g., ADMIN, CUSTOMER"
    }
    
    RESTAURANT {
        int id PK "Primary key"
        string name
        string address
        string phone
        string description
    }
    
    TABLE {
        int id PK "Primary key"
        int number "Table number"
        int capacity "Number of people"
        int restaurant_id FK "Foreign key to RESTAURANT"
    }
    
    SCHEDULE {
        int id PK "Primary key"
        time opening_time
        time closing_time
        int restaurant_id FK "Foreign key to RESTAURANT"
    }
    
    RESERVATION {
        int id PK "Primary key"
        datetime reservation_time "Date and time of the reservation"
        int user_id FK "Foreign key to USER"
        int restaurant_id FK "Foreign key to RESTAURANT"
        int table_id FK "Foreign key to TABLE"
        string status "e.g., PENDING, CONFIRMED, CANCELLED"
    }

    USER ||--o{ RESERVATION : "makes"
    RESTAURANT ||--o{ TABLE : "has"
    RESTAURANT ||--o{ SCHEDULE : "defines"
    RESTAURANT ||--o{ RESERVATION : "manages"
    TABLE ||--o{ RESERVATION : "is reserved at"
```




## Project Structure

```plaintext
reservation-system/
│── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/reservations/
│   │   │   │   ├── controllers/
│   │   │   │   ├── models/
│   │   │   │   ├── repositories/
│   │   │   │   ├── services/
│   │   │   ├── resources/
│   │   ├── test/
│   ├── pom.xml
│
│── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── views/
│   ├── angular.json
│   ├── package.json
│
│── docker-compose.yml (Optional)
│── README.md
```





