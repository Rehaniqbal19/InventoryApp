# Inventory Management App – Power Apps & Dataverse

## App Demo:
https://1drv.ms/v/c/2bbcc47d40116a6a/IQChkMWlvwTBR6-Y8z5fnzBKAT_yu5KPAbh7IedejCr7qFE?e=ugvPwS

## Overview

This project is a simple **Inventory Management System** built on the Microsoft Power Platform.  
It uses **Power Apps** (canvas app) for the user interface and **Dataverse** as the central data source.

Users can:

- View all products and their stock levels
- Filter by category
- Search by product name
- Add and edit products
- See how many items are in the catalog and how many are in low stock

The app is designed as a lightweight solution for small teams that need a quick way to track inventory without building a full custom application from scratch.

---

## Problem Statement

A small operations team needs to:

- Maintain a list of products and categories
- Track current stock and reorder thresholds
- Quickly identify which products are at risk of running out

The goal is to prototype an app that business users can access via web or mobile with minimal setup and no traditional coding.

---

## Tools & Technologies

- **Power Apps (Canvas App)** – UI, screens, layout and business logic
- **Microsoft Dataverse** – Central table to store product and inventory data
- **Power Platform Environment / Solutions** – For managing the app and data schema

---

## Data Model – Dataverse Table

The inventory data is stored in a Dataverse table named **`Inventories`**.

Key columns:

- `ProductName` (Text) – Name of the product  
- `Category` (Choice) – Product category (Accessories, Furniture, Electronics, etc.)  
- `ReorderLevel` (Whole Number) – Threshold below which the item is considered low stock  
- `Quantity` (Whole Number) – Current stock on hand  

This single table is used throughout the app for listing, filtering and editing records.

<img width="1918" height="847" alt="image" src="https://github.com/user-attachments/assets/ef427fb2-247f-4ee6-887a-f577e51c13eb" />

---

## App Features

### 1. Product Listing Screen

- Main screen built with a **gallery** bound to `Inventories`.
- Displays a table-like layout with:

  - Product Name  
  - Category  
  - Reorder Level  
  - Quantity
 
<img width="1912" height="983" alt="image" src="https://github.com/user-attachments/assets/29bafd29-de42-43a8-a08e-2b9699332ff0" />


- **Category filter** using a dropdown:

  ```powerfx
  // Gallery Items with category filter
  Filter(
      Inventories,
      DropdownCategory.Selected.Value = "All" ||
      Text(Category) = DropdownCategory.Selected.Value
  )
- **Total products metric**:

  ```powerfx
  CountRows(Gallery2.AllItems)
- **Low stock count (Quantity < ReorderLevel)**:

  ```powerfx
  CountRows(
    Filter(
        Gallery2.AllItems,
        Quantity < 3
    ))
### 2. Search Functionality

A search box filters products by name:
  ```powerfx
  // Gallery Items with search + category filter
  Search(
    If(
        Dropdown1.Selected.Value = "All",
        Inventories,
        Filter(
            Inventories,
            Text(Category) = Dropdown1.Selected.Value
        )
    ),
    Searchbox.Text,
    ProductName)
```
### 3. Add / Edit Product Form

Editable form control connected to `Inventories`.

Variable `varFormMode` controls `New` vs `Edit`. Based on New or Edit, the form input new data or update previous one respectively. Layout of this form page is as follows:

<img width="1915" height="991" alt="image" src="https://github.com/user-attachments/assets/32fd88ba-e21d-4323-a616-2d3afa2de78d" />

---

## Key Learnings

Designing a simple inventory data model in `Dataverse`

Building a functional Power Apps canvas app with:

- Galleries and forms

- Search and filter logic

- Aggregate metrics and low-stock calculations

- Conditional formatting with Power Fx


---

## Conclusion

This project shows on a basic level how quickly an inventory tracking solution can be delivered using the Microsoft Power Platform, without traditional custom development.



  
