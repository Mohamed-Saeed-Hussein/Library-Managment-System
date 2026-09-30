# Library Management System

**A Java desktop workspace for books, members, and lending.**

A Swing application that connects everyday library operations to a MySQL database: maintain the catalog, register users, rent and return books, and inspect statistics.

`Java / Swing` · `MySQL` · `JDBC` · `NetBeans / Ant`

[Features](#features) · [Local setup](#local-setup) · [Code map](#code-map)

This repository is a fork of [Kaytbay/Library-Managment-System](https://github.com/Kaytbay/Library-Managment-System). Credit belongs to the upstream project and its contributors.

---

## Features

| Workspace | Relevant screens |
| :--- | :--- |
| Accounts | Login, signup, and password recovery |
| Catalog | Add books and update quantities |
| Members | Add library users |
| Circulation | Rent, return, and sell books |
| Reporting | Statistics screen |

The application is organized around separate Swing forms, with JDBC queries connecting the UI to the database.

## Local setup

This is a NetBeans/Ant project. Its checked-in configuration targets **JDK 23 with preview enabled**; the SQL dumps were exported from **MySQL 8.0.40**.

### 1. Prepare a local database

Create an empty development database named `librarynew`, then import these scripts into it:

- [Accounts](librarynew_account.sql)
- [Books](librarynew_books.sql)
- [Rentals](librarynew_rental.sql)
- [Users](librarynew_users.sql)

The dump scripts include `DROP TABLE` statements. Use an empty local database rather than importing them over existing data.

### 2. Configure the connection

Review [src/javaconnect.java](src/javaconnect.java). It currently connects to a local `librarynew` database with hard-coded development credentials. Adjust the connection for your own local MySQL account.

### 3. Open and repair project references

Open the repository in NetBeans and check **Project Properties → Libraries** and the selected Java platform.

| Dependency | Included location |
| :--- | :--- |
| MySQL Connector/J | `dist/lib/mysql-connector-j-8.2.0.jar` |
| jBCrypt | `dist/lib/jBCrypt-0.4.jar` |
| JCalendar | `dist/lib/jcalendar-1.4.jar` |
| NetBeans AbsoluteLayout | `dist/lib/AbsoluteLayout.jar` |

[nbproject/project.properties](nbproject/project.properties) contains machine-specific Windows paths and unresolved merge-conflict markers. Resolve those entries and point the libraries to valid local files before building. Any remaining named NetBeans library references also need to be configured in the IDE.

### 4. Build and launch

Use NetBeans **Clean and Build**, then **Run**. The configured entry point is `Login`.

Once the project references are repaired, the corresponding Ant commands are:

```bash
ant clean jar
ant run
```

These are setup instructions, not a claim that the current checkout builds without the repairs above.

## Code map

| Location | Responsibility |
| :--- | :--- |
| [Login.java](src/Login.java), [Signup.java](src/Signup.java), [Forgot.java](src/Forgot.java) | Account screens |
| [Home.java](src/Home.java) | Main navigation |
| [NewBook.java](src/NewBook.java), [UpdateQuantityForm.java](src/UpdateQuantityForm.java) | Catalog management |
| [RentBook.java](src/RentBook.java), [ReturnBook.java](src/ReturnBook.java), [SellBook.java](src/SellBook.java) | Book transactions |
| [Statistics.java](src/Statistics.java) | Reporting |
| [javaconnect.java](src/javaconnect.java) | Database connection |
| [build.xml](build.xml) | Ant build entry point |

## Project material

[Original presentation](Library%20Management%20System%20%281%29.pptx) · [Source files](src) · [Bundled dependencies](dist/lib)
