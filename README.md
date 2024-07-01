  # # Online Bookstore System Documentation

## Prerequisites

Before starting the project, ensure you have the following installed:

1. **Docker** (to run PostgreSQL)
2. **Node.js** (at least version 12)
3. **TypeScript** (globally installed)
4. **pg (node-postgres)** library for PostgreSQL interaction

You can install these prerequisites using the following commands:

```bash
# Install Docker
# For Ubuntu
sudo apt update
sudo apt install docker.io
```

# For macOS

```
brew install --cask docker
```

# For Ubuntu
```
sudo apt update
sudo apt install nodejs npm
```

# For macOS

```
brew install node
```

# Install TypeScript globally

```
npm install -g typescript
```

# Install pg library for PostgreSQL interaction

```
npm install pg
```

## Setting Up PostgreSQL with Docker and pgAdmin

Before creating the database, ensure you have PostgreSQL and pgAdmin running in Docker containers. Use the following steps to set up PostgreSQL and pgAdmin with Docker:

To check if you have docker installed, run the following:

```
docker
```

For details on this, please visit the official docker documentation(https://docs.docker.com/engine/install/)

1.Download the zip file from the git repo and then extract it 
2.cd into extract folder

```bash
cd postgres-with-pgadmin
```

3.then run command

```bash
docker-compose up -d --build
```

4.Now you can visit pgAdmin4 at your LocalHost(local)

When you are done, be sure to shut down the services with:

```
bash
docker-compose down
```

This setup will allow you to manage your PostgreSQL instance using pgAdmin.

For more information, you can visit the [Conestoga GitLab page](https://gitlab.com/conestogac).

# # Table of Contents

1. [Project Overview](#project-overview)
2. [Duties Assigned to Individual Members](#duties-assigned-to-individual-members)
3. [Database Tables and Attributes](#database-tables-and-attributes)
    - [Authors](#authors)
    - [Publishers](#publishers)
    - [Genres](#genres)
    - [Books](#books)
    - [Customers](#customers)
    - [Orders](#orders)
    - [Sales](#sales)
    - [Reviews](#reviews)
4. [SQL Code to Create the Database](#sql-code-to-create-the-database)
5. [Sample Data Insertion](#sample-data-insertion)
6. [DDL/DML for Authors Table](#ddldml-for-authors-table)
7. [SQL Queries for Requirements](#sql-queries-for-requirements)
8. [TypeScript Interface and Implementation](#typescript-interface-and-implementation)
9. [Explanation of the TypeScript Interface and Implementation](#explanation-of-the-typescript-interface-and-implementation)

## Project Overview
Welcome to the Online Bookstore System project! This project involves designing a comprehensive database system for an online bookstore that sells physical books, e-books, and audiobooks. The system allows customers to browse the catalog, make purchases, and leave reviews. Authors and publishers are also integrated into the system.

## Duties Assigned to Individual Members
 _note -- (SID = Student ID)_
- **Database Design**: Dhrumilbhai Dhameliya --> SID - 
- **SQL Queries**: Muzammil Shaikh --> SID - 8969614
- **TypeScript Interface**: Dharmesh Vanani --> ID - 8952848
