# LapMart-Manager(Laptop Rental/Seller CRM project)
The LapMart Manager CRM automates the management of laptop rentals, sales, customer interactions, billing, and overdue reminders. This system utilizes Salesforce components such as custom objects, validation rules, flows, Apex classes, and dashboards to streamline rental and sales processes. The goal is to provide an efficient, automated experience for both rentals and purchases, offering timely reminders, inventory tracking, and payment management.
# Objectives
  ### Business Goals
⚪ Automate and streamline the process of renting and selling laptops to customers, reducing manual effort and increasing efficiency.<br>
⚪ Track customer interactions, rental histories, and purchase records to support customer relationship management (CRM).<br>
⚪ Automate billing and reminders for late returns to ensure efficient payment collection and timely laptop returns.<br>
### Specific Outcomes
⚪ A fully functional CRM platform for managing laptop rentals, sales, customer details, and payments.<br>
⚪ Automated billing system with calculated rental fees and late fees.<br>
⚪ Integration of overdue reminders to minimize late returns.<br>
⚪ Tracking of inventory levels, rental/purchase history, and customer profiles for streamlined administration.<br>
# Salesforce Key Features and Concepts Utilized
⚪ Custom Objects: Key objects include Laptop, Customer, Rental, Order, and Payment Process.
⚪ Formula Fields: Used in the Payment Process object to calculate total amounts and handle late fees.
⚪ Automated Workflows: Implemented for overdue rental reminders and automated email notifications based on End Date and payment status.
⚪ Validation Rules: Enforced across the system to ensure accurate data input, such as requiring Rental End Date to follow Rental Start Date.
⚪ Relationships: Lookup fields to manage associations between Laptops, Customers, Rentals, and Payments.
⚪ Apex Triggers: Used for automated tasks such as sending welcome emails and overdue reminders.
