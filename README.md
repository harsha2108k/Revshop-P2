# RevShop — Enterprise E-Commerce Platform

RevShop is a robust, full-featured e-commerce solution engineered with **Spring Boot**, **Thymeleaf**, **Spring Security**, and **Oracle Database**. The platform implements a multi-role architecture, supporting both **Buyers** and **Sellers** through dedicated dashboards, role-based access control (RBAC), and a streamlined shopping workflow.

---

## 📋 Table of Contents

- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Testing](#-testing)
- [API Reference](#-api-reference)
- [Security Implementation](#-security-implementation)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Key Features

### Buyer Capabilities
- **Secure Authentication:** User registration and login with encrypted credentials.
- **Product Discovery:** Advanced browsing and category-based filtering.
- **Shopping Workflow:** Intuitive cart management with real-time quantity updates.
- **Order Management:** Secure checkout process and comprehensive order history.
- **Personalization:** Product wishlists/favorites and review submission for purchased items.
- **Account Recovery:** Security question-based password recovery.
- **Notifications:** Real-time in-app alerts for order updates and promotions.

### Seller Capabilities
- **Business Onboarding:** Dedicated registration for commercial entities.
- **Inventory Dashboard:** Centralized management for tracking stock and sales.
- **Product Lifecycle Management:** Full CRUD operations for products, including high-quality image uploads.
- **Category Control:** Management of product categories to improve searchability.
- **Order Fulfillment:** Comprehensive view of incoming orders and customer demand.

### System-Wide Features
- **Security:** Industry-standard BCrypt password hashing and RBAC (BUYER / SELLER).
- **Navigation:** Custom login success handlers for role-specific redirection.
- **Observability:** Structured logging utilizing Log4j2.
- **Resilience:** Graceful handling of errors with custom 404 and 500 status pages.

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Backend** | Java 17, Spring Boot 4.0.3 |
| **Web Framework** | Spring MVC (WebMVC) |
| **Templating Engine** | Thymeleaf |
| **Security** | Spring Security (BCrypt, Form-Based Login) |
| **Persistence** | Spring Data JPA / Hibernate |
| **Database** | Oracle Database XE (ojdbc11) |
| **Logging** | Log4j2 |
| **Build Tool** | Maven |
| **Testing** | JUnit 5, Mockito, Spring Boot Test |

---

## 📁 Project Architecture

```text
revshop/
├── src/
│   ├── main/
│   │   ├── java/com/revshopproject/revshop/
│   │   │   ├── config/          # Security, Web, and Logging configurations
│   │   │   ├── controller/      # MVC and REST API endpoints
│   │   │   ├── dto/             # Data Transfer Objects
│   │   │   ├── entity/          # JPA Domain Models
│   │   │   ├── exception/       # Custom exceptions and Global Exception Handler
│   │   │   ├── repository/      # Spring Data JPA repositories
│   │   │   ├── security/        # UserDetailsService and Auth logic
│   │   │   ├── service/         # Business logic interfaces and implementations
│   │   │   └── utils/           # Utility classes (e.g., File I/O)
│   │   └── resources/
│   │       ├── templates/       # Thymeleaf HTML views
│   │       ├── static/          # Assets (CSS, JS, Images)
│   │       ├── application.properties
│   │       └── log4j2-spring.xml
│   └── test/                    # Comprehensive unit and integration tests
├── RevshopP2.sql                # Database schema and seed data
└── pom.xml                      # Project dependencies
```

---

## ✅ Prerequisites

Ensure the following are installed on your local environment:
- **Java Development Kit (JDK) 17** or higher
- **Apache Maven 3.8+**
- **Oracle Database XE**
- **Oracle JDBC Driver (`ojdbc11`)**

---

## 🚀 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/harsha2108k/Revshop-P2.git
cd revshop
```

### 2. Database Initialization
Execute the provided SQL script to initialize the schema and populate initial data:

**Using SQL*Plus:**
```bash
sqlplus username/password@localhost:1521/xe @RevshopP2.sql
```
**Manual Execution:**
Alternatively, run the contents of `RevshopP2.sql` in your preferred SQL client (e.g., Oracle SQL Developer).

### 3. Environment Configuration
Update `src/main/resources/application.properties` with your database credentials:

```properties
spring.datasource.url=jdbc:oracle:thin:@localhost:1521:xe
spring.datasource.username=YOUR_USERNAME
spring.datasource.password=YOUR_PASSWORD
```

---

## ⚙️ Configuration

Key application settings can be modified in `application.properties`:

- **Server Port:** Defaulted to `8888`.
- **JPA Strategy:** Set to `validate` to ensure schema integrity without modification.
- **File Upload Limits:**
    - Max File Size: 10MB
    - Max Request Size: 30MB

---

## ▶️ Usage

### Running the Application
Launch the application using the Maven wrapper:
```bash
./mvnw spring-boot:run
```
Once started, the platform is accessible at: **`http://localhost:8888`**

### Building for Production
To generate an executable JAR file:
```bash
./mvnw clean package -DskipTests
java -jar target/revshop-0.0.1-SNAPSHOT.jar
```

---

## 🧪 Testing

The project includes comprehensive unit tests for the service layer using JUnit 5 and Mockito. To execute the test suite:

```bash
./mvnw test
```

**Key Test Coverage:**
- `UserServiceImplTest` & `SellerServiceImplTest` (Account Logic)
- `ProductServiceImplTest` & `CategoryServiceImplTest` (Catalog Logic)
- `OrderServiceImplTest` & `CartServiceImplTest` (Transaction Logic)

---

## 🌐 API Reference

### Public Endpoints
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | Home Page / Product Catalog |
| `GET` | `/product/{id}` | Product Details |
| `POST` | `/api/users/register` | User Registration |

### Buyer Endpoints (Role: `BUYER`)
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET/POST` | `/api/cart/**` | Cart Operations |
| `POST` | `/api/orders/place` | Checkout |
| `GET` | `/api/orders/my-orders` | View Personal History |

### Seller Endpoints (Role: `SELLER`)
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/seller/**` | Seller Dashboard |
| `POST` | `/api/products/**` | Inventory Management |
| `PUT/DELETE` | `/api/products/**` | Product Updates/Removal |

---

## 🔒 Security Implementation

- **Encryption:** All user passwords utilize **BCrypt** hashing.
- **Session Management:** Secure session-based authentication via Spring Security.
- **Authorization:** Strict role-based access control for Buyer and Seller resources.
- **Integrity:** CSRF protection is enabled globally.
- **Recovery:** Secure password reset workflow via predefined security questions.

---

## 🤝 Contributing

1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/NewFeature`).
3. Commit your changes (`git commit -m 'Add some NewFeature'`).
4. Push to the Branch (`git push origin feature/NewFeature`).
5. Open a Pull Request.

---

## 📄 License

This project was developed for educational project.
