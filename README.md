# 🏥 Clinique Rendez-Vous: Online Appointment Booking System

Welcome to the **Clinique Rendez-Vous** project! This is a comprehensive full-stack application designed to streamline the process of booking and managing medical appointments. It provides dedicated interfaces for patients, doctors, and administrators, ensuring a smooth and efficient healthcare experience.

---

### 🧠 Overview

This project aims to revolutionize traditional clinic appointment systems by offering a robust online platform. Patients can easily discover doctors and book appointments, while doctors can manage their schedules and patient interactions. Administrators have full control over user management and appointment oversight. The system is built with a modern React frontend and a powerful Spring Boot backend, integrated with JWT for secure authentication and a MySQL database for reliable data storage.

---

### ⚙️ Features

This application offers distinct functionalities tailored for different user roles:

#### Patient Features:

- **User Registration & Login:** Securely register and log in to access patient-specific features.
- **Doctor Directory:** Browse a list of available doctors with their specialties and contact details.
- **Doctor Profiles:** View detailed information about each doctor, including their availability slots.
- **Appointment Booking:** Schedule new appointments with chosen doctors based on their availability.
- **Appointment Management:** View all scheduled appointments and modify the appointment's motif.
- **Appointment Cancellation:** Delete upcoming appointments.

#### Doctor Features:

- **Dashboard Overview:** Get a quick summary of appointments, pending requests, and total patients.
- **Appointment Management:** View, accept, or reject patient appointment requests.
- **Availability Management:** Add or remove personal availability slots for patients to book.
- **Patient List:** Access a list of patients who have booked appointments with them.
- **Appointment Prediction (Backend Only):** The system has a backend capability to predict future appointment trends for doctors based on historical data.

#### Admin Features:

- **Admin Dashboard:** Centralized control panel for system management.
- **Doctor Management:** Add new doctors, update existing doctor profiles, or remove doctors from the system.
- **Patient Management:** Add new patients, modify patient information, or remove patient records.
- **Appointment Management:** Oversee all appointments in the system, with the ability to add, update, or delete any appointment.

---

### 🗂️ Project Structure

The project is divided into two main components: a `frontend` React application and a `Springboot` (Java/Spring Boot) backend.

```
.
├── frontend/                     # React.js application for the user interface
│   ├── public/                   # Static assets (HTML template, icons)
│   ├── src/                      # Source code for the React app
│   │   ├── Admin/                # Admin-specific components and pages
│   │   ├── Medecin/              # Doctor-specific components and pages
│   │   ├── Patient/              # Patient-specific components and pages
│   │   ├── AuthContext.js        # React Context for global authentication state
│   │   ├── App.js                # Main application component, handles routing
│   │   ├── login.js              # Login page component
│   │   ├── register.js           # Registration page component
│   │   ├── logout.js             # Logout component
│   │   └── ...                   # Other shared components (Header) and CSS files
│   ├── package.json              # Frontend dependencies and scripts (npm)
│   ├── package-lock.json         # Locked dependencies for npm
│   └── yarn.lock                 # Locked dependencies for Yarn
│
└── Springboot/                   # Spring Boot application for the backend API
    ├── .mvn/                     # Maven Wrapper files
    ├── src/main/java/com/backend/backend/ # Java source code
    │   ├── Controllers/          # REST API endpoints
    │   │   ├── AdminController.java
    │   │   ├── DisponibiliteController.java
    │   │   ├── MedecinController.java
    │   │   ├── PatientController.java
    │   │   ├── RendezVousController.java
    │   │   ├── PredictionController.java
    │   │   └── JwtModule/Controllers/ # Authentication related controllers
    │   │       ├── AuthController.java
    │   │       └── LogoutController.java
    │   ├── Models/               # JPA Entities (database models)
    │   │   ├── Admin.java
    │   │   ├── Disponibilite.java
    │   │   ├── Medecin.java
    │   │   ├── Patient.java
    │   │   ├── RendezVous.java
    │   │   └── JwtModule/models/AppUser.java # User model for authentication
    │   ├── Repository/           # Spring Data JPA repositories for database interaction
    │   │   └── ...               # Repositories for each model
    │   ├── Services/             # Business logic layer
    │   │   └── ...               # Services for each model and authentication
    │   │       └── PredictionService.java # Logic for appointment prediction
    │   └── JwtModule/            # JWT (JSON Web Token) related components
    │       ├── config/           # Security configuration and Swagger setup
    │       ├── dto/              # Data Transfer Objects for Auth
    │       ├── services/         # UserDetailsService for Spring Security
    │       └── util/             # JWT utility class for token operations
    │
    ├── src/main/resources/       # Configuration files
    │   └── application.properties # Database connection, server port, and other Spring settings
    ├── pom.xml                   # Backend dependencies and build configuration (Maven)
    └── mvnw                      # Maven Wrapper script (Linux/macOS)
    └── mvnw.cmd                  # Maven Wrapper script (Windows)
```

---

### 🌐 API Endpoints

The backend exposes a set of RESTful APIs to manage users, doctors, patients, appointments, and availabilities.

| Method   | Endpoint                                  | Description                                                             | Request Body (Example)                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Response (Example)                                                                                                                                  |
| :------- | :---------------------------------------- | :---------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| `POST`   | `/api/auth/login`                         | Authenticates a user and returns a JWT token, role, and user ID.        | `{ "email": "user@example.com", "motDePasse": "password" }`                                                                                                                                                                                                                                                                                                                                                                                                                                  | `{ "token": "eyJ...", "role": "ROLE_PATIENT", "id": 1 }`                                                                                            |
| `POST`   | `/api/auth/register`                      | Registers a new user (Patient, Medecin, or Admin).                      | Patient: `{ "nom": "Jane", "prenom": "Doe", "email": "patient@example.com", "motDePasse": "password123", "telephone": "1234567890", "adresse": "123 Main St", "sexe": "Femme", "dateNaissance": "1990-01-01", "role": "PATIENT" }`<br>Medecin: `{ "nom": "Dr. John", "prenom": "Smith", "email": "doctor@example.com", "motDePasse": "password123", "telephone": "0987654321", "adresseCabinet": "456 Oak Ave", "specialite": "Cardiology", "prixConsultation": 100.00, "role": "MEDECIN" }` | `"Utilisateur enregistré avec succès !"`                                                                                                            |
| `POST`   | `/api/auth/logout`                        | Logs out the current user (client-side token removal).                  | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `"Déconnexion réussie"`                                                                                                                             |
| `GET`    | `/api/medecins`                           | Retrieves a list of all doctors.                                        | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "nom": "John", "prenom": "Doe", "specialite": "Cardiology", ... }, ... ]`                                                             |
| `GET`    | `/api/medecins/{id}`                      | Retrieves a doctor by ID.                                               | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `{ "id": 1, "nom": "John", "prenom": "Doe", "specialite": "Cardiology", ... }`                                                                      |
| `POST`   | `/api/medecins/add`                       | Adds a new doctor. (Admin only)                                         | `{ "nom": "Alice", "prenom": "Brown", "specialite": "Pediatrics", "email": "alice@example.com", "telephone": "1112223333", "adresseCabinet": "789 Pine St", "prixConsultation": 80.0 }`                                                                                                                                                                                                                                                                                                      | `(No content, status 200 OK)`                                                                                                                       |
| `PUT`    | `/api/medecins/update/{id}`               | Updates an existing doctor by ID. (Admin only)                          | `{ "id": 1, "nom": "Johnathan", "prenom": "Doe", "specialite": "Cardiology", ... }`                                                                                                                                                                                                                                                                                                                                                                                                          | `(No content, status 200 OK)`                                                                                                                       |
| `DELETE` | `/api/medecins/{id}`                      | Deletes a doctor by ID. (Admin only)                                    | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `(No content, status 200 OK)`                                                                                                                       |
| `GET`    | `/api/patients`                           | Retrieves a list of all patients. (Admin only)                          | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "nom": "Jane", "prenom": "Doe", "email": "jane@example.com", ... }, ... ]`                                                            |
| `GET`    | `/api/patients/{id}`                      | Retrieves a patient by ID. (Admin only)                                 | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `{ "id": 1, "nom": "Jane", "prenom": "Doe", "email": "jane@example.com", ... }`                                                                     |
| `POST`   | `/api/patients/add`                       | Adds a new patient. (Admin only)                                        | `{ "nom": "Bob", "prenom": "Lee", "email": "bob@example.com", "motDePasse": "securepass", "telephone": "4445556666", "dateNaissance": "1985-05-10", "adresse": "321 River Rd", "sexe": "Homme" }`                                                                                                                                                                                                                                                                                            | `{ "id": 2, "nom": "Bob", ... }` (Status 201 Created)                                                                                               |
| `PUT`    | `/api/patients/update/{id}`               | Updates an existing patient by ID. (Admin only)                         | `{ "id": 1, "nom": "Janet", "prenom": "Doe", ... }`                                                                                                                                                                                                                                                                                                                                                                                                                                          | `{ "id": 1, "nom": "Janet", ... }`                                                                                                                  |
| `DELETE` | `/api/patients/{id}`                      | Deletes a patient by ID. (Admin only)                                   | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `(No content, status 200 OK)`                                                                                                                       |
| `GET`    | `/api/medecin/{medecinId}/patients`       | Retrieves all patients associated with a specific doctor. (Doctor only) | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "nom": "Jane", "prenom": "Doe", ... }, ... ]`                                                                                         |
| `GET`    | `/api/rendezvous`                         | Retrieves a list of all appointments.                                   | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "patient": {...}, "medecin": {...}, "dateRdv": "2024-07-20T10:00:00", "statut": "Pending", "motif": "Check-up" }, ... ]`              |
| `GET`    | `/api/rendezvous/{id}`                    | Retrieves an appointment by ID.                                         | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `{ "id": 1, "patient": {...}, "medecin": {...}, "dateRdv": "2024-07-20T10:00:00", "statut": "Pending", "motif": "Check-up" }`                       |
| `GET`    | `/api/rendezvous/medecin/{medecinId}`     | Retrieves all appointments for a specific doctor. (Doctor only)         | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "patient": {...}, "medecin": {...}, "dateRdv": "2024-07-20T10:00:00", "statut": "Pending", "motif": "Check-up" }, ... ]`              |
| `POST`   | `/api/rendezvous/add`                     | Adds a new appointment.                                                 | `{ "patient": { "id": 1 }, "medecin": { "id": 2 }, "dateRdv": "2024-08-15T11:00:00", "statut": "Pending", "motif": "Follow-up" }`                                                                                                                                                                                                                                                                                                                                                            | `{ "id": 2, "patient": {...}, "medecin": {...}, "dateRdv": "2024-08-15T11:00:00", "statut": "Pending", "motif": "Follow-up" }` (Status 201 Created) |
| `PUT`    | `/api/rendezvous/update/{id}`             | Updates an existing appointment by ID.                                  | `{ "id": 1, "patient": { "id": 1 }, "medecin": { "id": 2 }, "dateRdv": "2024-07-21T10:30:00", "statut": "Confirmed", "motif": "Urgent consultation" }`                                                                                                                                                                                                                                                                                                                                       | `{ "id": 1, "patient": {...}, "medecin": {...}, "dateRdv": "2024-07-21T10:30:00", "statut": "Confirmed", "motif": "Urgent consultation" }`          |
| `DELETE` | `/api/rendezvous/{id}`                    | Deletes an appointment by ID.                                           | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `(No content, status 200 OK)`                                                                                                                       |
| `GET`    | `/api/disponibilites`                     | Retrieves all availability slots.                                       | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "medecin": {...}, "date": "2024-07-25", "startTime": "09:00:00", "endTime": "17:00:00" }, ... ]`                                      |
| `GET`    | `/api/disponibilites/medecin/{medecinId}` | Retrieves availability slots for a specific doctor.                     | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `[ { "id": 1, "medecin": {...}, "date": "2024-07-25", "startTime": "09:00:00", "endTime": "17:00:00" }, ... ]`                                      |
| `POST`   | `/api/disponibilites/add`                 | Adds a new availability slot. (Doctor only)                             | `{ "medecin": { "id": 2 }, "date": "2024-08-01", "startTime": "09:00:00", "endTime": "13:00:00" }`                                                                                                                                                                                                                                                                                                                                                                                           | `{ "id": 2, "medecin": {...}, "date": "2024-08-01", "startTime": "09:00:00", "endTime": "13:00:00" }`                                               |
| `PUT`    | `/api/disponibilites/update/{id}`         | Updates an existing availability slot by ID. (Doctor only)              | `{ "id": 1, "medecin": { "id": 2 }, "date": "2024-07-26", "startTime": "10:00:00", "endTime": "18:00:00" }`                                                                                                                                                                                                                                                                                                                                                                                  | `{ "id": 1, "medecin": {...}, "date": "2024-07-26", "startTime": "10:00:00", "endTime": "18:00:00" }`                                               |
| `DELETE` | `/api/disponibilites/{id}`                | Deletes an availability slot by ID. (Doctor only)                       | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `(No content, status 200 OK)`                                                                                                                       |
| `GET`    | `/api/predictions/medecins`               | Predicts future appointment counts for doctors using linear regression. | `(None)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `{ "1": 15.5, "2": 22.1, ... }` (Doctor ID to predicted appointment count)                                                                          |

---

### 🧩 Frontend Pages

The React frontend provides a dynamic user interface with distinct pages for various functionalities:

- **Home Page (`/`)**:
  - **Description**: The landing page of the application, welcoming users and highlighting key features and services of the clinic.
  - **Interaction**: Provides navigation links to other parts of the application, particularly for booking appointments.
  - **Components**: Displays hero section, services, and advantages of the clinic.
- **Login Page (`/login`)**:
  - **Description**: Allows registered users (patients, doctors, or admins) to log into their respective accounts.
  - **Interaction**: Sends `POST` requests to `/api/auth/login` with user credentials. Upon successful login, receives a JWT token, user role, and user ID from the backend, which are then stored in local storage and used for subsequent authenticated requests. Redirects users based on their role (`/Admin`, `/DashboardMedecin`, `/`).
- **Register Page (`/register`)**:
  - **Description**: Enables new users to create an account as a patient or a doctor. Admin registration would typically be managed internally or by existing admins.
  - **Interaction**: Sends `POST` requests to `/api/auth/register` with user details (name, email, password, role, etc.). Redirects to the login page upon successful registration.
- **Doctors Page (`/medecins`)**:
  - **Description**: Displays a comprehensive list of all doctors available in the system.
  - **Interaction**: Fetches doctor data from `/api/medecins` via `GET` request. Users can click on a doctor to view their detailed profile.
- **Doctor Details Page (`/medecins/:id`)**:
  - **Description**: Shows detailed information about a specific doctor and allows patients to book appointments.
  - **Interaction**: Fetches doctor details from `/api/medecins/{id}` and their availability from `/api/disponibilites/medecin/{id}`. Patients can select an available slot and send a `POST` request to `/api/rendezvous/add` to book an appointment. It also fetches the patient's existing appointments from `/api/rendezvous/patient/{patientId}` to check for overlaps.
- **Appointments Page (`/Rendez-vous`) (Patient View)**:
  - **Description**: Allows logged-in patients to view and manage their personal appointments.
  - **Interaction**: Fetches patient-specific appointments from `/api/rendezvous` (filtered by `userId`). Patients can update an appointment's motif by sending a `PUT` request to `/api/rendezvous/update/{id}` or delete an appointment with a `DELETE` request to `/api/rendezvous/{id}`.
- **Admin Dashboard (`/Admin`)**:
  - **Description**: The main entry point for administrators, providing links to manage different entities within the system.
  - **Interaction**: Purely navigational within the frontend, leading to other admin management pages. Enforces `ROLE_ADMIN` authentication.
- **Admin Patient Management (`/AdminPatient`)**:
  - **Description**: Provides an interface for administrators to manage patient records (view, add, edit, delete).
  - **Interaction**: Interacts with `/api/patients` for `GET` (all), `POST` (add), `PUT` (update), and `DELETE` (delete) operations.
- **Admin Doctor Management (`/AdminMedecin`)**:
  - **Description**: Provides an interface for administrators to manage doctor records (view, add, edit, delete).
  - **Interaction**: Interacts with `/api/medecins` for `GET` (all), `POST` (add), `PUT` (update), and `DELETE` (delete) operations.
- **Admin Appointment Management (`/AdminRendezVous`)**:
  - **Description**: Allows administrators to manage all appointments in the system (view, add, edit, delete).
  - **Interaction**: Interacts with `/api/rendezvous` for `GET` (all), `POST` (add), `PUT` (update), and `DELETE` (delete) operations. Also fetches lists of patients and doctors from `/api/patients` and `/api/medecins` for selection during appointment creation/editing.
- **Doctor Dashboard (`/DashboardMedecin`)**:
  - **Description**: The primary dashboard for doctors, summarizing their appointments, patients, and allowing management of availabilities.
  - **Interaction**: Fetches doctor details from `/api/medecins/{medecinId}`, appointments from `/api/rendezvous/medecin/{medecinId}`, patients from `/api/medecin/{medecinId}/patients`, and availabilities from `/api/disponibilites/medecin/{medecinId}`. Allows creating new availabilities (`POST /api/disponibilites/add`), updating appointment statuses (e.g., `PUT /api/rendezvous/update/{id}`), and deleting availabilities (`DELETE /api/disponibilites/{id}`).

---

### 🛠️ Tech Stack

This project leverages a modern full-stack architecture:

**Frontend:**

- **React.js**: A JavaScript library for building user interfaces.
- **React Router DOM v6**: For declarative routing in the application.
- **Bootstrap 5 & React-Bootstrap**: Responsive UI components and styling.
- **Axios**: Promise-based HTTP client for making API requests.
- **Lucide-React & React-Feather & React-Icons**: Icon libraries for enhanced UI.
- **JWT-Decode**: Client-side decoding of JWT tokens.
- **React-Toastify**: For professional-looking toast notifications.
- **Chart.js**: For data visualization on dashboards (if implemented).

**Backend:**

- **Spring Boot (3.4.4)**: A powerful framework for building robust, stand-alone, production-grade Spring applications.
- **Java 21**: The programming language used for the backend.
- **Spring Data JPA**: For easy interaction with the database.
- **Hibernate ORM**: JPA implementation for object-relational mapping.
- **Spring Security & JWT**: For secure authentication and authorization.
  - `jjwt-api`, `jjwt-impl`, `jjwt-jackson` for JWT token handling.
- **MySQL**: Relational database for storing application data.
- **Lombok**: Reduces boilerplate code (e.g., getters, setters, constructors).
- **SpringDoc OpenAPI UI / Swagger**: For automatic generation and serving of API documentation.
- **Apache Commons Math3**: Used for statistical operations, specifically linear regression in the prediction service.
- **Maven**: Build automation tool.

---

### 🚀 Installation & Usage

Follow these steps to set up and run the Clinique Rendez-Vous application locally.

#### Prerequisites

- **Java Development Kit (JDK) 21 or higher**
- **Node.js (LTS version recommended)**
- **npm** (comes with Node.js) or **Yarn**
- **MySQL Database** (or other relational database supported by JPA)

#### 1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-directory>
```

#### 2. Backend Setup (Springboot)

1.  **Navigate to the backend directory:**

    ```bash
    cd Springboot
    ```

2.  **Configure Database:**

    - Open `src/main/resources/application.properties`.
    - Ensure your MySQL database connection details are correctly configured:
      ```properties
      spring.datasource.url=jdbc:mysql://localhost:3306/springbootdb
      spring.datasource.username=root
      spring.datasource.password=
      ```
      - **Note**: Replace `springbootdb` with your database name, `root` with your MySQL username, and provide your `password` if you have one configured.
      - The application uses `spring.jpa.hibernate.ddl-auto=update`, which will automatically create/update tables on startup if they don't exist.

3.  **Build the Backend:**

    - Use Maven to build the project.

    ```bash
    ./mvnw clean install
    # On Windows, use: mvnw.cmd clean install
    ```

4.  **Run the Backend Application:**
    ```bash
    ./mvnw spring-boot:run
    # On Windows, use: mvnw.cmd spring-boot:run
    ```
    The backend will start on `http://localhost:8082`.
    You can verify the API documentation (Swagger UI) at `http://localhost:8082/swagger-ui.html`.

#### 3. Frontend Setup (React)

1.  **Open a new terminal and navigate to the frontend directory:**

    ```bash
    cd ../frontend
    ```

2.  **Install Dependencies:**

    - Using npm:
      ```bash
      npm install
      ```
    - Or using Yarn:
      ```bash
      yarn install
      ```

3.  **Run the Frontend Application:**
    - Using npm:
      ```bash
      npm start
      ```
    - Or using Yarn:
      `bash
    yarn start
    `
      The frontend application will open in your browser at `http://localhost:3000`.

---

### 🔐 Environment Configuration

#### Frontend (`frontend/.env.local`)

For local development, the frontend is configured to connect to `http://localhost:8082` by default (see `frontend/src/login.js`). If your backend is hosted elsewhere, you would typically use an `.env.local` file (ignored by Git) to specify the API base URL.

Example `frontend/.env.local`:

```
REACT_APP_API_BASE_URL=http://localhost:8082
```

(Although not explicitly used in the provided `login.js` `axios.defaults.baseURL`, it's a common pattern for production deployments.)

#### Backend (`Springboot/src/main/resources/application.properties`)

The backend configuration is managed directly within `application.properties`.

```properties
spring.application.name=backend
server.port=8082
spring.datasource.url=jdbc:mysql://localhost:3306/springbootdb
spring.datasource.username=root
spring.datasource.password=
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
logging.level.org.springframework=DEBUG
logging.level.org.hibernate.SQL=DEBUG
```

- `server.port`: The port on which the Spring Boot application runs.
- `spring.datasource.*`: Database connection details (URL, username, password, driver).
- `spring.jpa.hibernate.ddl-auto`: Hibernate DDL generation strategy. `update` will update the schema based on entity changes. For production, consider `validate` or `none` and manage schema with migrations.

---

### 📦 Optional Sections

#### Authentication Method

The application implements **JWT (JSON Web Token) based authentication** using Spring Security on the backend.

- When a user logs in via `/api/auth/login`, the backend authenticates credentials and, upon success, generates a JWT containing the user's email, role, and ID. This token is sent back to the frontend.
- On the frontend, this JWT is stored in `localStorage` (`token`, `userRole`, `userId`).
- For all subsequent authenticated requests from the frontend, the JWT is included in the `Authorization` header as a `Bearer` token (e.g., `Authorization: Bearer <your_jwt_token>`).
- The `JwtFilter` on the backend intercepts these requests, validates the token, extracts user details, and sets the `SecurityContextHolder`, allowing Spring Security to enforce role-based access control (e.g., `ROLE_ADMIN`, `ROLE_MEDECIN`, `ROLE_PATIENT`).
- Protected routes on the frontend (`ProtectedRoute.js`) ensure that only users with the correct roles can access specific pages.

#### Testing Strategy

- **Frontend**: The React application includes default testing setup with `react-scripts`. You can run frontend tests using:
  ```bash
  cd frontend
  npm test
  # or yarn test
  ```
  This launches the test runner in interactive watch mode.
- **Backend**: The Spring Boot application includes `spring-boot-starter-test`, which provides JUnit and Mockito for unit and integration testing. A basic test `BackendApplicationTests.java` is present. You can run backend tests using Maven:
  ```bash
  cd Springboot
  ./mvnw test
  # On Windows: mvnw.cmd test
  ```

#### API Documentation

The Spring Boot backend is configured with **SpringDoc OpenAPI UI** (based on Swagger UI). Once the backend is running, you can access the interactive API documentation at:
`http://localhost:8082/swagger-ui.html`
This interface allows you to explore all available endpoints, their expected inputs, and possible responses directly in your browser.

#### Deployment Guide (High-Level)

- **Frontend**: To deploy the React application, build it for production:
  ```bash
  cd frontend
  npm run build
  # or yarn build
  ```
  This creates a `build` folder with optimized static assets, which can then be served by any static file server (e.g., Nginx, Apache, or a CDN).
- **Backend**: To deploy the Spring Boot application, the `mvnw clean install` command generates a `.jar` file in the `Springboot/target/` directory (e.g., `backend-0.0.1-SNAPSHOT.jar`). This executable JAR can be run on any server with a compatible Java Runtime Environment (JRE):
  ```bash
  java -jar backend-0.0.1-SNAPSHOT.jar
  ```
  For production environments, consider using Docker, cloud platforms (AWS, Azure, GCP), or traditional server deployments with process managers (e.g., Systemd, pm2).
