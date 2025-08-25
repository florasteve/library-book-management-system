# Library Book Management System

Relational database for end-to-end library operations: **catalog, members, lending, reservations, fines**.  
Built for **SQL Server** in **SSMS** with a **3NF** schema, **T-SQL** stored procedures, and reporting views.

---

## 🚀 Features
- Catalog management: Books ↔ Authors (many-to-many)
- Circulation: Checkout / Return with due dates, renewals, grace period
- Reservations/holds queue with first-come fulfillment
- Overdue tracking & fine calculation (optional)
- Reporting views: availability, overdues, active reservations

## 🧱 Schema (Core Tables)
- `Authors(AuthorId, FirstName, LastName, ... )`
- `Books(BookId, ISBN, Title, PublishedYear, CopiesTotal, CopiesAvailable, ...)`
- `BookAuthors(BookId, AuthorId)` (M:N)
- `Members(MemberId, FirstName, LastName, Email, Status, ...)`
- `Loans(LoanId, BookId, MemberId, LoanDate, DueDate, ReturnDate, FineAccrued)`
- `Reservations(ReservationId, BookId, MemberId, ReservedAt, FulfilledAt, CanceledAt, Position)`

## 🗺️ ER Diagram (Mermaid)
```mermaid
erDiagram
  AUTHORS ||--o{ BOOK_AUTHORS : writes
  BOOKS }o--o{ BOOK_AUTHORS : includes
  MEMBERS ||--o{ LOANS : borrows
  BOOKS ||--o{ LOANS : loaned
  MEMBERS ||--o{ RESERVATIONS : requests
  BOOKS ||--o{ RESERVATIONS : reserved
