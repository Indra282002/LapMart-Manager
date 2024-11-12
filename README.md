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
⚪ Custom Objects: Key objects include Laptop, Customer, Rental, Order, and Payment Process.<br>
⚪ Formula Fields: Used in the Payment Process object to calculate total amounts and handle late fees.<br>
⚪ Automated Workflows: Implemented for overdue rental reminders and automated email notifications based on End Date and payment status.<br>
⚪ Validation Rules: Enforced across the system to ensure accurate data input, such as requiring Rental End Date to follow Rental Start Date.<br>
⚪ Relationships: Lookup fields to manage associations between Laptops, Customers, Rentals, and Payments.<br>
⚪ Apex Triggers: Used for automated tasks such as sending welcome emails and overdue reminders.<br>
## Apex Code for Schedulable Class Overdue Reminder
```java
public class OverdueReminder implements Schedulable {
    // Method called by the scheduler
    public void execute(SchedulableContext sc) {
        sendOverdueReminders();
    }

    // Method to send overdue reminders for laptop rentals
    public static void sendOverdueReminders() {
        List<Rental__c> overdueRentals = [
            SELECT Customer__r.Email__c, Customer__r.Name, Laptop__r.Name, End_Date__c
            FROM Rental__c
            WHERE End_Date__c < :Date.today() 
            AND Return_Date__c = NULL
        ];

        for (Rental__c rental : overdueRentals) {
            // Build the detailed email message
            String customerName = rental.Customer__r.Name;
            String laptopName = rental.Laptop__r.Name;
            Date endDate = rental.End_Date__c;
            
            String messageBody = 'Dear ' + customerName + ',\n\n' +
                                 'This is a reminder that the following laptop you rented is overdue:\n\n' +
                                 'Laptop Model: ' + laptopName + '\n' +
                                 'End Date: ' + String.valueOf(endDate) + '\n\n' +
                                 'Please return the laptop as soon as possible to avoid additional charges.\n\n' +
                                 'Best regards,\nThe LapMart Team';

            // Create the email message
            Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
            mail.setToAddresses(new String[] { rental.Customer__r.Email__c });
            mail.setSubject('Overdue Laptop Reminder for ' + laptopName);
            mail.setPlainTextBody(messageBody);
            Messaging.sendEmail(new Messaging.SingleEmailMessage[] { mail });
        }
    }
}
```

