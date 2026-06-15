# Farmer Supply Chain - Technical Knowledge Base

## Technology Stack
*   **Frontend**: Next.js 16 (App Router)
*   **Styling**: Tailwind CSS v4
*   **Backend**: Next.js API Routes (or Express in `server/`)
*   **Database**: Relational Database (Prisma/PostgreSQL recommended)

## Core Database Schema Design (Proposed)

### Users Schema
```sql
CREATE TABLE users (
  id VARCHAR PRIMARY KEY,
  name VARCHAR NOT NULL,
  email VARCHAR UNIQUE NOT NULL,
  password_hash VARCHAR NOT NULL,
  role VARCHAR NOT NULL, -- FARMER, MIDDLEMAN, TRADER, PROCESSOR, MANUFACTURER, FMCG, EXPORTER, BULK_CONSUMER, TRANSPORTER, ASSESSOR
  gst_number VARCHAR,
  address TEXT NOT NULL,
  phone VARCHAR NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Inventory Schema (with Traceability)
```sql
CREATE TABLE inventory_items (
  id VARCHAR PRIMARY KEY,
  owner_id VARCHAR REFERENCES users(id),
  title VARCHAR NOT NULL,
  description TEXT,
  category VARCHAR NOT NULL, -- RAW, SEMI_PROCESSED, FINISHED
  quantity DECIMAL NOT NULL,
  unit VARCHAR NOT NULL, -- KGS, TONS, BAGS
  price_per_unit DECIMAL NOT NULL,
  location VARCHAR NOT NULL,
  quality_grade VARCHAR DEFAULT 'UNGRADED',
  traceability_parent_id VARCHAR REFERENCES inventory_items(id), -- Tracks heritage of the batch
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Order & Invoicing Schema
```sql
CREATE TABLE orders (
  id VARCHAR PRIMARY KEY,
  buyer_id VARCHAR REFERENCES users(id),
  seller_id VARCHAR REFERENCES users(id),
  status VARCHAR NOT NULL, -- PENDING, ACCEPTED, IN_TRANSIT, DELIVERED, CANCELLED
  total_amount DECIMAL NOT NULL,
  payment_status VARCHAR NOT NULL, -- UNPAID, ESCROW, PAID
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Logistics & Tracking
```sql
CREATE TABLE shipments (
  id VARCHAR PRIMARY KEY,
  order_id VARCHAR REFERENCES orders(id),
  transporter_id VARCHAR REFERENCES users(id),
  vehicle_number VARCHAR,
  status VARCHAR NOT NULL, -- DISPATCHED, IN_TRANSIT, DELIVERED
  dispatch_date TIMESTAMP,
  delivery_date TIMESTAMP,
  tracking_data JSONB
);
```
