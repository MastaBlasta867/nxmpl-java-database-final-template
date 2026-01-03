Warehouse Retail System – Backend
The Warehouse Retail System is a backend service for a warehouse distribution company that manages multiple retail stores. It provides internal admin users with tools to manage stores, products, inventory, customer orders, and product reviews.

The system uses:

MySQL for core transactional data

MongoDB for unstructured customer reviews

This project was built as a full backend implementation using Java, Spring Boot, and Hibernate, with an emphasis on clean architecture, clear domain modeling, and production‑style practices.

1. Core Features
Store Management
Create, update, list, and deactivate retail stores

Store metadata such as location, status, and identifiers

Product Catalog Management
Manage the entire product catalog with categories, pricing, and activation status

Designed to support large catalogs across multiple stores

Inventory Management
Track inventory per store and product

View stock levels by store

Update stock levels and enforce constraints (e.g., cannot reduce below zero)

Order Placement
Place customer orders through internal tools (phone or in‑store)

Calculate totals, validate inventory, and update stock atomically

Associate orders with stores, customers, and line items

Customer Management
Basic customer profiles for order tracking and analytics

Review System (MongoDB / NoSQL)
Store product reviews as unstructured or semi‑structured data

Fetch reviews per product

Reporting (MySQL Stored Procedures)
Monthly sales per store

Aggregate company sales by month and year

Top‑selling products by category

Error Handling
Global exception handling

Standardized error responses for the frontend

2. Architecture Overview
At a high level, the system is a layered Spring Boot application:

Controller Layer
Exposes REST APIs to the frontend, handles HTTP requests and responses.

Service Layer
Contains business logic, validations, and orchestration across repositories.

Repository Layer
Communicates with databases using:

Spring Data JPA (MySQL)

Spring Data MongoDB (MongoDB)

Data Layer
Contains:

JPA entities for structured SQL data

MongoDB documents for unstructured review data

Backend Design Principles
Clear separation of concerns

Domain‑focused models (Store, Product, Inventory, Order, Customer, Review)

Transactional integrity around order placement and inventory updates

3. Tech Stack
Language: Java (Spring Boot)

Frameworks: Spring Boot, Spring Web, Spring Data JPA, Spring Data MongoDB, Hibernate

Databases:

MySQL (relational, transactional data)

MongoDB (NoSQL, reviews)

Build Tool: Maven or Gradle

Documentation: README, JavaDoc

Testing: JUnit, Spring Boot Test

4. Domain Model (Business Entities)
4.1 SQL Entities (MySQL via JPA/Hibernate)
Store
Represents a physical or virtual retail location

Contains name, code, address, active status

Product
Represents items in the catalog

Includes SKU, name, category, description, price, active status

Inventory
Connects a Store and a Product

Tracks quantity available per store

Customer
Represents a customer placing orders

Includes basic contact information

OrderDetails (Order Header)
Main order record

Contains store, customer, date, status, total amount

Connected to multiple OrderItem entries

OrderItem
Represents line items for each order

Includes product, quantity, unit price, line total

4.2 NoSQL Documents (MongoDB)
Review
Stores customer reviews for products

Contains product reference, rating, comment, timestamps

Uses MongoDB for flexible schema evolution
src/main/java/com/example/warehouseretailsystem
├── controller
│   ├── StoreController.java
│   ├── ProductController.java
│   ├── InventoryController.java
│   ├── OrderController.java
│   ├── CustomerController.java
│   └── ReviewController.java
├── service
│   ├── StoreService.java
│   ├── ProductService.java
│   ├── InventoryService.java
│   ├── OrderService.java
│   ├── CustomerService.java
│   └── ReviewService.java
├── repository
│   ├── StoreRepository.java
│   ├── ProductRepository.java
│   ├── InventoryRepository.java
│   ├── OrderDetailsRepository.java
│   ├── OrderItemRepository.java
│   ├── CustomerRepository.java
│   └── ReviewRepository.java
├── model
│   ├── sql
│   │   ├── Store.java
│   │   ├── Product.java
│   │   ├── Inventory.java
│   │   ├── Customer.java
│   │   ├── OrderDetails.java
│   │   └── OrderItem.java
│   └── nosql
│       └── Review.java
├── dto
│   ├── OrderRequestDto.java
│   ├── OrderItemRequest.java
│   └── other DTOs as needed
├── exception
│   ├── GlobalExceptionHandler.java
│   ├── ResourceNotFoundException.java
│   ├── InsufficientStockException.java
│   └── other custom exceptions
└── config
    ├── DatabaseConfig.java
    └── MongoConfig.java
