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

## Database Tables and Attributes

### Explanation

The database is structured into several tables to represent different entities within the online bookstore. Each table captures essential information about the entity it represents. This design ensures data integrity and supports efficient queries and transactions.


### Authors
| Attribute   | Type          |
|-------------|---------------|
| author_id   | INT PRIMARY KEY |
| name        | VARCHAR(255)  |
| bio         | TEXT          |
| total_books | INT           |

### Publishers
| Attribute     | Type          |
|---------------|---------------|
| publisher_id  | INT PRIMARY KEY |
| name          | VARCHAR(255)  |
| address       | VARCHAR(255)  |

### Genres
| Attribute   | Type            |
|-------------|-----------------|
| genre_id    | INT PRIMARY KEY |
| genre_name  | VARCHAR(100)    |

### Books
| Attribute       | Type            |
|-----------------|-----------------|
| book_id         | INT PRIMARY KEY |
| title           | VARCHAR(255)    |
| genre_id        | INT             |
| price           | DECIMAL(10,2)   |
| format          | VARCHAR(20)     |
| author_id       | INT             |
| publisher_id    | INT             |
| published_date  | DATE            |
| stock_quantity  | INT             |

### Customers
| Attribute      | Type            |
|----------------|-----------------|
| customer_id    | INT PRIMARY KEY |
| name           | VARCHAR(255)    |
| email          | VARCHAR(255)    |
| total_spent    | DECIMAL(10,2)   |
| join_date      | DATE            |

### Orders
| Attribute     | Type            |
|---------------|-----------------|
| order_id      | INT PRIMARY KEY |
| customer_id   | INT             |
| order_date    | DATE            |
| total_amount  | DECIMAL(10,2)   |

### Sales
| Attribute    | Type            |
|--------------|-----------------|
| sale_id      | INT PRIMARY KEY |
| order_id     | INT             |
| book_id      | INT             |
| quantity     | INT             |
| sale_price   | DECIMAL(10,2)   |

### Reviews
| Attribute     | Type            |
|---------------|-----------------|
| review_id     | INT PRIMARY KEY |
| book_id       | INT             |
| customer_id   | INT             |
| rating        | INT             |
| review_text   | TEXT            |
| review_date   | DATE            |

## SQL Code to Create the Database

The SQL code below creates the necessary tables for the online bookstore database. Each table is defined with its attributes and data types.


```sql
CREATE TABLE Authors (
    author_id INT PRIMARY KEY,
    name VARCHAR(255),
    bio TEXT,
    total_books INT
);

CREATE TABLE Publishers (
    publisher_id INT PRIMARY KEY,
    name VARCHAR(255),
    address VARCHAR(255)
);

CREATE TABLE Genres (
    genre_id INT PRIMARY KEY,
    genre_name VARCHAR(100)
);

CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(255),
    genre_id INT,
    price DECIMAL(10,2),
    format VARCHAR(20),
    author_id INT,
    publisher_id INT,
    published_date DATE,
    stock_quantity INT,
    FOREIGN KEY (genre_id) REFERENCES Genres(genre_id),
    FOREIGN KEY (author_id) REFERENCES Authors(author_id),
    FOREIGN KEY (publisher_id) REFERENCES Publishers(publisher_id)
);

CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255),
    total_spent DECIMAL(10,2),
    join_date DATE
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);

CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    order_id INT,
    book_id INT,
    quantity INT,
    sale_price DECIMAL(10,2),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (book_id) REFERENCES Books(book_id)
);

CREATE TABLE Reviews (
    review_id INT PRIMARY KEY,
    book_id INT,
    customer_id INT,
    rating INT,
    review_text TEXT,
    review_date DATE,
    FOREIGN KEY (book_id) REFERENCES Books(book_id),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```
 
 # Sample Data Insertion
Some sample data insertion for the Database :

```markdown
```sql
INSERT INTO Authors (author_id, name, bio, total_books) VALUES
(1, 'Dharmesh', 'Biography of Author One', 10),
(2, 'Muz', 'Biography of Author Two', 15),
(3, 'Dhrumil', 'Biography of Author Three', 5);

INSERT INTO Genres (genre_id, genre_name) VALUES
(1, 'Fiction'),
(2, 'Non-Fiction'),
(3, 'Science Fiction');

INSERT INTO Publishers (publisher_id, name, address) VALUES
(1, 'Penguin Random House', '123 Publisher St.'),
(2, 'HarperCollins', '456 Publisher Ave.'),
(3, 'Simon & Schuster', '789 Publisher Blvd.');

INSERT INTO Books (book_id, title, genre_id, price, format, author_id, publisher_id, published_date, stock_quantity) VALUES
(1, 'Sample Book', 1, 19.99, 'physical', 1, 1, '2024-01-01', 100);

INSERT INTO Books (book_id, title, genre_id, price, format, author_id, publisher_id, published_date, stock_quantity) VALUES 
(2, 'Advanced Databases', 2, 29.99, 'ebook', 2, 2, '2023-03-15', 150),
(3, 'Intro to SQL', 3, 25.99, 'audiobook', 3, 3, '2022-11-20', 120),
(4, 'NoSQL Databases', 1, 35.50, 'physical', 1, 1, '2023-07-05', 90),
(5, 'Data Modeling', 2, 18.75, 'ebook', 2, 2, '2021-08-17', 60),
(6, 'Database Optimization', 3, 22.40, 'physical', 3, 3, '2024-02-14', 110),
(7, 'Relational Databases', 1, 28.80, 'audiobook', 1, 1, '2020-12-10', 80),
(8, 'SQL for Beginners', 2, 15.00, 'ebook', 2, 2, '2022-04-22', 140),
(9, 'Mastering SQL', 3, 40.00, 'physical', 3, 3, '2023-01-30', 130),
(10, 'Database Security', 1, 50.99, 'ebook', 1, 1, '2021-05-12', 70),
(11, 'Big Data and Databases', 2, 60.00, 'audiobook', 2, 2, '2020-09-03', 95),
(12, 'Cloud Databases', 3, 35.25, 'physical', 3, 3, '2024-06-28', 200),
(13, 'Data Warehousing', 1, 55.45, 'ebook', 1, 1, '2021-07-19', 75);

INSERT INTO Customers (customer_id, name, email, total_spent, join_date) VALUES
(1, 'Alice', 'alice@example.com', 200.50, '2022-01-01'),
(2, 'Bob', 'bob@example.com', 350.75, '2021-05-15'),
(3, 'Charlie', 'charlie@example.com', 120.00, '2023-03-20');

INSERT INTO Orders (order_id, customer_id, order_date, total_amount) VALUES
(1, 1, '2023-06-01', 50.75),
(2, 2, '2023-07-15', 120.50),
(3, 3, '2023-08-20', 75.25);

INSERT INTO Sales (sale_id, order_id, book_id, quantity, sale_price) VALUES
(1, 1, 1, 1, 19.99),
(2, 2, 2, 2, 59.98),
(3, 3, 3, 1, 25.99);

INSERT INTO Reviews (review_id, book_id, customer_id, rating, review_text, review_date) VALUES
(1, 1, 1, 5, 'Great book!', '2023-01-01'),
(2, 2, 2, 4, 'Very informative.', '2023-02-15'),
(3, 3, 3, 3, 'Average read.', '2023-03-20');
```

# DDL/DML for Authors Table

CRUD operations for the Authors table:

The following SQL code demonstrates how to perform Create, Read, Update, and Delete (CRUD) operations on the Authors table.


```markdown

```sql
-- Create Authors Table
CREATE TABLE Authors (
    author_id INT PRIMARY KEY,
    name VARCHAR(255),
    bio TEXT,
    total_books INT
);

-- Insert into Authors Table
INSERT INTO Authors (author_id, name, bio, total_books) VALUES
(1, 'Dharmesh', 'Biography of Author One', 10),
(2, 'Muz', 'Biography of Author Two', 15),
(3, 'Dhrumil', 'Biography of Author Three', 5);

-- Read from Authors Table
SELECT * FROM Authors WHERE author_id = 3;

-- Update Authors Table
UPDATE Authors SET total_books = 9 WHERE author_id = 4;

-- Delete from Authors Table
DELETE FROM Authors WHERE author_id = 4;

-- Read all records from Authors Table
SELECT * FROM Authors;
```

# SQL Queries for Requirements

The following SQL queries fulfill the specific requirements provided by the bookstore.


```markdown

```sql
-- Power Writers
SELECT Authors.author_id, Authors.name, Genres.genre_name,
       COUNT(Books.book_id) AS book_count
FROM Books
JOIN Authors ON Books.author_id = Authors.author_id
JOIN Genres ON Books.genre_id = Genres.genre_id
WHERE Books.published_date >= CURRENT_DATE - INTERVAL '2 year'
GROUP BY Authors.author_id, Authors.name, Genres.genre_name
HAVING COUNT(Books.book_id) > 2;

-- Loyal Customers
SELECT Customers.customer_id, Customers.name AS customer_name,
       SUM(Orders.total_amount) AS total_spent_last_year
FROM Customers
JOIN Orders ON Customers.customer_id = Orders.customer_id
WHERE Orders.order_date >= CURRENT_DATE - INTERVAL '1 year'
GROUP BY Customers.customer_id, Customers.name
HAVING SUM(Orders.total_amount) > 50;

-- Well Reviewed Books
SELECT Books.book_id, Books.title, AVG(Reviews.rating) AS average_rating
FROM Books
JOIN Reviews ON Books.book_id = Reviews.book_id
GROUP BY Books.book_id, Books.title
HAVING AVG(Reviews.rating) > (SELECT AVG(rating) FROM Reviews);

-- Most Popular Genre by Sales
SELECT Genres.genre_name, SUM(Sales.quantity) AS total_sales
FROM Genres
JOIN Books ON Genres.genre_id = Books.genre_id
JOIN Sales ON Books.book_id = Sales.book_id
GROUP BY Genres.genre_name
ORDER BY total_sales DESC
LIMIT 1;

-- 10 Most Recent Reviews
SELECT Reviews.review_id, Reviews.book_id, Reviews.customer_id, Reviews.rating, Reviews.review_text, Reviews.review_date
FROM Reviews
ORDER BY Reviews.review_date DESC
LIMIT 10;
```
# TypeScript Interface and Implementation

The TypeScript interface and implementation are designed to interact with the database and perform CRUD operations on the Books table. This ensures that the application can create, read, update, and delete book records as required.

## Before starting typescript run the following to make dir and config files


mkdir bookstore
cd bookstore
npm init -y
Sec3: npm install typescript --save-dev
npm install ts-node --save-dev
npx tsc --init
touch src/interfaces/Book.ts


```
typescript
import { Pool, QueryResult } from 'pg';

// Database configuration
const pool = new Pool({
  user: 'postgres', // Replace with your PostgreSQL username
  host: 'localhost',
  database: 'postgres', // Replace with your PostgreSQL database name
  password: 'password', // Replace with your PostgreSQL password
  port: 5432,
});

// Interfaces for database entities
interface Book {
  book_id: number;
  title: string;
  genre_id: number;
  price: number;
  format: string;
  author_id: number;
  publisher_id: number;
  published_date: Date;
  stock_quantity: number;
}

interface CreateBookDTO {
  title: string;
  genre_id: number;
  price: number;
  format: string;
  author_id: number;
  publisher_id: number;
  published_date: Date;
  stock_quantity: number;
}

// BookRepository class
class BookRepository {
  private pool: Pool;

  constructor(pool: Pool) {
    this.pool = pool;
  }

  async createBook(book: CreateBookDTO): Promise<Book> {
    const query = `
      INSERT INTO Books (title, genre_id, price, format, author_id, publisher_id, published_date, stock_quantity)
      VALUES ($1, $2, $3, $4, $5, $6, $7, $8)
      RETURNING *
    `;
    const values = [
      book.title,
      book.genre_id,
      book.price,
      book.format,
      book.author_id,
      book.publisher_id,
      book.published_date,
      book.stock_quantity,
    ];
    
    try {
      const result: QueryResult = await this.pool.query(query, values);
      return result.rows[0];
    } catch (error) {
      console.error('Error creating book:', error);
      throw error;
    }
  }

  async getBookById(bookId: number): Promise<Book | null> {
    const query = 'SELECT * FROM Books WHERE book_id = $1';
    const values = [bookId];

    try {
      const result: QueryResult = await this.pool.query(query, values);
      return result.rows.length ? result.rows[0] : null;
    } catch (error) {
      console.error(Error fetching book with ID ${bookId}:, error);
      throw error;
    }
  }

  async updateBook(bookId: number, updatedBook: Partial<CreateBookDTO>): Promise<Book | null> {
    const query = `
      UPDATE Books
      SET title = $1,
          genre_id = $2,
          price = $3,
          format = $4,
          author_id = $5,
          publisher_id = $6,
          published_date = $7,
          stock_quantity = $8
      WHERE book_id = $9
      RETURNING *
    `;
    const values = [
      updatedBook.title,
      updatedBook.genre_id,
      updatedBook.price,
      updatedBook.format,
      updatedBook.author_id,
      updatedBook.publisher_id,
      updatedBook.published_date,
      updatedBook.stock_quantity,
      bookId,
    ];

    try {
      const result: QueryResult = await this.pool.query(query, values);
      return result.rows.length ? result.rows[0] : null;
    } catch (error) {
      console.error(Error updating book with ID ${bookId}:, error);
      throw error;
    }
  }

  async deleteBook(bookId: number): Promise<boolean> {
    const query = 'DELETE FROM Books WHERE book_id = $1';
    const values = [bookId];

    try {
      const result: QueryResult = await this.pool.query(query, values);
      return result.rowCount !== null && result.rowCount > 0;
    } catch (error) {
      console.error(Error deleting book with ID ${bookId}:, error);
      throw error;
    }
  }

  async getAllBooks(): Promise<Book[]> {
    const query = 'SELECT * FROM Books';
    try {
      const result: QueryResult = await this.pool.query(query);
      return result.rows;
    } catch (error) {
      console.error('Error fetching books:', error);
      throw error;
    }
  }
}

async function initializeDatabase() {
  // Create tables if they don't exist
  const createTablesQuery = `
    CREATE TABLE IF NOT EXISTS Books (
      book_id SERIAL PRIMARY KEY,
      title VARCHAR(255),
      genre_id INT,
      price DECIMAL(10,2),
      format VARCHAR(20),
      author_id INT,
      publisher_id INT,
      published_date DATE,
      stock_quantity INT
    );
    -- Add other tables (Authors, Publishers, Genres, etc.) similarly
  `;
  
  try {
    await pool.query(createTablesQuery);
    console.log('Tables created successfully.');

    // Insert sample data if needed
    // Example: Inserting a sample book
    const bookRepo = new BookRepository(pool);
    const newBook: CreateBookDTO = {
      title: 'Sample Book',
      genre_id: 1,
      price: 19.99,
      format: 'physical',
      author_id: 1,
      publisher_id: 1,
      published_date: new Date('2024-01-01'),
      stock_quantity: 100,
    };
    const createdBook = await bookRepo.createBook(newBook);
    console.log('Created book:', createdBook);

    // Retrieve all books
    const allBooks = await bookRepo.getAllBooks();
    console.log('All books:', allBooks);

    // Example: Get book by ID
    const bookById = await bookRepo.getBookById(1);
    console.log('Book with ID 1:', bookById);

    // Example: Update book
    if (bookById) {
      const updatedBookData: Partial<CreateBookDTO> = {
        ...bookById,
        price: 24.99,
        format: 'ebook',
        stock_quantity: 120,
      };
      const updatedBook = await bookRepo.updateBook(1, updatedBookData);
      console.log('Updated book:', updatedBook);
    }

    // Example: Delete book
    const deleteResult = await bookRepo.deleteBook(1);
    console.log('Book deleted successfully:', deleteResult);

  } catch (error) {
    console.error('Error initializing database:', error);
    throw error;
  }
}

async function main() {
  try {
    await initializeDatabase();
  } catch (error) {
    console.error('An error occurred:', error);
  } finally {
    await pool.end();
  }
}

main();
```

## Explanation of the TypeScript Interface and Implementation

The TypeScript interface and implementation provide a structured way to interact with the Books table in the database. The BookRepository class contains methods to create, read, update, and delete books. The use of TypeScript interfaces ensures type safety and helps maintain a clear contract for the data structures used within the application.

- *CreateBookDTO*: Defines the structure of data required to create a new book.
- *UpdateBookDTO*: Defines the structure of data required to update an existing book.
- *BookRepository*: Contains methods to perform CRUD operations on the Books table.

By using these interfaces and classes, the application can reliably interact with the database, ensuring data integrity and consistency.
