# Football Ticket Booking System - Database Design

## Project Overview

The Football Ticket Booking System is a relational database designed to manage football match ticket sales. The system stores information about users, football matches, and ticket bookings while maintaining relationships between tables using primary keys and foreign keys.

---

# Database Schema

## Users Table

Stores information about customers and administrative staff who use the platform.

| Field Name   | Description                                                 |
| ------------ | ----------------------------------------------------------- |
| user_id      | Unique identification number for each registered user       |
| full_name    | Stores the first and last name of the user                  |
| email        | Stores the user's email address used for login              |
| role         | Defines access permissions (Ticket Manager or Football Fan) |
| phone_number | Stores the contact mobile number of the user                |

### Sample Data

| user_id | full_name     | email                                     | role           | phone_number   |
| ------- | ------------- | ----------------------------------------- | -------------- | -------------- |
| 1       | Tanvir Rahman | [tanvir@mail.com](mailto:tanvir@mail.com) | Football Fan   | +8801711111111 |
| 2       | Asif Haque    | [asif@mail.com](mailto:asif@mail.com)     | Football Fan   | +8801722222222 |
| 3       | Sajjad Rahman | [sajjad@mail.com](mailto:sajjad@mail.com) | Ticket Manager | +8801733333333 |
| 4       | Jannat Ara    | [jannat@mail.com](mailto:jannat@mail.com) | Football Fan   | NULL           |

---

## Matches Table

Stores information about football matches and ticket pricing.

| Field Name          | Description                                          |
| ------------------- | ---------------------------------------------------- |
| match_id            | Unique identification number for each football match |
| fixture             | Tracks the two competing teams                       |
| tournament_category | League or tournament name                            |
| base_ticket_price   | Standard ticket price                                |
| match_status        | Current ticket availability status                   |

### Sample Data

| match_id | fixture                  | tournament_category | base_ticket_price | match_status |
| -------- | ------------------------ | ------------------- | ----------------- | ------------ |
| 101      | Real Madrid vs Barcelona | Champions League    | 150               | Available    |
| 102      | Man City vs Liverpool    | Premier League      | 120               | Selling Fast |
| 103      | Bayern Munich vs PSG     | Champions League    | 130               | Available    |
| 104      | AC Milan vs Inter Milan  | Serie A             | 90                | Sold Out     |
| 105      | Juventus vs Roma         | Serie A             | 80                | Available    |

---

## Bookings Table

Stores ticket purchase transactions linking users and matches.

| Field Name     | Description                            |
| -------------- | -------------------------------------- |
| booking_id     | Unique booking transaction number      |
| user_id        | References the user making the booking |
| match_id       | References the selected football match |
| seat_number    | Allocated stadium seat number          |
| payment_status | Current payment status                 |
| total_cost     | Final booking amount                   |

### Sample Data

| booking_id | user_id | match_id | seat_number | payment_status | total_cost |
| ---------- | ------- | -------- | ----------- | -------------- | ---------- |
| 501        | 1       | 101      | A-12        | Confirmed      | 150        |
| 502        | 1       | 102      | B-04        | Confirmed      | 120        |
| 503        | 2       | 101      | A-13        | Confirmed      | 150        |
| 504        | 2       | 101      | NULL        | NULL           | 150        |
| 505        | 3       | 102      | C-20        | Pending        | 120        |

---

# Relationships

### Users → Bookings (One-to-Many)

One user can create multiple bookings, while each booking belongs to one user.

### Matches → Bookings (One-to-Many)

One match can have multiple bookings, while each booking is associated with one match.

---

# Keys

### Primary Keys

- Users: user_id
- Matches: match_id
- Bookings: booking_id

### Foreign Keys

- Bookings.user_id → Users.user_id
- Bookings.match_id → Matches.match_id

---

# Features

- User management
- Football match management
- Ticket booking tracking
- Payment status monitoring
- Match availability tracking
- Relational database design using primary and foreign keys
