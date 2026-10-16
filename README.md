# RaceDay Web API

A complete, production-ready ASP.NET Core Web API designed for athletic event management, race registrations, and live results tracking.

---

## 🛠 Tech Stack & Architecture

* **Framework:** ASP.NET Core Web API (.NET 8/9 SDK)
* **Database/ORM:** Entity Framework Core
* **Authentication:** JSON Web Tokens (JWT) with Role-Based Access Control (RBAC)
* **Testing:** xUnit, Moq, EF Core InMemory Provider

---

## 📂 Entity Schema Relationships

The relational data model manages the full lifecycle of an event through relational foreign keys:

$$\text{Events} \longrightarrow \text{Categories} \longrightarrow \text{Enrolments} \longrightarrow \text{Results}$$

* **`Users`**: Holds system credentials, participant/organizer roles, and profile info.
* **`Venue`**: Stores geographic and physical venue hosting details.
* **`Events`**: Represents the race competition managed by an organizer.
* **`Categories`**: Defines race distances (e.g., 5km, 10km, 21km) tied to an `EventID`.
* **`Enrolments`**: Connects a `ParticipantID` to a specific `CategoryID` and generates registration data.
* **`Results`**: Stores official finish times and final rankings tied to an `EnrolmentID`.

---

## 🚀 API Endpoint Reference

### 1. Authentication
| Method | Route | Access | Description |
|---|---|---|---|
| `POST` | `/api/auth/register` | Public | Registers a new user account and returns a JWT token. |
| `POST` | `/api/auth/login` | Public | Verifies credentials and returns a JWT token with user role claims. |

### 2. User Profiles
| Method | Route | Access | Description |
|---|---|---|---|
| `GET` | `/api/users/profile` | Authenticated | Retrieves the authenticated user's profile information. |
| `PUT` | `/api/users/profile` | Authenticated | Updates contact numbers and emergency details. |

### 3. Events & Categories
| Method | Route | Access | Description |
|---|---|---|---|
| `GET` | `/api/events` | Public | Lists all upcoming events with optional type and date filters. |
| `POST` | `/api/events` | Organiser | Creates a new race event. |
| `GET` | `/api/events/{id}` | Public | Retrieves full event details, venue data, and distance categories. |
| `GET` | `/api/events/{id}/categories` | Public | Retrieves all distance categories associated with an event. |
| `POST` | `/api/events/{id}/categories` | Organiser | Adds a new distance category to a specific event. |

### 4. Enrolments
| Method | Route | Access | Description |
|---|---|---|---|
| `POST` | `/api/enrolments` | Participant | Registers a participant into a race category (prevents duplicate entries). |
| `GET` | `/api/enrolments/my-entries
