# أمومه كلينك - نظام حجز المواعيد (Omoma Clinic - Appointment Reservation System)

## Description

This project is a web-based clinic appointment reservation system designed for "أمومه كلينك" (Omoma Clinic). It allows patients to register, log in, book, view, edit, and cancel their appointments. The system also provides an interface for clinic administrators and receptionists to manage appointments and patient information.

**Key Objectives:**
- Streamline the appointment booking process for patients.
- Provide patients with a convenient way to manage their appointments online.
- Offer clinic staff tools to manage schedules and patient bookings efficiently.
- Enhance the overall patient experience and clinic operational efficiency.

**Target Users:**
- **Patients:** Individuals seeking to book and manage appointments at Omoma Clinic.
- **Clinic Administrators:** Staff responsible for overall system management, user management, and overseeing clinic operations.
- **Receptionists:** Staff responsible for managing daily appointments, patient check-ins, and assisting patients with bookings.

## Features

**Patient-Facing:**
-   **User Registration & Login:** Patients can create accounts and log in securely.
-   **Password Management:** Initial default password (year of birth) with a prompt for a mandatory password change (`force_password_reset`).
-   **Dashboard:** Central hub for patients to access services.
-   **Appointment Booking:**
    -   Book In-Clinic Appointments (`patient/in_clinic_booking.php`).
    -   Book Online Consultations (via `patient/online_consultation_booking.php` linked from dashboard).
    -   Dynamic fetching of available time slots based on selected date (`core/ajax_get_slots.php`).
-   **My Appointments:** View a list of past and upcoming appointments (`patient/my_appointments.php`).
-   **Edit Appointments:** Modify details of existing, active appointments (`patient/edit_appointment.php`).
-   **Cancel Appointments:** Cancel upcoming appointments (`patient/cancel_patient_appointment.php`).
-   **Profile Management:** (Assumed via `patient/profile.php` link).
-   **Responsive Design:** User-friendly interface on various devices (using Bootstrap).
-   **Arabic Language Support:** Interface and messages primarily in Arabic.

**Admin/Receptionist-Facing (Inferred):**
-   **Secure Login:** Separate login for staff (`login.php`).
-   **Role-Based Access:** Different dashboards and functionalities for 'admin' and 'receptionist' roles (`process_login.php`).
-   **Dashboard:** Dedicated dashboards for admin (`admin/dashboard.php`) and receptionists (`receptionist/dashboard.php`).
-   **Patient Search:** Ability for admin to search for patients by phone number (`core/ajax_search_patient.php`).
-   **View Appointment Details:** Admin can retrieve detailed information about specific appointments (`core/ajax_get_appointment_details.php`).
-   **(Potential Features - not fully detailed in provided files but common for such systems):**
    -   Manual appointment booking/editing/cancellation for patients.
    -   Management of doctor schedules and blocked time slots.
    -   Patient record management.
    -   Reporting and analytics.

**General:**
-   **Landing Page:** Informative homepage (`index.php`) showcasing clinic services, doctor information, and contact details.
-   **Dynamic Content:** Site content (titles, descriptions, services) largely configurable within `index.php`.
-   **SEO & Social Media Meta Tags:** Basic meta tags for search engine optimization and social sharing included in `index.php`.

## Table of Contents

- Installation
- Usage
- Configuration
- File Structure Highlights
- Contributing
- License
- Acknowledgements

## Installation

Follow these steps to set up the project locally or on a server.

**Prerequisites:**
-   A web server (e.g., Apache, Nginx). XAMPP or WAMP for local development is suitable.
-   PHP (version 7.0 or higher recommended, given the syntax used).
-   MySQL or MariaDB database server.
-   A web browser.

**Steps:**

1.  **Clone the Repository (or Download Files):**
    ```bash
    # If using Git
    git clone https://github.com/mostafaalameer/clinic_reservation_system.git
    cd clinic_reservation_system
    ```
    Alternatively, download the project files and extract them.

2.  **Place Project Files:**
    Copy the entire project folder (e.g., `clinic_reservation_system`) into your web server's document root (e.g., `htdocs` for XAMPP, `www` for WAMP).

3.  **Database Setup:**
    *   Create a new MySQL database. You can use a tool like phpMyAdmin. The default database name used in `core/config.php` is `if0_39216848_clinic_db`, but you can change this.
    *   **Important:** You will need to create the necessary tables for the system to function (e.g., `patients`, `appointments`, `users`, `doctor_schedule`, `blocked_periods`). It's recommended to have a `.sql` file with the database schema. If one is not present, you'll need to create it based on the queries in the PHP files.

4.  **Configure the Application:**
    *   Navigate to the `core/` directory.
    *   Rename or copy `config.php.example` to `config.php` (if an example file is provided, otherwise edit `config.php` directly).
    *   Open `core/config.php` and update the following constants:
        *   **Database Credentials:**
            ```php
            define('DB_SERVER', 'your_db_host'); // e.g., 'localhost'
            define('DB_USERNAME', 'your_db_username'); // e.g., 'root'
            define('DB_PASSWORD', 'your_db_password'); // e.g., '' for default XAMPP
            define('DB_NAME', 'your_db_name'); // e.g., 'if0_39216848_clinic_db' or your chosen name
            ```
        *   **Base URL:**
            ```php
            define('BASE_URL', 'http://localhost/clinic_reservation_system/'); // Adjust if your project is in a subfolder or on a live domain
            // Example from your config: define('BASE_URL', 'https://omoma.fwh.is/');
            ```
        *   **SMS API (Optional):** If you plan to use SMS notifications, update these:
            ```php
            define('SMS_API_KEY', 'YOUR_SMS_API_KEY');
            define('SMS_API_SENDER_ID', 'YourClinic');
            define('SMS_API_URL', 'https://api.smsprovider.com/send');
            ```
        *   **Timezone:**
            ```php
            date_default_timezone_set('Asia/Riyadh'); // Set to your clinic's timezone
            ```

5.  **Access the Application:**
    Open your web browser and navigate to the `BASE_URL` you configured (e.g., `http://localhost/clinic_reservation_system/`).

## Usage

### Patients

1.  **Registration:**
    *   Navigate to `BASE_URL/patient/login.php`.
    *   Click on "Create an account" (or the Arabic equivalent).
    *   Fill in the registration form (Name, Phone, Email, DOB, Gender).
    *   The default password will be the patient's **year of birth** (e.g., if DOB is 1990-05-15, password is `1990`).
2.  **Login:**
    *   Go to `BASE_URL/patient/login.php`.
    *   Enter your registered phone number and password.
    *   Upon first login, you will be prompted to change your password if `force_password_reset` is active.
3.  **Dashboard (`BASE_URL/patient/dashboard.php`):**
    *   After login, you'll be redirected here.
    *   Choose to book an "In-Clinic Appointment" or "Online Consultation".
4.  **Booking an Appointment:**
    *   Select appointment type, date, and an available time slot.
    *   Add optional notes.
    *   Confirm booking.
5.  **Managing Appointments (`BASE_URL/patient/my_appointments.php`):**
    *   View a list of all your appointments.
    *   Edit details of upcoming appointments (date, time, type, notes).
    *   Cancel upcoming appointments.

### Admin / Receptionist

1.  **Login:**
    *   Navigate to `BASE_URL/login.php` (the login page at the root of the project).
    *   Enter your assigned username and password.
2.  **Dashboard:**
    *   Based on your role (admin or receptionist), you will be redirected to your respective dashboard:
        *   Admin: `BASE_URL/admin/dashboard.php`
        *   Receptionist: `BASE_URL/receptionist/dashboard.php`
3.  **Functionality (Examples):**
    *   Admins can search for patients.
    *   Admins can view detailed appointment information.
    *   (Other functionalities depend on the implementation of the admin/receptionist panels).

## Configuration

The main configuration file for the application is `core/config.php`. Key settings include:

-   `DB_SERVER`, `DB_USERNAME`, `DB_PASSWORD`, `DB_NAME`: Database connection details.
-   `BASE_URL`: The root URL of your application. **Crucial for all links and redirects to work correctly.**
-   `SMS_API_KEY`, `SMS_API_SENDER_ID`, `SMS_API_URL`: For SMS notification integration (if implemented).
-   `date_default_timezone_set()`: Sets the default timezone for date/time functions.

Content for the public landing page (`index.php`) such as clinic name, hero text, service descriptions, and contact information can be directly edited within the PHP variables at the top of `index.php`.

## File Structure Highlights

