# Database Setup and Configuration

This guide covers the MariaDB setup and configuration steps required for the EasyCRUD project.

## 1. Install MariaDB

### On Ubuntu/Linux
```bash
sudo apt update
sudo apt install mariadb-server -y
```

### On Windows
Download and install MariaDB from the official website:
https://mariadb.org/download/

## 2. Secure MariaDB

Run the secure installation utility:
```bash
sudo mysql_secure_installation
```

Then follow the prompts to:
- Set the MariaDB root password
- Remove anonymous users
- Disable remote root login
- Remove the test database
- Reload privilege tables

## 3. Create the Database and User

Open the MariaDB shell:
```bash
mysql -u root -p
```

Then run:
```sql
CREATE DATABASE student_db;
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON student_db.* TO 'app_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Replace `app_user` and `your_password` with your own credentials.

## 4. Configure Backend Connection

Use these values in the backend configuration file `backend/src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/student_db
spring.datasource.username=app_user
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

## 5. Optional: Create a Sample Table

If you need an explicit table structure, run this after selecting the database:

```sql
USE student_db;
CREATE TABLE students (
  id BIGINT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255),
  email VARCHAR(255),
  course VARCHAR(255),
  student_class VARCHAR(255),
  percentage DOUBLE,
  branch VARCHAR(255),
  mobile_number VARCHAR(255),
  PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 6. Database Credentials Summary

- DB_HOST: `localhost`
- DB_PORT: `3306`
- DB_NAME: `student_db`
- DB_USER: `app_user`
- DB_PASSWORD: `your_password`

## 7. Test the Connection

Start the backend application and confirm it connects successfully to MariaDB. If there are connection issues, verify the credentials and database URL in `application.properties`.
