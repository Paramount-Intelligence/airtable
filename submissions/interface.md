# Airtable Interface Design

The interface was created to provide a dashboard for HR to monitor new hires and quickly identify high-value employees.

## Interface Layout

The interface contains three main components:

1. Summary Tiles
2. High Value Grid
3. Record Detail View

---

## Summary Tiles

Three number tiles are used to display the count of hires in each category.

High Value Tile  
Filter: Status = High Value

Medium Value Tile  
Filter: Status = Medium Value

Low Value Tile  
Filter: Status = Low Value

These tiles allow HR to quickly understand the distribution of hires based on equipment spending.

---

## High Value Grid View

A filtered grid view is included to display only high-value hires.

Filter applied:

Status = High Value

Fields displayed:

- Full Name
- Cleaned Email
- Amount Spent on Equipment
- Created Date

This allows HR to easily identify and review the most important hires.

---

## Record Detail View

A detail component displays full information about the selected hire.

Fields included:

- Full Name
- Email
- Status
- Amount Spent on Equipment
- Days Since Created

This provides HR with a complete overview of each record without leaving the interface.

---

## Purpose of Interface

The interface provides a centralized dashboard that helps HR:

- Monitor new hires
- Identify high-value employees
- Track hiring activity
- Quickly access detailed information about each hire