# Pharmacy-Management (PHP + MySQL)

Simple pharmacy management web app (PHP + MySQL) that provides inventory, purchase, sales, invoice and reporting features. UI uses Bootstrap. Data model and seed are in `pharmacy.sql`.

## Quick summary
- Server: Apache (XAMPP / WAMP / LAMP)
- Language: PHP (mysqli)
- Database: MySQL (database name: `pharmacy` by default)
- Frontend: HTML, Bootstrap, JS

## Prerequisites
1. Apache + PHP (PHP >= 7 recommended) and MySQL / MariaDB. Use XAMPP/WAMP on Windows or LAMP on Linux.
2. Enable mysqli extension in PHP.
3. Place project inside your web server document root (e.g. XAMPP `htdocs`).

## Files you will use
- Project root web entry pages: [index.html](index.html), [index.php](index.php), [login.php](login.php)
- DB connection: [php/db_connection.php](php/db_connection.php)
- Database dump: [pharmacy.sql](pharmacy.sql)
- Setup/validation logic: [php/validateCredentials.php](php/validateCredentials.php)
- Main header helper: [php/header.php](php/header.php) — symbol: [`php.createHeader`](php/header.php)
- Invoice logic: [php/add_new_invoice.php](php/add_new_invoice.php) and [`js/add_new_invoice.js`](js/add_new_invoice.js)
- Suggestion/autocomplete: [js/suggestions.js](js/suggestions.js)
- Frontend login/setup scripts: [js/index.js](js/index.js)

## Step-by-step setup

1. Copy project to web root
   - Example (XAMPP): copy the `Pharmacy-Management` folder to `C:\xampp\htdocs\` so the path is `C:\xampp\htdocs\Pharmacy-Management`.

2. Start server
   - Start Apache and MySQL (via XAMPP/WAMP control panel).

3. Create database and import schema
   - Option A — phpMyAdmin:
     - Open phpMyAdmin -> create database `pharmacy` -> Import -> choose `pharmacy.sql` -> Execute.
   - Option B — MySQL CLI:
     - Open a terminal and run:
       ```sh
       mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS pharmacy;"
       mysql -u root -p pharmacy < /path/to/Pharmacy-Management/pharmacy.sql
       ```

4. Configure DB credentials (if different)
   - Edit [php/db_connection.php](php/db_connection.php) and update `$SERVER`, `$USERNAME`, `$PASSWORD`, `$DB` if your MySQL user or DB differs.

5. Run the web app (one-time setup)
   - Open browser:
     - Setup page: http://localhost/Pharmacy-Management/index.html — completes initial admin setup (JS: [js/index.js](js/index.js), server: [php/validateCredentials.php](php/validateCredentials.php)).
     - After setup use: http://localhost/Pharmacy-Management/index.php or [login.php](login.php).

6. First login / admin
   - The setup flow stores admin info (see [`php.isSetupDone`](php/validateCredentials.php) and [`php.isAdmin`](php/validateCredentials.php)).
   - If login fails, check DB user records in `admin_credentials` table (imported from `pharmacy.sql` or created during setup).

## Common commands / tips
- If database connection fails, [php/db_connection.php](php/db_connection.php) will show:
  > "Oops, Unable to connect with database!"
  - Verify MySQL is running and credentials in `php/db_connection.php` are correct.
- To reset DB, drop & recreate `pharmacy` and re-import `pharmacy.sql`.
- If a page returns blank/500, check Apache/PHP error log (XAMPP: `apache/logs/error.log`).

## Important code entry points (symbols)
- [`php.createHeader`](php/header.php) — builds page header.
- [`php.isSetupDone`](php/validateCredentials.php) — checks initial setup state.
- [`php.isAdmin`](php/validateCredentials.php) — login validation/update login flag.
- [`php.getInvoiceNumber`](php/add_new_invoice.php) — current invoice number helper.
- [`js.addInvoice`](js/add_new_invoice.js) — client-side add invoice flow.

## Troubleshooting notes
- Character set: SQL uses utf16 fields; if your MySQL import fails due to charset, import with default charset or adjust DB/SQL charsets in phpMyAdmin.
- Ensure browser can reach `http://localhost/Pharmacy-Management/`.
- If JavaScript features (autocomplete, invoice row add) do not work, open browser console to see errors and confirm JS files are loaded (look at page source and network tab).

---

## Installation

Prerequisites
- Windows with XAMPP or WAMP (Apache + PHP + MySQL)
- PHP 7.x or newer with mysqli enabled
- Web browser

Step-by-step install (Windows / XAMPP)

1. Copy project to web root  
   - Using File Explorer: copy `Pharmacy-Management` into `C:\xampp\htdocs\`  
   - Or PowerShell:
     ```powershell
     xcopy /E /I "C:\Users\Vivek\Downloads\Pharmacy-Management" "C:\xampp\htdocs\Pharmacy-Management"
     ```

2. Start services  
   - Open XAMPP Control Panel (C:\xampp\xampp-control.exe) and start Apache and MySQL.

3. Create and import the database  
   - Using phpMyAdmin:
     - Open http://localhost/phpmyadmin
     - Create database named `pharmacy`
     - Import `C:\xampp\htdocs\Pharmacy-Management\pharmacy.sql`
   - Or using MySQL CLI (XAMPP):
     ```cmd
     "C:\xampp\mysql\bin\mysql.exe" -u root -p -e "CREATE DATABASE IF NOT EXISTS pharmacy;"
     "C:\xampp\mysql\bin\mysql.exe" -u root -p pharmacy < "C:\xampp\htdocs\Pharmacy-Management\pharmacy.sql"
     ```
   - If you use a different MySQL user, substitute username and password accordingly.

4. Configure DB credentials (if needed)  
   - Open `php\db_connection.php` and set:
     - $SERVER (usually `localhost`)
     - $USERNAME (e.g., `root`)
     - $PASSWORD
     - $DB (`pharmacy`)

5. Open the app in a browser  
   - Initial setup / admin creation: http://localhost/Pharmacy-Management/index.html  
   - Login / main app: http://localhost/Pharmacy-Management/index.php or http://localhost/Pharmacy-Management/login.php

6. Verify basic flow  
   - Add a sample product, record a sale, and generate an invoice.

Troubleshooting
- DB connection fails: ensure MySQL is running and credentials in `php/db_connection.php` are correct.  
- mysqli missing: enable `extension=mysqli` in `php.ini` and restart Apache.  
- Blank page / server error: check Apache error log: `C:\xampp\apache\logs\error.log`.  
- JavaScript features not working: open browser DevTools Console and Network tab for errors or missing files.

Optional
- To reset, drop and recreate `pharmacy` and re-import `pharmacy.sql`.
- Secure before production: use prepared statements, validate/sanitize input, secure config files.
