# Employee management schema + seed (reference)

This file is a **reference** for the SQL used by this project.
Per project rules, execute statements **one line at a time** with `mysql -e "..."`.

## Schema

```sql
CREATE TABLE IF NOT EXISTS employees (
  id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  email VARCHAR(255) NOT NULL,
  title VARCHAR(150) NULL,
  department VARCHAR(150) NULL,
  salary DECIMAL(12,2) NULL,
  hire_date DATE NULL,
  active BOOLEAN NOT NULL DEFAULT TRUE,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (id),
  UNIQUE KEY uk_employees_email (email),
  KEY idx_employees_last_first (last_name, first_name),
  KEY idx_employees_department (department),
  KEY idx_employees_active (active)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

## Seed data

```sql
INSERT INTO employees (first_name, last_name, email, title, department, salary, hire_date, active)
VALUES ('Ava', 'Patel', 'ava.patel@example.com', 'Software Engineer', 'Engineering', 115000.00, '2024-02-12', TRUE);

INSERT INTO employees (first_name, last_name, email, title, department, salary, hire_date, active)
VALUES ('Noah', 'Kim', 'noah.kim@example.com', 'QA Engineer', 'Engineering', 95000.00, '2023-08-01', TRUE);

INSERT INTO employees (first_name, last_name, email, title, department, salary, hire_date, active)
VALUES ('Mia', 'Garcia', 'mia.garcia@example.com', 'HR Manager', 'People Ops', 105000.00, '2022-05-20', TRUE);
```
