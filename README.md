# Thrift & Handmade Store — Database ER Diagram

A database design for a small Instagram-based store that sells thrifted fashion items and handmade products. Orders are received via Instagram DMs and WhatsApp, and the owner needs to manage products, stock, customers, payments, and deliveries.


## Entities

| Entity | Description |
|---|---|
| `CUSTOMER` | Stores customer contact info and Instagram handle |
| `PRODUCT` | Shared product details — name, category, price, and type |
| `THRIFT_ITEM` | Subtype for thrifted products — condition, brand, size, color |
| `HANDMADE_ITEM` | Subtype for handmade products — material, batch number, quantity |
| `ORDER` | A customer's order — status, date, and total amount |
| `ORDER_ITEM` | Junction table linking orders to products (many-to-many) |
| `PAYMENT` | Payment method, status, and transaction details for an order |
| `SHIPMENT` | Carrier, tracking, and delivery status for an order |

---

## Key Design Decisions

- **Product subtyping** — `THRIFT_ITEM` and `HANDMADE_ITEM` are separate tables that extend `PRODUCT`. A thrift item typically has `quantity = 1` since each piece is unique. A handmade item can have `quantity_available > 1` and may belong to a batch.
- **ORDER_ITEM as a junction table** — handles the many-to-many relationship between orders and products. Stores `unit_price` at time of purchase so price changes don't affect order history.
- **Payment and Shipment are separate** — each has its own lifecycle and status, and both are optional extensions of an order.
- **Customer is reusable** — one customer record links to all their past orders.

---

## Relationships

- A **customer** can place many **orders**
- An **order** contains one or more **products** (via `ORDER_ITEM`)
- A **product** is either a **thrift item** or a **handmade item**
- An **order** has at most one **payment** and one **shipment**

---

## Tools Used

- Diagram designed using **Draw.io** 
- Exported as PNG for submission
