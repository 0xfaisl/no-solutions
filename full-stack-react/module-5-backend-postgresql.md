# Module 5: Backend Development with Node.js & PostgreSQL

**Duration:** 10 weeks (1-2 hours/day)

**Prerequisites:** Modules 1-4 completed

**Philosophy:** You will build real backend systems from scratch. Labs provide requirements only—figuring out implementation is the learning.

---

## Why Node.js, Express, and PostgreSQL?

Before diving in, it's worth understanding why this particular stack was chosen.

### Why Node.js for Backend?

**Node.js vs Python/Django:**
- **JavaScript everywhere** — Same language on frontend and backend reduces context switching
- **npm ecosystem** — Largest package registry with solutions for almost anything
- **Non-blocking I/O** — Excellent for handling many concurrent connections (APIs, real-time apps)
- **JSON native** — No serialization needed; JavaScript objects flow naturally between layers

**Node.js vs Go:**
- **Lower barrier to entry** — If you know JavaScript, you're already halfway there
- **Faster prototyping** — Dynamic typing and vast ecosystem speed up development
- **Sufficient performance** — For most applications, Node.js is fast enough

**When Node.js might NOT be ideal:**
- CPU-intensive tasks (heavy computation, video processing)
- Systems requiring strict type safety at compile time
- When your team already has deep expertise in another language

### Why Express?

**Express vs Fastify:**
- **Mature ecosystem** — More middleware, tutorials, and community support
- **Industry standard** — Most Node.js job postings mention Express
- **Simple mental model** — Request comes in, middleware chain runs, response goes out
- Fastify is faster but Express's ecosystem advantage usually outweighs raw performance

**Express vs Hono:**
- Hono is newer, optimized for edge runtimes (Cloudflare Workers, Deno)
- Express is better documented and understood
- Choose Hono when targeting edge deployments specifically

**Express vs NestJS:**
- NestJS adds structure, decorators, dependency injection (more like Spring/Angular)
- Express is unopinionated — you decide the architecture
- Start with Express to understand fundamentals; consider NestJS for large enterprise projects

### Why PostgreSQL?

**PostgreSQL vs MongoDB:**
- **Relational data** — Most real-world data has relationships (users have orders, orders have items)
- **ACID compliance** — Transactions ensure data integrity
- **SQL is universal** — Knowledge transfers to MySQL, SQLite, SQL Server
- **JSON support** — PostgreSQL has excellent JSONB when you need flexibility
- MongoDB shines for truly document-oriented data, but SQL handles 90% of use cases better

**PostgreSQL vs MySQL:**
- More advanced features (CTEs, window functions, JSONB, full-text search)
- Better standards compliance
- Superior handling of concurrent writes
- MySQL is fine too, but PostgreSQL has become the modern default

### Why Prisma for ORM?

**Prisma vs raw SQL:**
- Type safety and autocompletion
- Migrations and schema management built-in
- Protection against SQL injection
- Still lets you drop to raw SQL when needed

**Prisma vs Sequelize/TypeORM:**
- Modern, intuitive API
- Excellent TypeScript support
- Prisma Studio for visual database browsing
- Better migration experience

**When to use raw SQL:**
- Complex analytical queries
- Performance-critical operations
- Learning SQL fundamentals (this module!)

---

## Week 1-2: Node.js & Express Fundamentals

### Learning Objectives
- Understand Node.js event loop and async patterns
- Build REST APIs with Express
- Create and use middleware
- Handle requests and responses properly

### Node.js Basics

**Core Concepts:**
- Node.js runtime vs browser JavaScript
- CommonJS (`require`) vs ES Modules (`import`)
- The event loop and non-blocking I/O
- `package.json` and dependency management

**npm Essentials:**
```bash
npm init -y                  # Initialize project
npm install express          # Install dependency
npm install -D nodemon       # Dev dependency
npm run <script>             # Run package scripts
```

**File System & Path:**
```javascript
const fs = require('fs');
const path = require('path');

// Async file operations
fs.readFile(path.join(__dirname, 'data.json'), 'utf8', (err, data) => {
  if (err) throw err;
  console.log(JSON.parse(data));
});

// Promise-based
const fsPromises = require('fs').promises;
const data = await fsPromises.readFile('data.json', 'utf8');
```

### Express Setup & Routing

**Basic Server:**
```javascript
const express = require('express');
const app = express();

// Middleware for JSON parsing
app.use(express.json());

// Routes
app.get('/api/users', (req, res) => {
  res.json({ users: [] });
});

app.post('/api/users', (req, res) => {
  const { name, email } = req.body;
  // Create user...
  res.status(201).json({ id: 1, name, email });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

**Route Parameters & Query Strings:**
```javascript
// Route params: /api/users/123
app.get('/api/users/:id', (req, res) => {
  const { id } = req.params;
});

// Query strings: /api/users?page=2&limit=10
app.get('/api/users', (req, res) => {
  const { page = 1, limit = 10 } = req.query;
});
```

**Router Modules:**
```javascript
// routes/users.js
const router = require('express').Router();

router.get('/', getAllUsers);
router.get('/:id', getUserById);
router.post('/', createUser);
router.put('/:id', updateUser);
router.delete('/:id', deleteUser);

module.exports = router;

// app.js
app.use('/api/users', require('./routes/users'));
```

### Middleware Concepts

Middleware functions have access to `req`, `res`, and `next`.

**Types of Middleware:**
```javascript
// Application-level
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
});

// Router-level
router.use(authMiddleware);

// Error-handling (4 parameters)
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong' });
});

// Built-in
app.use(express.json());
app.use(express.static('public'));

// Third-party
const cors = require('cors');
app.use(cors());
```

**Middleware Order Matters:**
```javascript
// This runs first
app.use(logger);

// Then authentication
app.use('/api', authenticate);

// Then routes
app.use('/api/users', userRoutes);

// Finally, error handler (must be last)
app.use(errorHandler);
```

### REST API Principles

**HTTP Methods:**
| Method | Purpose | Idempotent |
|--------|---------|------------|
| GET | Retrieve resource | Yes |
| POST | Create resource | No |
| PUT | Replace resource | Yes |
| PATCH | Partial update | Yes |
| DELETE | Remove resource | Yes |

**Status Codes:**
- `200` OK - Successful GET/PUT/PATCH
- `201` Created - Successful POST
- `204` No Content - Successful DELETE
- `400` Bad Request - Invalid input
- `401` Unauthorized - Authentication required
- `403` Forbidden - Authenticated but not allowed
- `404` Not Found - Resource doesn't exist
- `500` Internal Server Error - Server failure

**Resource Naming:**
```
GET    /api/users          # List all users
GET    /api/users/123      # Get specific user
POST   /api/users          # Create user
PUT    /api/users/123      # Replace user
PATCH  /api/users/123      # Update user
DELETE /api/users/123      # Delete user

# Nested resources
GET    /api/users/123/posts    # User's posts
POST   /api/users/123/posts    # Create post for user
```

### Week 1-2 Labs

**Lab 1: In-Memory CRUD API** | :red_circle: **Core**
Build a REST API for managing a todo list stored in memory (array).
- Implement all CRUD operations
- Add filtering by status (completed/pending)
- Add pagination (page, limit query params)
- Return proper status codes

**Lab 2: Request Logger Middleware** | :yellow_circle: **Recommended**
Create middleware that logs:
- Timestamp
- HTTP method and path
- Response time (requires measuring before/after)
- Response status code

**Lab 3: Multi-Resource API** | :red_circle: **Core**
Build an API with multiple related resources (e.g., authors and books).
- Separate route files for each resource
- Nested routes for relationships
- Consistent error responses

### Week 1-2 Review Prompts

Before moving on, reflect:
- **What did you learn?** Write down 3 key concepts from this section.
- **What's still unclear?** List any topics that need more practice or research.
- **What would you teach someone else?** Explaining solidifies understanding — pick one concept and write a brief explanation as if teaching a beginner.

---

## Week 3-4: SQL Fundamentals

### Learning Objectives
- Write CRUD operations in SQL
- Filter, sort, and limit results
- Join multiple tables
- Aggregate and group data

### Database Concepts

**PostgreSQL Setup:**
```bash
# Install PostgreSQL
brew install postgresql    # macOS
sudo apt install postgresql # Ubuntu

# Start service
brew services start postgresql

# Create database
createdb myapp_development

# Connect
psql myapp_development
```

**Basic psql Commands:**
```
\l          # List databases
\c dbname   # Connect to database
\dt         # List tables
\d table    # Describe table
\q          # Quit
```

### CRUD Operations

**CREATE - INSERT:**
```sql
-- Single row
INSERT INTO users (name, email, created_at)
VALUES ('Alice', 'alice@example.com', NOW());

-- Multiple rows
INSERT INTO users (name, email) VALUES
  ('Bob', 'bob@example.com'),
  ('Carol', 'carol@example.com');

-- Return inserted row
INSERT INTO users (name, email)
VALUES ('Dave', 'dave@example.com')
RETURNING id, name, email;
```

**READ - SELECT:**
```sql
-- All columns
SELECT * FROM users;

-- Specific columns
SELECT name, email FROM users;

-- With alias
SELECT name AS username, email AS contact FROM users;
```

**UPDATE:**
```sql
UPDATE users
SET name = 'Alice Smith', updated_at = NOW()
WHERE id = 1
RETURNING *;

-- Update multiple rows
UPDATE products
SET price = price * 1.10
WHERE category = 'electronics';
```

**DELETE:**
```sql
DELETE FROM users WHERE id = 1 RETURNING *;

-- Delete multiple
DELETE FROM sessions WHERE expires_at < NOW();
```

### Filtering & Sorting

**WHERE Clause:**
```sql
-- Comparison operators
SELECT * FROM products WHERE price > 100;
SELECT * FROM products WHERE price BETWEEN 50 AND 100;
SELECT * FROM users WHERE email LIKE '%@gmail.com';
SELECT * FROM users WHERE name ILIKE '%john%';  -- Case insensitive

-- Logical operators
SELECT * FROM products
WHERE category = 'electronics' AND price < 500;

SELECT * FROM products
WHERE category = 'books' OR category = 'music';

-- IN operator
SELECT * FROM users WHERE status IN ('active', 'pending');

-- NULL checks
SELECT * FROM users WHERE deleted_at IS NULL;
SELECT * FROM users WHERE phone IS NOT NULL;
```

**ORDER BY:**
```sql
SELECT * FROM products ORDER BY price ASC;
SELECT * FROM products ORDER BY created_at DESC;

-- Multiple columns
SELECT * FROM products
ORDER BY category ASC, price DESC;

-- With NULLS positioning
SELECT * FROM users ORDER BY last_login DESC NULLS LAST;
```

**LIMIT & OFFSET:**
```sql
-- First 10 rows
SELECT * FROM products LIMIT 10;

-- Pagination (page 3, 10 per page)
SELECT * FROM products
ORDER BY id
LIMIT 10 OFFSET 20;
```

### JOINs

**Sample Tables:**
```sql
-- users: id, name, email
-- posts: id, user_id, title, content
-- comments: id, post_id, user_id, body
```

**INNER JOIN:**
Returns only matching rows from both tables.
```sql
SELECT users.name, posts.title
FROM users
INNER JOIN posts ON users.id = posts.user_id;

-- With aliases
SELECT u.name, p.title
FROM users u
JOIN posts p ON u.id = p.user_id;
```

**LEFT JOIN:**
Returns all rows from left table, matched rows from right (or NULL).
```sql
-- All users, even those without posts
SELECT u.name, p.title
FROM users u
LEFT JOIN posts p ON u.id = p.user_id;

-- Find users with no posts
SELECT u.name
FROM users u
LEFT JOIN posts p ON u.id = p.user_id
WHERE p.id IS NULL;
```

**FULL OUTER JOIN:**
Returns all rows from both tables.
```sql
SELECT u.name, p.title
FROM users u
FULL OUTER JOIN posts p ON u.id = p.user_id;
```

**Multiple JOINs:**
```sql
SELECT u.name, p.title, c.body
FROM users u
JOIN posts p ON u.id = p.user_id
JOIN comments c ON p.id = c.post_id;
```

### Aggregate Functions

**Basic Aggregates:**
```sql
SELECT COUNT(*) FROM users;
SELECT COUNT(DISTINCT category) FROM products;
SELECT SUM(price) FROM order_items WHERE order_id = 1;
SELECT AVG(price) FROM products;
SELECT MIN(price), MAX(price) FROM products;
```

**GROUP BY:**
```sql
-- Count posts per user
SELECT user_id, COUNT(*) as post_count
FROM posts
GROUP BY user_id;

-- Total sales per category
SELECT category, SUM(price * quantity) as total
FROM order_items
JOIN products ON order_items.product_id = products.id
GROUP BY category;
```

**HAVING (filter groups):**
```sql
-- Users with more than 5 posts
SELECT user_id, COUNT(*) as post_count
FROM posts
GROUP BY user_id
HAVING COUNT(*) > 5;
```

### Week 3-4 Labs

**Lab 4: Query Challenge Set** | :red_circle: **Core**
Given these tables, write queries for each requirement:
```sql
-- Schema provided, write the queries yourself
CREATE TABLE customers (id, name, email, city, created_at);
CREATE TABLE orders (id, customer_id, total, status, created_at);
CREATE TABLE order_items (id, order_id, product_id, quantity, price);
CREATE TABLE products (id, name, category, price, stock);
```

Requirements:
1. Find all customers from a specific city
2. List orders with customer names
3. Calculate total revenue per product
4. Find customers who have never ordered
5. Top 5 products by quantity sold
6. Average order value per customer
7. Products that have never been ordered
8. Monthly revenue for the past year

**Lab 5: Library Database** | :yellow_circle: **Recommended**
Design and query a library system:
- Books, authors, members, loans
- Track borrowing history
- Handle multiple authors per book
- Write queries for overdue books, popular authors, member activity

### Week 3-4 Review Prompts

Before moving on, reflect:
- **What did you learn?** Write down 3 key concepts from this section.
- **What's still unclear?** List any topics that need more practice or research.
- **What would you teach someone else?** Explaining solidifies understanding — pick one concept and write a brief explanation as if teaching a beginner.

---

## Week 5-6: Database Design

### Learning Objectives
- Apply normalization rules
- Design proper relationships
- Create effective schemas
- Know when rules should be broken

### Normalization

**First Normal Form (1NF):**
- Each column contains atomic (indivisible) values
- Each column contains values of a single type
- Each row is unique

```sql
-- Violates 1NF (multiple values in one column)
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT,
  phone_numbers TEXT  -- '555-1234, 555-5678'
);

-- 1NF compliant
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT
);

CREATE TABLE phone_numbers (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  phone TEXT
);
```

**Second Normal Form (2NF):**
- Must be in 1NF
- All non-key columns depend on the entire primary key

```sql
-- Violates 2NF (course_name depends only on course_id)
CREATE TABLE enrollments (
  student_id INTEGER,
  course_id INTEGER,
  course_name TEXT,  -- Depends only on course_id
  grade TEXT,
  PRIMARY KEY (student_id, course_id)
);

-- 2NF compliant
CREATE TABLE courses (
  id SERIAL PRIMARY KEY,
  name TEXT
);

CREATE TABLE enrollments (
  student_id INTEGER,
  course_id INTEGER REFERENCES courses(id),
  grade TEXT,
  PRIMARY KEY (student_id, course_id)
);
```

**Third Normal Form (3NF):**
- Must be in 2NF
- No transitive dependencies (non-key depending on non-key)

```sql
-- Violates 3NF (city depends on zip_code, not directly on id)
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name TEXT,
  zip_code TEXT,
  city TEXT  -- Depends on zip_code
);

-- 3NF compliant
CREATE TABLE zip_codes (
  code TEXT PRIMARY KEY,
  city TEXT
);

CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name TEXT,
  zip_code TEXT REFERENCES zip_codes(code)
);
```

### Keys & Constraints

**Primary Keys:**
```sql
-- Serial (auto-increment)
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email TEXT UNIQUE NOT NULL
);

-- UUID
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT UNIQUE NOT NULL
);

-- Composite key
CREATE TABLE order_items (
  order_id INTEGER REFERENCES orders(id),
  product_id INTEGER REFERENCES products(id),
  quantity INTEGER NOT NULL,
  PRIMARY KEY (order_id, product_id)
);
```

**Foreign Keys:**
```sql
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  user_id INTEGER NOT NULL REFERENCES users(id),
  title TEXT NOT NULL
);

-- With actions
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  user_id INTEGER NOT NULL REFERENCES users(id)
    ON DELETE CASCADE
    ON UPDATE CASCADE,
  title TEXT NOT NULL
);
```

**Foreign Key Actions:**
- `CASCADE` - Delete/update related rows
- `SET NULL` - Set foreign key to NULL
- `SET DEFAULT` - Set to default value
- `RESTRICT` - Prevent delete/update (default)

**Other Constraints:**
```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  price DECIMAL(10,2) CHECK (price >= 0),
  sku TEXT UNIQUE,
  category TEXT DEFAULT 'uncategorized'
);
```

### Relationship Types

**One-to-One:**
```sql
-- User has one profile
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email TEXT UNIQUE NOT NULL
);

CREATE TABLE profiles (
  id SERIAL PRIMARY KEY,
  user_id INTEGER UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  bio TEXT,
  avatar_url TEXT
);
```

**One-to-Many:**
```sql
-- User has many posts
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL
);

CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  content TEXT
);
```

**Many-to-Many:**
```sql
-- Posts have many tags, tags have many posts
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title TEXT NOT NULL
);

CREATE TABLE tags (
  id SERIAL PRIMARY KEY,
  name TEXT UNIQUE NOT NULL
);

-- Junction/join table
CREATE TABLE post_tags (
  post_id INTEGER REFERENCES posts(id) ON DELETE CASCADE,
  tag_id INTEGER REFERENCES tags(id) ON DELETE CASCADE,
  PRIMARY KEY (post_id, tag_id)
);
```

### Schema Design Process

**Step 1: Identify Entities**
List all nouns from requirements (users, products, orders, etc.)

**Step 2: Define Attributes**
For each entity, list its properties.

**Step 3: Identify Relationships**
How do entities relate? What's the cardinality?

**Step 4: Apply Normalization**
Remove redundancy, ensure data integrity.

**Step 5: Add Constraints**
NOT NULL, UNIQUE, CHECK, DEFAULT values.

**Step 6: Consider Indexes**
What queries will be common? Index accordingly.

### When to Denormalize

**Acceptable Denormalization:**
- Read-heavy applications with infrequent writes
- Calculated fields that are expensive to compute
- Caching aggregates for reporting

```sql
-- Denormalized: store post_count on user
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT,
  post_count INTEGER DEFAULT 0  -- Updated via trigger
);

-- Instead of counting every time
SELECT u.*, COUNT(p.id) as post_count
FROM users u
LEFT JOIN posts p ON u.id = p.user_id
GROUP BY u.id;
```

**Red Flags for Denormalization:**
- Data can become inconsistent
- Updates become complex
- Storage increases

### Week 5-6 Labs

**Lab 6: E-Commerce Schema Design** | :red_circle: **Core**
Design a complete e-commerce database:
- Users with addresses (shipping, billing)
- Products with categories and variants (size, color)
- Orders with items and status history
- Reviews and ratings
- Wishlists

Requirements:
- Handle products with multiple images
- Support discount codes
- Track inventory per variant
- Draw the ERD before writing SQL

**Lab 7: Social Network Schema** | :yellow_circle: **Recommended**
Design a social platform:
- User profiles with followers/following
- Posts with likes and comments
- Comments can be nested (replies)
- Direct messages between users
- Groups with members and roles

Challenges:
- How to handle the follower relationship efficiently?
- How to store nested comments?
- How to prevent duplicate likes?

### Week 5-6 Review Prompts

Before moving on, reflect:
- **What did you learn?** Write down 3 key concepts from this section.
- **What's still unclear?** List any topics that need more practice or research.
- **What would you teach someone else?** Explaining solidifies understanding — pick one concept and write a brief explanation as if teaching a beginner.

---

## Week 7-8: Advanced SQL

### Learning Objectives
- Optimize queries with indexes
- Write complex queries with subqueries and CTEs
- Use window functions for analytics
- Work with JSON data in PostgreSQL

### Indexes & Performance

**Creating Indexes:**
```sql
-- Single column
CREATE INDEX idx_users_email ON users(email);

-- Composite index
CREATE INDEX idx_orders_user_date ON orders(user_id, created_at);

-- Unique index
CREATE UNIQUE INDEX idx_users_email ON users(email);

-- Partial index
CREATE INDEX idx_active_users ON users(email)
WHERE status = 'active';

-- Expression index
CREATE INDEX idx_users_lower_email ON users(LOWER(email));
```

**When to Index:**
- Columns in WHERE clauses
- Columns in JOIN conditions
- Columns in ORDER BY
- Foreign key columns

**When NOT to Index:**
- Small tables
- Columns with low cardinality (few unique values)
- Tables with heavy INSERT/UPDATE activity
- Columns rarely used in queries

**EXPLAIN ANALYZE:**
```sql
EXPLAIN ANALYZE
SELECT * FROM orders
WHERE user_id = 123
ORDER BY created_at DESC;

-- Look for:
-- Seq Scan (bad for large tables)
-- Index Scan (good)
-- actual time and rows
```

### Subqueries

**In WHERE clause:**
```sql
-- Users who have placed orders
SELECT * FROM users
WHERE id IN (SELECT DISTINCT user_id FROM orders);

-- Products priced above average
SELECT * FROM products
WHERE price > (SELECT AVG(price) FROM products);
```

**In FROM clause (derived table):**
```sql
-- Top customer per month
SELECT month, customer_id, total
FROM (
  SELECT
    DATE_TRUNC('month', created_at) as month,
    customer_id,
    SUM(total) as total,
    ROW_NUMBER() OVER (
      PARTITION BY DATE_TRUNC('month', created_at)
      ORDER BY SUM(total) DESC
    ) as rank
  FROM orders
  GROUP BY 1, 2
) ranked
WHERE rank = 1;
```

**Correlated Subquery:**
```sql
-- Users with their latest order date
SELECT
  u.name,
  (SELECT MAX(created_at) FROM orders o WHERE o.user_id = u.id) as last_order
FROM users u;
```

### Common Table Expressions (CTEs)

**Basic CTE:**
```sql
WITH active_users AS (
  SELECT * FROM users WHERE status = 'active'
)
SELECT * FROM active_users WHERE created_at > '2024-01-01';
```

**Multiple CTEs:**
```sql
WITH
  monthly_orders AS (
    SELECT
      DATE_TRUNC('month', created_at) as month,
      COUNT(*) as order_count,
      SUM(total) as revenue
    FROM orders
    GROUP BY 1
  ),
  monthly_growth AS (
    SELECT
      month,
      revenue,
      LAG(revenue) OVER (ORDER BY month) as prev_revenue
    FROM monthly_orders
  )
SELECT
  month,
  revenue,
  ROUND((revenue - prev_revenue) / prev_revenue * 100, 2) as growth_pct
FROM monthly_growth
WHERE prev_revenue IS NOT NULL;
```

**Recursive CTE:**
```sql
-- Organizational hierarchy
WITH RECURSIVE org_tree AS (
  -- Base case: top-level managers
  SELECT id, name, manager_id, 1 as level
  FROM employees
  WHERE manager_id IS NULL

  UNION ALL

  -- Recursive case
  SELECT e.id, e.name, e.manager_id, t.level + 1
  FROM employees e
  JOIN org_tree t ON e.manager_id = t.id
)
SELECT * FROM org_tree ORDER BY level, name;
```

### Window Functions

**ROW_NUMBER, RANK, DENSE_RANK:**
```sql
SELECT
  name,
  category,
  price,
  ROW_NUMBER() OVER (ORDER BY price DESC) as row_num,
  RANK() OVER (ORDER BY price DESC) as rank,
  DENSE_RANK() OVER (ORDER BY price DESC) as dense_rank
FROM products;
```

**PARTITION BY:**
```sql
-- Rank within each category
SELECT
  name,
  category,
  price,
  RANK() OVER (PARTITION BY category ORDER BY price DESC) as category_rank
FROM products;
```

**LAG and LEAD:**
```sql
-- Compare to previous/next row
SELECT
  date,
  revenue,
  LAG(revenue) OVER (ORDER BY date) as prev_day,
  LEAD(revenue) OVER (ORDER BY date) as next_day,
  revenue - LAG(revenue) OVER (ORDER BY date) as daily_change
FROM daily_sales;
```

**Running Totals and Averages:**
```sql
SELECT
  date,
  revenue,
  SUM(revenue) OVER (ORDER BY date) as running_total,
  AVG(revenue) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) as week_avg
FROM daily_sales;
```

### JSONB in PostgreSQL

**Creating JSONB Columns:**
```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  attributes JSONB DEFAULT '{}'
);

INSERT INTO products (name, attributes) VALUES
  ('T-Shirt', '{"color": "red", "size": "M", "material": "cotton"}'),
  ('Laptop', '{"brand": "Dell", "ram": 16, "storage": 512}');
```

**Querying JSONB:**
```sql
-- Access field
SELECT name, attributes->>'color' as color FROM products;

-- Filter by JSONB field
SELECT * FROM products
WHERE attributes->>'color' = 'red';

-- Check if key exists
SELECT * FROM products
WHERE attributes ? 'brand';

-- Contains
SELECT * FROM products
WHERE attributes @> '{"size": "M"}';
```

**JSONB Operators:**
```sql
->    -- Get JSON object field (returns JSON)
->>   -- Get JSON object field (returns text)
#>    -- Get nested field (returns JSON)
#>>   -- Get nested field (returns text)
?     -- Key exists
@>    -- Contains
```

**Modifying JSONB:**
```sql
-- Add/update field
UPDATE products
SET attributes = attributes || '{"on_sale": true}'
WHERE id = 1;

-- Remove field
UPDATE products
SET attributes = attributes - 'on_sale'
WHERE id = 1;
```

**JSONB Indexes:**
```sql
-- GIN index for containment queries
CREATE INDEX idx_products_attrs ON products USING GIN (attributes);

-- Index specific path
CREATE INDEX idx_products_color ON products ((attributes->>'color'));
```

### Week 7-8 Labs

**Lab 8: Query Optimization Challenge** | :red_circle: **Core**
Given a slow-performing database:
- Use EXPLAIN ANALYZE to identify bottlenecks
- Add appropriate indexes
- Rewrite queries for better performance
- Document before/after query times

**Lab 9: Analytics Dashboard Queries** | :yellow_circle: **Recommended**
Write queries for a business dashboard:
- Revenue by day/week/month with comparison to previous period
- Top 10 customers by lifetime value
- Product performance with running totals
- Customer cohort retention analysis
- Moving averages for trend analysis

All queries should use CTEs and window functions where appropriate.

### Week 7-8 Review Prompts

Before moving on, reflect:
- **What did you learn?** Write down 3 key concepts from this section.
- **What's still unclear?** List any topics that need more practice or research.
- **What would you teach someone else?** Explaining solidifies understanding — pick one concept and write a brief explanation as if teaching a beginner.

---

## Week 9-10: API Development

### Learning Objectives
- Implement secure authentication
- Hash passwords properly
- Validate input data
- Handle errors gracefully
- Use an ORM for database operations

### Authentication with JWT

**How JWT Works:**
1. User logs in with credentials
2. Server verifies and returns signed token
3. Client includes token in subsequent requests
4. Server verifies token signature

**Implementation:**
```javascript
const jwt = require('jsonwebtoken');
const JWT_SECRET = process.env.JWT_SECRET;

// Generate token
function generateToken(user) {
  return jwt.sign(
    { id: user.id, email: user.email },
    JWT_SECRET,
    { expiresIn: '7d' }
  );
}

// Verify middleware
function authenticate(req, res, next) {
  const authHeader = req.headers.authorization;

  if (!authHeader?.startsWith('Bearer ')) {
    return res.status(401).json({ error: 'No token provided' });
  }

  const token = authHeader.split(' ')[1];

  try {
    const decoded = jwt.verify(token, JWT_SECRET);
    req.user = decoded;
    next();
  } catch (err) {
    return res.status(401).json({ error: 'Invalid token' });
  }
}

// Login route
app.post('/api/login', async (req, res) => {
  const { email, password } = req.body;

  const user = await findUserByEmail(email);
  if (!user || !await verifyPassword(password, user.password_hash)) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }

  const token = generateToken(user);
  res.json({ token, user: { id: user.id, email: user.email } });
});
```

### Password Hashing

**Never store plain text passwords.**

```javascript
const bcrypt = require('bcrypt');
const SALT_ROUNDS = 12;

// Hash password before storing
async function hashPassword(password) {
  return bcrypt.hash(password, SALT_ROUNDS);
}

// Verify password
async function verifyPassword(password, hash) {
  return bcrypt.compare(password, hash);
}

// Registration
app.post('/api/register', async (req, res) => {
  const { email, password } = req.body;

  const existingUser = await findUserByEmail(email);
  if (existingUser) {
    return res.status(400).json({ error: 'Email already registered' });
  }

  const passwordHash = await hashPassword(password);
  const user = await createUser({ email, password_hash: passwordHash });

  const token = generateToken(user);
  res.status(201).json({ token, user: { id: user.id, email: user.email } });
});
```

### Input Validation

**Using express-validator:**
```javascript
const { body, validationResult } = require('express-validator');

const userValidation = [
  body('email')
    .isEmail()
    .normalizeEmail()
    .withMessage('Valid email required'),
  body('password')
    .isLength({ min: 8 })
    .withMessage('Password must be at least 8 characters')
    .matches(/[A-Z]/)
    .withMessage('Password must contain uppercase letter')
    .matches(/[0-9]/)
    .withMessage('Password must contain number'),
  body('name')
    .trim()
    .notEmpty()
    .withMessage('Name required')
    .escape()
];

// Validation middleware
function validate(req, res, next) {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    return res.status(400).json({ errors: errors.array() });
  }
  next();
}

app.post('/api/register', userValidation, validate, async (req, res) => {
  // Input is validated and sanitized
});
```

### Error Handling Middleware

**Custom Error Class:**
```javascript
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.isOperational = true;
  }
}

// Not found
class NotFoundError extends AppError {
  constructor(resource = 'Resource') {
    super(`${resource} not found`, 404);
  }
}

// Validation error
class ValidationError extends AppError {
  constructor(message) {
    super(message, 400);
  }
}
```

**Error Handler Middleware:**
```javascript
function errorHandler(err, req, res, next) {
  console.error(err);

  // Operational errors (expected)
  if (err.isOperational) {
    return res.status(err.statusCode).json({
      error: err.message
    });
  }

  // Programming errors (unexpected)
  res.status(500).json({
    error: 'Internal server error'
  });
}

// Async wrapper to catch errors
function asyncHandler(fn) {
  return (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
}

// Usage
app.get('/api/users/:id', asyncHandler(async (req, res) => {
  const user = await findUserById(req.params.id);
  if (!user) throw new NotFoundError('User');
  res.json(user);
}));

// Must be last middleware
app.use(errorHandler);
```

### Prisma ORM Basics

**Setup:**
```bash
npm install prisma @prisma/client
npx prisma init
```

**Schema Definition (prisma/schema.prisma):**
```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  password  String
  posts     Post[]
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
  createdAt DateTime @default(now())
}
```

**Migrations:**
```bash
npx prisma migrate dev --name init
npx prisma generate
```

**CRUD Operations:**
```javascript
const { PrismaClient } = require('@prisma/client');
const prisma = new PrismaClient();

// Create
const user = await prisma.user.create({
  data: {
    email: 'alice@example.com',
    name: 'Alice',
    password: hashedPassword
  }
});

// Read
const users = await prisma.user.findMany({
  where: { name: { contains: 'ali', mode: 'insensitive' } },
  include: { posts: true },
  orderBy: { createdAt: 'desc' },
  take: 10,
  skip: 0
});

const user = await prisma.user.findUnique({
  where: { id: 1 }
});

// Update
const updated = await prisma.user.update({
  where: { id: 1 },
  data: { name: 'Alice Smith' }
});

// Delete
await prisma.user.delete({
  where: { id: 1 }
});
```

**Relations:**
```javascript
// Create with relation
const post = await prisma.post.create({
  data: {
    title: 'Hello World',
    content: 'My first post',
    author: {
      connect: { id: 1 }
    }
  }
});

// Include relations
const userWithPosts = await prisma.user.findUnique({
  where: { id: 1 },
  include: {
    posts: {
      where: { published: true },
      orderBy: { createdAt: 'desc' }
    }
  }
});
```

### Week 9-10 Labs

**Lab 10: Authenticated API** | :red_circle: **Core**
Build a complete API with:
- User registration and login
- JWT authentication
- Protected routes
- Role-based access control (user/admin)
- Password reset flow (describe the logic)

**Lab 11: Full CRUD with Prisma** | :yellow_circle: **Recommended**
Create an API for a blog platform:
- Users, posts, comments, tags
- Full CRUD for all resources
- Input validation on all endpoints
- Proper error handling
- Pagination and filtering

### Week 9-10 Review Prompts

Before moving on, reflect:
- **What did you learn?** Write down 3 key concepts from this section.
- **What's still unclear?** List any topics that need more practice or research.
- **What would you teach someone else?** Explaining solidifies understanding — pick one concept and write a brief explanation as if teaching a beginner.

---

## Build-Your-Own Projects

### Project 1: Simple Query Builder

Build a JavaScript class that generates SQL queries through method chaining.

**Requirements:**
- Support SELECT, INSERT, UPDATE, DELETE operations
- Method chaining: `.select().from().where().orderBy().limit()`
- Handle multiple conditions with AND/OR
- Support JOINs
- Prevent SQL injection (use parameterized queries)
- Return both query string and parameters

**Example Interface (implement yourself):**
```javascript
const query = new QueryBuilder()
  .select('id', 'name', 'email')
  .from('users')
  .where('status', '=', 'active')
  .where('created_at', '>', '2024-01-01')
  .orderBy('name', 'ASC')
  .limit(10);

console.log(query.toSQL());
// SELECT id, name, email FROM users WHERE status = $1 AND created_at > $2 ORDER BY name ASC LIMIT 10

console.log(query.getParams());
// ['active', '2024-01-01']
```

**Stretch Goals:**
- Support subqueries
- Add `.orWhere()` method
- Support aggregate functions
- Generate INSERT with RETURNING

#### Project Variations

**Option A: Guided** (More structure)
- Start with a provided class skeleton with method signatures
- Follow step-by-step implementation order: SELECT -> WHERE -> ORDER BY -> LIMIT -> JOINs
- Use provided test cases to verify each step
- Hints for handling parameterized queries

**Option B: Standard** (Current approach)
- Requirements and example interface provided
- Figure out class structure and implementation yourself
- Build tests as you go

**Option C: Open-ended** (Minimal hints)
- Goal: Build a query builder that prevents SQL injection
- No interface provided — design your own API
- Bonus: Support transactions, CTEs, or subqueries

---

### Project 2: Basic ORM Layer

Build a simple Object-Relational Mapper that converts between JavaScript objects and database rows.

**Requirements:**
- Define models with field types
- Automatic table creation from model definition
- CRUD operations: `create()`, `findById()`, `findAll()`, `update()`, `delete()`
- Simple query filters: `findAll({ where: { status: 'active' } })`
- Handle relationships (hasMany, belongsTo)
- Validate data types before saving

**Example Interface (implement yourself):**
```javascript
class User extends Model {
  static tableName = 'users';

  static fields = {
    id: { type: 'serial', primaryKey: true },
    email: { type: 'string', unique: true, required: true },
    name: { type: 'string', required: true },
    createdAt: { type: 'timestamp', default: 'now' }
  };

  static hasMany = {
    posts: { model: 'Post', foreignKey: 'user_id' }
  };
}

// Usage
const user = await User.create({ email: 'test@example.com', name: 'Test' });
const found = await User.findById(1);
const active = await User.findAll({ where: { status: 'active' }, limit: 10 });
await User.update(1, { name: 'Updated' });
await User.delete(1);
```

**Stretch Goals:**
- Add migrations support
- Implement transactions
- Add hooks (beforeSave, afterCreate, etc.)
- Support eager loading of relations

#### Project Variations

**Option A: Guided** (More structure)
- Start with a base Model class skeleton
- Implement in order: field definitions -> create() -> findById() -> findAll() -> update() -> delete() -> relationships
- Provided SQL templates for each operation
- Step-by-step hints for handling relationships

**Option B: Standard** (Current approach)
- Requirements and example interface provided
- Design the Model base class yourself
- Decide how to handle SQL generation and relationships

**Option C: Open-ended** (Minimal hints)
- Goal: Build an ORM that maps JavaScript classes to database tables
- Design your own API — it doesn't have to match the example
- Bonus: Support migrations, query scopes, or soft deletes

---

## Comprehensive Labs

### Lab: Library Management System | :red_circle: **Core**

Design and implement a complete library database system.

**Entities:**
- Books (title, ISBN, publication year, etc.)
- Authors (books can have multiple authors)
- Members (name, membership date, contact info)
- Loans (track who borrowed what and when)
- Categories/Genres

**Requirements:**
- Design the schema with proper normalization
- Implement all relationships correctly
- Write queries for:
  - All books by a specific author
  - Currently overdue books with member contact info
  - Most popular books (by loan count)
  - Members who have never borrowed
  - Books that have never been borrowed
  - Average loan duration by category
  - Members with overdue fines (calculate based on days overdue)

---

### Lab: E-Commerce Database | :yellow_circle: **Recommended**

Build the database for an online store.

**Entities:**
- Customers (with multiple addresses)
- Products (with variants like size/color)
- Categories (hierarchical)
- Orders and order items
- Reviews
- Inventory tracking

**Requirements:**
- Handle product variants properly
- Support multiple shipping/billing addresses per customer
- Track order status history
- Write queries for:
  - Product inventory alerts (stock below threshold)
  - Best-selling products by category
  - Customer lifetime value
  - Revenue by month with growth percentage
  - Products frequently bought together
  - Average rating per product with review count

---

### Lab: Social Network Database | :green_circle: **Stretch**

Design a social platform's data layer.

**Entities:**
- Users with profiles
- Posts (text, images, links)
- Comments (support nesting/replies)
- Likes (on posts and comments)
- Followers/Following relationships
- Direct messages
- Groups with members and roles

**Requirements:**
- Efficient follower/following queries
- Handle nested comments (consider: adjacency list vs nested sets)
- Prevent duplicate likes
- Write queries for:
  - User's feed (posts from people they follow)
  - Suggested connections (friends of friends)
  - Trending posts (most engagement in last 24 hours)
  - Mutual followers between two users
  - Group activity summary
  - Conversation threads between two users

---

## Fourth Deploy Checkpoint

### Deploy API to Railway with PostgreSQL

**Objective:** Deploy your Module 5 API to Railway with a PostgreSQL database.

**Requirements:**
1. Working Express API with at least 3 resources
2. PostgreSQL database with proper schema
3. Authentication implemented
4. Environment variables for secrets
5. Error handling middleware
6. Input validation

**Steps:**
1. Create Railway account
2. Create new project
3. Add PostgreSQL plugin
4. Configure environment variables:
   - `DATABASE_URL` (provided by Railway)
   - `JWT_SECRET`
   - `NODE_ENV=production`
5. Deploy from GitHub repository
6. Run migrations in production
7. Test all endpoints

**Verification Checklist:**
- [ ] API responds at Railway URL
- [ ] Database connection works
- [ ] Authentication flow functions
- [ ] Protected routes require valid token
- [ ] Error responses are consistent
- [ ] No sensitive data in error messages

---

## Recommended Resources

### Official Documentation
- **Node.js:** https://nodejs.org/docs/latest/api/ — Core modules reference
- **Express.js:** https://expressjs.com/en/guide/routing.html — Routing and middleware guides
- **PostgreSQL:** https://www.postgresql.org/docs/current/ — Comprehensive SQL reference
- **Prisma:** https://www.prisma.io/docs — ORM setup, schema, and queries

### SQL Practice Platforms
- **SQLZoo:** https://sqlzoo.net — Interactive SQL tutorials
- **PostgreSQL Exercises:** https://pgexercises.com — PostgreSQL-specific practice
- **LeetCode Database:** https://leetcode.com/problemset/database/ — SQL interview problems
- **HackerRank SQL:** https://www.hackerrank.com/domains/sql — Structured SQL challenges

### Video Tutorials
- **Traversy Media:** Node.js and Express crash courses on YouTube
- **The Net Ninja:** PostgreSQL and Prisma tutorial series
- **Fireship:** Short, dense explanations of backend concepts
- **Hussein Nasser:** Deep dives on database internals and performance

### Books
- **"Designing Data-Intensive Applications"** by Martin Kleppmann — Essential for understanding databases
- **"SQL Antipatterns"** by Bill Karwin — Learn what NOT to do
- **"Node.js Design Patterns"** by Mario Casciaro — Advanced Node.js architecture

### Tools
- **Postman** or **Insomnia:** API testing and documentation
- **pgAdmin** or **DBeaver:** Database management GUIs
- **TablePlus:** Clean PostgreSQL GUI (macOS/Windows)
- **Prisma Studio:** Visual database browser (comes with Prisma)

---

## Self-Assessment Checkpoint

### Can You Do This?

Before moving to Module 6, test yourself with these challenges. No hints provided — if you can complete them all, you're ready.

**SQL Challenges:**

1. **Write a query** that finds all customers who have placed more than 3 orders in the last 30 days, showing their name and total spent.

2. **Write a query** using a CTE and window function that ranks products within each category by revenue, showing only the top 3 per category.

3. **Write a query** that finds "loyal customers" — those who have ordered every month for the past 6 months.

**Backend Challenges:**

4. **Build an endpoint** `GET /api/stats/daily` that returns order counts and revenue for each of the last 7 days, including days with zero orders.

5. **Implement middleware** that rate-limits requests to 100 per minute per IP address, returning a 429 status when exceeded.

6. **Design a schema** for a booking system (like Calendly) where users can set available time slots and others can book appointments. Include the SQL to find all available slots for a given user on a given day.

---

**How did you do?**
- **6/6:** You're ready for Module 6
- **4-5/6:** Review the topics you struggled with, then retry
- **3 or fewer:** Spend more time on the labs before moving on

---

## Additional Resources

### PostgreSQL Documentation
- Official docs: postgresql.org/docs
- Interactive tutorial: pgexercises.com

### Express.js
- Official guide: expressjs.com/en/guide
- Best practices: expressjs.com/en/advanced/best-practice-security.html

### Security
- OWASP API Security Top 10
- Node.js Security Checklist

### Tools
- Postman or Insomnia for API testing
- pgAdmin or DBeaver for database management
- TablePlus (macOS) for PostgreSQL GUI

---

## Module Completion Criteria

Before proceeding to Module 6, ensure you can:

- [ ] Build REST APIs with Express.js
- [ ] Write complex SQL queries with joins and aggregations
- [ ] Design normalized database schemas
- [ ] Use CTEs and window functions
- [ ] Implement JWT authentication
- [ ] Hash passwords securely
- [ ] Validate and sanitize input
- [ ] Handle errors gracefully
- [ ] Use Prisma for database operations
- [ ] Deploy to Railway with PostgreSQL

**Project Portfolio Addition:** Your deployed API demonstrates backend competency to potential employers.
