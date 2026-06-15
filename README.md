# Football Ticket Booking System - Database Design & SQL Query Results

## Project Overview

The Football Ticket Booking System is a relational database designed to manage football match ticket sales. The system stores information about users, football matches, and ticket bookings while maintaining relationships through primary and foreign keys.
<br>
<br>
ERD LINK: https://drawsql.app/draw?t=2eb319bc-7d40-4a50-af63-065503742d1f&view=1

---

# Database Schema

## Users Table

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

# Entity Relationships

### Users → Bookings (One-to-Many)

One user can create multiple bookings, while each booking belongs to exactly one user.

### Matches → Bookings (One-to-Many)

One match can have multiple bookings, while each booking belongs to exactly one match.

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

# SQL Query Questions & Results

## Query 1

**Retrieve all upcoming football matches belonging to the 'Champions League' where the match status is 'Available'.**

### Result

| match_id | fixture                  | base_ticket_price |
| -------- | ------------------------ | ----------------- |
| 101      | Real Madrid vs Barcelona | 150               |
| 103      | Bayern Munich vs PSG     | 130               |

---

## Query 2

**Search for all users whose full names start with 'Tanvir' or contain the phrase 'Haque' (case-insensitive).**

### Result

| user_id | full_name     | email                                     |
| ------- | ------------- | ----------------------------------------- |
| 1       | Tanvir Rahman | [tanvir@mail.com](mailto:tanvir@mail.com) |
| 2       | Asif Haque    | [asif@mail.com](mailto:asif@mail.com)     |

---

## Query 3

**Retrieve all booking records where the payment status is missing (NULL), replacing the empty result with 'Action Required'.**

### Result

| booking_id | user_id | match_id | systematic_status |
| ---------- | ------- | -------- | ----------------- |
| 504        | 2       | 101      | Action Required   |

---

## Query 4

**Retrieve match booking details along with the User's full name and the scheduled Match fixture teams.**

### Result

| booking_id | full_name     | fixture                  | total_cost |
| ---------- | ------------- | ------------------------ | ---------- |
| 501        | Tanvir Rahman | Real Madrid vs Barcelona | 150        |
| 502        | Tanvir Rahman | Man City vs Liverpool    | 120        |
| 503        | Asif Haque    | Real Madrid vs Barcelona | 150        |
| 504        | Asif Haque    | Real Madrid vs Barcelona | 150        |
| 505        | Sajjad Rahman | Man City vs Liverpool    | 120        |

---

## Query 5

**Display a comprehensive list of all users and their booking IDs, ensuring that fans who have never bought a ticket are still listed.**

### Result

| user_id | full_name     | booking_id |
| ------- | ------------- | ---------- |
| 1       | Tanvir Rahman | 501        |
| 1       | Tanvir Rahman | 502        |
| 2       | Asif Haque    | 503        |
| 2       | Asif Haque    | 504        |
| 3       | Sajjad Rahman | 505        |
| 4       | Jannat Ara    | NULL       |

---

## Query 6

**Find all ticket bookings where the total cost is strictly higher than the average cost of all ticket bookings.**

### Result

| booking_id | match_id | total_cost |
| ---------- | -------- | ---------- |
| 501        | 101      | 150        |
| 503        | 101      | 150        |
| 504        | 101      | 150        |

---

## Query 7

**Retrieve the top 2 most expensive matches sorted by base ticket price, skipping the absolute highest premium match.**

### Result

| match_id | fixture               | base_ticket_price |
| -------- | --------------------- | ----------------- |
| 103      | Bayern Munich vs PSG  | 130               |
| 102      | Man City vs Liverpool | 120               |

---

# Features

- User Management
- Match Management
- Ticket Booking Tracking
- Payment Status Monitoring
- Match Availability Management
- Relational Database Design using Primary and Foreign Keys
- SQL Query Practice with Filtering, Joins, NULL Handling, and Aggregation
