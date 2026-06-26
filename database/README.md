# Database container — Employee Management (MySQL)

This container stores the MySQL schema and demo seed data for the Employee Management system.

## How to connect (required)

Per project convention, connection details are provided at runtime in:

- `db_connection.txt`

It typically contains a ready-to-run mysql CLI command (example format only):
`mysql -u<user> -p<password> <database>`

Use that file to determine:
- username
- password
- database name
- host/port (if needed)

## Apply schema (one statement at a time)

Run the following statements **one at a time** using the mysql CLI.

If your `db_connection.txt` includes host/port, include them in the command you run. Examples below use the pattern:

`mysql ... -e "SQL_STATEMENT"`

### 1) Create table

```bash
mysql ... -e "CREATE TABLE IF NOT EXISTS employees (id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT, first_name VARCHAR(100) NOT NULL, last_name VARCHAR(100) NOT NULL, email VARCHAR(255) NOT NULL, title VARCHAR(150) NULL, department VARCHAR(150) NULL, salary DECIMAL(12,2) NULL, hire_date DATE NULL, active BOOLEAN NOT NULL DEFAULT TRUE, created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP, PRIMARY KEY (id), UNIQUE KEY uk_employees_email (email), KEY idx_employees_last_first (last_name, first_name), KEY idx_employees_department (department), KEY idx_employees_active (active)) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;"
```

## Seed minimal demo data (one INSERT per row)

```bash
mysql ... -e "INSERT INTO employees (first_name, last_name, email, title, department, salary, hire_date, active) VALUES ('Ava', 'Patel', 'ava.patel@example.com', 'Software Engineer', 'Engineering', 115000.00, '2024-02-12', TRUE);"
mysql ... -e "INSERT INTO employees (first_name, last_name, email, title, department, salary, hire_date, active) VALUES ('Noah', 'Kim', 'noah.kim@example.com', 'QA Engineer', 'Engineering', 95000.00, '2023-08-01', TRUE);"
mysql ... -e "INSERT INTO employees (first_name, last_name, email, title, department, salary, hire_date, active) VALUES ('Mia', 'Garcia', 'mia.garcia@example.com', 'HR Manager', 'People Ops', 105000.00, '2022-05-20', TRUE);"
```

Note: re-running seed inserts will fail due to the unique email constraint. If you need to re-seed, delete rows first.

## Verification commands

```bash
mysql ... -e "SHOW TABLES LIKE 'employees';"
mysql ... -e "DESCRIBE employees;"
mysql ... -e "SELECT id, first_name, last_name, email, department, active, created_at FROM employees ORDER BY id;"
mysql ... -e "SELECT COUNT(*) AS employee_count FROM employees;"
```

## Minimal CRUD smoke checks (optional)

```bash
# Create
mysql ... -e "INSERT INTO employees (first_name, last_name, email) VALUES ('Test', 'User', 'test.user@example.com');"

# Read
mysql ... -e "SELECT * FROM employees WHERE email='test.user@example.com';"

# Update
mysql ... -e "UPDATE employees SET department='IT', title='Support' WHERE email='test.user@example.com';"

# Delete
mysql ... -e "DELETE FROM employees WHERE email='test.user@example.com';"
```
