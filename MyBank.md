# 🏦MyBank table scripts

## Customer Table
```sql
CREATE SEQUENCE IF NOT EXISTS seq_customer_id START 1000000001;

CREATE TABLE IF NOT EXISTS customers (
    customer_id BIGINT PRIMARY KEY DEFAULT nextval('seq_customer_id'),
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15) UNIQUE,
    pan_number VARCHAR(20) UNIQUE,
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ALTER SEQUENCE seq_customer_id OWNED BY customers.customer_id;

CREATE INDEX IF NOT EXISTS idx_customers_email ON customers(email);
CREATE INDEX IF NOT EXISTS idx_customers_phone ON customers(phone);
```
## Branch Table
```sql
CREATE SEQUENCE IF NOT EXISTS seq_branch_id START 1001;

CREATE TABLE IF NOT EXISTS branches (
    branch_id BIGINT PRIMARY KEY DEFAULT nextval('seq_branch_id'),
    branch_name VARCHAR(100) NOT NULL,
    ifsc_code VARCHAR(15) UNIQUE NOT NULL,
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ALTER SEQUENCE seq_branch_id OWNED BY branches.branch_id;
```
## Account Types
```sql
CREATE SEQUENCE IF NOT EXISTS seq_account_type_id START 1;

CREATE TABLE IF NOT EXISTS account_types (
    account_type_id SMALLINT PRIMARY KEY DEFAULT nextval('seq_account_type_id'),
    type_name VARCHAR(50) UNIQUE NOT NULL,       -- e.g., Savings, Current
    interest_rate DECIMAL(5,2) DEFAULT 0.00,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ALTER SEQUENCE seq_account_type_id OWNED BY account_types.account_type_id;
```
### Status Table
```sql
CREATE SEQUENCE IF NOT EXISTS seq_status_id START 1;

CREATE TABLE IF NOT EXISTS statuses (
    status_id SMALLINT PRIMARY KEY DEFAULT nextval('seq_status_id'),
    entity_type VARCHAR(20) NOT NULL CHECK (entity_type IN ('ACCOUNT','TRANSACTION')),
    status_name VARCHAR(20) NOT NULL,
    description TEXT
);

ALTER SEQUENCE seq_status_id OWNED BY statuses.status_id;

-- Example inserts
INSERT INTO statuses (entity_type, status_name) VALUES
('ACCOUNT','ACTIVE'),
('ACCOUNT','INACTIVE'),
('ACCOUNT','CLOSED'),
('TRANSACTION','CREDIT'),
('TRANSACTION','DEBIT')
ON CONFLICT DO NOTHING;
```
### Accounts Table
```sql
CREATE SEQUENCE IF NOT EXISTS seq_account_id START 5000000001; -- realistic 10-digit numbers

CREATE TABLE IF NOT EXISTS accounts (
    account_id BIGINT PRIMARY KEY DEFAULT nextval('seq_account_id'),  -- external account number
    internal_id BIGINT NOT NULL GENERATED ALWAYS AS IDENTITY,          -- internal DB id
    account_type_id SMALLINT NOT NULL REFERENCES account_types(account_type_id),
    branch_id BIGINT REFERENCES branches(branch_id),
    status_id SMALLINT NOT NULL REFERENCES statuses(status_id),
    balance NUMERIC(18,2) DEFAULT 0.00 CHECK (balance >= 0),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ALTER SEQUENCE seq_account_id OWNED BY accounts.account_id;

-- Indexes
CREATE INDEX IF NOT EXISTS idx_accounts_branch_id ON accounts(branch_id);
CREATE INDEX IF NOT EXISTS idx_accounts_status_id ON accounts(status_id);
```
## Customer-Accounts Mapping (Joint Accounts)
```sql
CREATE TABLE IF NOT EXISTS customer_accounts (
    customer_id BIGINT NOT NULL REFERENCES customers(customer_id) ON DELETE CASCADE,
    account_id BIGINT NOT NULL REFERENCES accounts(account_id) ON DELETE CASCADE,
    ownership_type VARCHAR(10) DEFAULT 'PRIMARY' CHECK (ownership_type IN ('PRIMARY','JOINT')),
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(customer_id, account_id)
);

CREATE INDEX IF NOT EXISTS idx_customer_accounts_account_id ON customer_accounts(account_id);
```
## Transactions Table
```sql
CREATE SEQUENCE IF NOT EXISTS seq_transaction_id START 1;

CREATE TABLE IF NOT EXISTS transactions (
    transaction_id BIGINT PRIMARY KEY DEFAULT nextval('seq_transaction_id'),
    account_id BIGINT NOT NULL REFERENCES accounts(account_id) ON DELETE CASCADE,
    amount NUMERIC(18,2) NOT NULL CHECK (amount >= 0),
    status_id SMALLINT NOT NULL REFERENCES statuses(status_id),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ALTER SEQUENCE seq_transaction_id OWNED BY transactions.transaction_id;

CREATE INDEX IF NOT EXISTS idx_transactions_account_id ON transactions(account_id);
CREATE INDEX IF NOT EXISTS idx_transactions_status_id ON transactions(status_id);
```
