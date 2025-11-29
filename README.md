# RestAssured Cucumber APITesting Automation Framework

A comprehensive **Behavior-Driven Development (BDD)** test automation framework for testing the Restful-Booker API using **Cucumber**, **RestAssured**, and **Java**.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Test Coverage](#test-coverage)
- [Architecture](#architecture)

---

## 🎯 Project Overview

This framework automates API testing for the **Restful-Booker** (`https://restful-booker.herokuapp.com`) — a sample hotel booking REST API. It implements **CRUD operations** (Create, Read, Update, Delete) on booking resources using a **data-driven approach** with multiple data sources.

### API Under Test

**Base URL:** `https://restful-booker.herokuapp.com`

**Main Endpoints:**
- `POST /auth` — Generate authentication tokens
- `GET /booking` — Retrieve all booking IDs or filtered bookings
- `GET /booking/{id}` — Get specific booking details
- `POST /booking` — Create new booking
- `PUT /booking/{id}` — Update booking (full update)
- `PATCH /booking/{id}` — Partial update booking
- `DELETE /booking/{id}` — Delete booking
- `GET /ping` — Health check endpoint

---

## ✨ Features

### 1. **Behavior-Driven Development (BDD)**
- Tests written in human-readable Gherkin syntax
- Feature files describe business requirements
- Easy for non-technical stakeholders to understand

### 2. **Data-Driven Testing**
- **Cucumber DataTables** — Inline test data
- **Excel Files** (`testData.xlsx`) — External structured data
- **JSON Files** (`bookingBody.json`) — JSON-based test data
- **Scenario Outlines** — Multiple test iterations with different parameters

### 3. **Comprehensive Test Coverage**
- ✅ Create booking operations
- ✅ View/Read booking details
- ✅ Update booking details (full and partial)
- ✅ Delete booking operations
- ✅ End-to-End (E2E) CRUD workflow
- ✅ Authentication & authorization
- ✅ Health check validation

### 4. **JSON Schema Validation**
- Validate API response structure and data types
- Ensures responses conform to expected schemas
- Catches breaking changes in API contracts

### 5. **Authentication Support**
- Token-based authentication via `/auth` endpoint
- Basic authentication for protected operations
- Secure credentials management

### 6. **Advanced Filtering**
- Filter bookings by check-in/checkout dates
- Filter bookings by customer name
- Retrieve all booking IDs

---

## 🛠️ Technology Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| **Framework** | Cucumber (BDD) | 7.x+ |
| **Language** | Java | 11+ |
| **Build Tool** | Maven | 3.6+ |
| **HTTP Client** | RestAssured | 5.x+ |
| **JSON Processing** | io.rest-assured | 5.x+ |
| **Assertions** | JUnit / AssertJ | 4.13+ |
| **JSON Schema Validation** | json-schema-validator | 1.0+ |
| **Logging** | Log4j / SLF4J | 2.x / 1.7+ |
| **Test Runner** | JUnit | 4.13+ |
| **CI/CD** | GitHub Actions | Latest |

---

## 📁 Project Structure

```
restful-booker-automation/
│
├── src/
│   ├── test/
│   │   ├── java/
│   │   │   ├── stepDefinitions/
│   │   │   │   ├── BookingSteps.java          # Booking operation steps
│   │   │   │   ├── AuthSteps.java             # Authentication steps
│   │   │   │   ├── CommonSteps.java           # Common/reusable steps
│   │   │   │   └── ValidationSteps.java       # Assertion & validation steps
│   │   │   │
│   │   │   ├── context/
│   │   │   │   └── APIContext.java            # Context class for state management
│   │   │   │
│   │   │   ├── utilities/
│   │   │   │   ├── RestAssuredConfig.java     # RestAssured configuration
│   │   │   │   ├── DataReader.java            # Excel/JSON data reader
│   │   │   │   ├── SchemaValidator.java       # JSON schema validation
│   │   │   │   └── PropertyReader.java        # Configuration properties reader
│   │   │   │
│   │   │   ├── runners/
│   │   │   │   └── TestRunner.java            # Cucumber test runner
│   │   │   │
│   │   │   └── models/
│   │   │       ├── BookingRequest.java        # Request POJO
│   │   │       └── BookingResponse.java       # Response POJO
│   │   │
│   │   └── resources/
│   │       ├── features/
│   │       │   ├── CreateBooking.feature      # Create booking scenarios
│   │       │   ├── ViewBookingDetails.feature # View booking scenarios
│   │       │   ├── UpdateBooking.feature      # Update booking scenarios
│   │       │   └── DeleteBooking.feature      # Delete booking scenarios
│   │       │
│   │       ├── testdata/
│   │       │   ├── testData.xlsx              # Excel test data
│   │       │   └── bookingBody.json           # JSON test data
│   │       │
│   │       ├── schemas/
│   │       │   ├── createBookingSchema.json   # Create booking response schema
│   │       │   ├── bookingDetailsSchema.json  # Booking details response schema
│   │       │   ├── bookSchema.json            # Book response schema
│   │       │   └── userSchema.json            # User response schema
│   │       │
│   │       └── config/
│   │           ├── application.properties     # Configuration properties
│   │           └── log4j2.xml                 # Logging configuration
│
├── .github/
│   └── workflows/
│       └── maven.yml                          # GitHub Actions CI/CD pipeline
│
├── pom.xml                                    # Maven configuration
├── README.md                                  # This file
└── .gitignore                                 # Git ignore rules

```
---

## 📊 Test Coverage

### Test Scenarios Implemented

#### 1. **Create Booking** (`CreateBooking.feature`)
- ✅ Create booking using Cucumber DataTable
- ✅ Create booking using Excel data
- ✅ Create booking using JSON data
- **Data Driven:** 2+ test iterations per scenario

#### 2. **View Booking Details** (`ViewBookingDetails.feature`)
- ✅ View all booking IDs
- ✅ View specific booking details by ID
- ✅ Filter bookings by check-in/checkout dates
- ✅ Filter bookings by customer name
- ✅ Health check endpoint validation
- **Data Driven:** 2+ date range variations

#### 3. **Update Booking** (`UpdateBooking.feature`)
- ✅ Full update using DataTable
- ✅ Full update using Excel data
- ✅ Full update using JSON data
- ✅ Partial update (PATCH) specific fields
- **Authentication Required:** Background creates auth token
- **Data Driven:** 2+ test iterations per scenario

#### 4. **Delete Booking** (`DeleteBooking.feature`)
- ✅ Delete specific booking
- ✅ End-to-End CRUD workflow (Create → Update → View → Delete)
- **Authentication Required:** Background creates auth token
- **Comprehensive Validation:** Schema & status code verification

### Total Test Coverage

| Operation | Scenarios | Data Sets | Total Tests |
|-----------|-----------|-----------|------------|
| Create | 3 | 2-3 each | 8-9 |
| View | 5 | 2-3 each | 10-12 |
| Update | 4 | 2-3 each | 10-12 |
| Delete | 2 | 1-2 each | 3-4 |
| **Total** | **14** | **Multiple** | **31-37** |

---

## 🏗️ Architecture

### Three-Tier Architecture

```
┌──────────────────────────────────────────────────────┐
│         FEATURE FILES (Gherkin/BDD)                  │
│  Business-readable test scenarios & requirements    │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│      STEP DEFINITIONS (Java Implementation)          │
│  Maps Gherkin steps to Java code                    │
│  - BookingSteps                                      │
│  - AuthSteps                                         │
│  - CommonSteps                                       │
│  - ValidationSteps                                   │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│   CONTEXT & UTILITIES (State & Helper Classes)      │
│  - APIContext (state management)                    │
│  - RestAssuredConfig (HTTP configuration)           │
│  - DataReader (Excel/JSON parsing)                  │
│  - SchemaValidator (JSON schema validation)         │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│    RESTASSURED LIBRARY (HTTP Communication)         │
│  Sends requests & receives responses                │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│      RESTFUL-BOOKER API (System Under Test)         │
│  https://restful-booker.herokuapp.com               │
└──────────────────────────────────────────────────────┘
```

### Request/Response Flow

```
User runs mvn test
       ↓
Cucumber reads .feature files
       ↓
TestRunner identifies scenarios
       ↓
For each scenario:
   ├─ Create APIContext instance
   ├─ Execute Background (if exists)
   │  └─ Create auth token → Store in context
   ├─ Execute each step:
   │  ├─ Step Definition retrieves context
   │  ├─ Builds RestAssured request
   │  ├─ Sends HTTP request
   │  ├─ Receives response
   │  ├─ Stores response in context
   │  └─ Validates response
   └─ Destroy context
       ↓
Generate HTML report
       ↓
Display results
```

---
