# University Management System (UMS)

UMS is a server-rendered PHP application for managing university rooms, bookings, announcements, important dates, faculty records, feedback, and reports.

## Features

### Administrator

- Sign in and manage the administrator account
- Add, view, and delete faculty records
- Add, edit, delete, and view rooms
- Review, accept, and cancel room-booking requests
- View the timetable and current bookings
- Publish announcements and important dates
- View faculty feedback and submit reports
- Change the administrator password
- Configure notification preferences

### Faculty

- Sign in and access a faculty dashboard
- View available rooms and request room bookings
- View booking status and accepted bookings
- Read announcements and notifications
- Apply for leave
- Submit feedback and view reports
- Change the faculty password

## Technology Stack

- PHP 7.4 or later; PHP 8.0+ is recommended
- MySQL or MariaDB
- Apache or another PHP-capable web server
- MySQLi for database access
- jQuery 3.6.0 loaded from a CDN on some pages
- Lato font loaded from Google Fonts on the login page

The project does not use Composer or another package manager.

## Project Structure

```text
.
|-- index.php                  # Login page
|-- database/
|   `-- projectums.sql         # Database schema and sample data
|-- module/
|   |-- admin/                 # Administrator pages and workflows
|   `-- faculty/               # Faculty pages and workflows
|-- service/
|   |-- AppSettings.php        # Singleton MySQLi connection
|   |-- check.access.php       # Login and role dispatch
|   `-- mysqlcon.php           # Shared MySQLi connection
`-- source/js/
	 `-- loginValidate.js       # Login validation script
```

The `original file` directories contain older copies and experiments. The active pages are the files directly inside `module/admin` and `module/faculty`.

## Requirements

Install the following before running the application:

1. PHP with the MySQLi extension
2. Apache or another web server configured to serve PHP
3. MySQL or MariaDB
4. A modern web browser

On Windows, XAMPP is a convenient way to provide Apache, PHP, and MariaDB together.

## Installation

1. Copy the project into the web server document root. For XAMPP, an example location is:

	```text
	C:\xampp\htdocs\University-Management-System
	```

2. Start Apache and MySQL/MariaDB.

3. Create a database named `projectums`.

4. Import [`database/projectums.sql`](database/projectums.sql) using phpMyAdmin or the MySQL command line. The SQL dump contains the tables and sample data, but it does not create the database itself.

5. Check the database settings in [`service/mysqlcon.php`](service/mysqlcon.php) and [`service/AppSettings.php`](service/AppSettings.php). The default configuration is:

	```text
	Host:     localhost or 127.0.0.1
	User:     root
	Password: empty
	Database: projectums
	```

	Update both files if the local database account uses a password or a different host.

6. Open the application in a browser. For the example XAMPP location, use:

	```text
	http://localhost/University-Management-System/
	```

## Sample Accounts

The imported SQL file includes these sample accounts:

| Role | User ID | Password |
| --- | --- | --- |
| Administrator | `ad-01` | `azaz` |
| Faculty | `IQN` | `asdf` |
| Faculty | `AKR` | `1234` |

Change these passwords before using the application beyond local testing.

## Database

The SQL dump currently defines these tables:

`admin`, `announcement`, `bookings`, `faculty`, `feedback`, `importantdates`, `report`, `request`, `room`, and `users`.

The sample data contains historical dates. Replace or remove the sample records when preparing a fresh demonstration or deployment.

## Known Limitations

- Passwords are stored and compared as plain text. This should be replaced with password hashing before production use.
- Database queries are built directly from request values in several pages. Prepared statements and stronger input validation should be added.
- The application does not currently show comprehensive CSRF protection.
- Some notification and leave workflows refer to tables or columns that are not present in the supplied SQL dump, including `quicknotifications`, `leavetable`, and some notification fields.
- The login form calls `loginValidate()`, but the validation script is not included by the current login page.
- Some legacy or experimental implementations remain under the `original file` directories and are not part of the active navigation.
- Some pages depend on external CDN resources, so those resources require internet access unless they are installed locally.
- The application is intended for local/course use and has not been hardened for production deployment.

- **Md.Asaduzzaman Reyan** - `#2211769042`

