import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Interface for authentication
interface Authenticatable {
    boolean authenticate(int enteredPin);
}

// Abstract class for common attributes and methods
abstract class Person implements Authenticatable {
    private int pin;
    private String name;
    private String branch;

    public Person(int pin, String name, String branch) {
        this.pin = pin;
        this.name = name;
        this.branch = branch;
    }

    public String getName() {
        return name;
    }

    public String getBranch() {
        return branch;
    }

    public boolean authenticate(int enteredPin) {
        return this.pin == enteredPin;
    }
}

// Customer class extending Person
class Customer extends Person {
    private double balance;

    public Customer(int pin, String name, String branch) {
        super(pin, name, branch);
        this.balance = 0.0;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrew: " + amount);
        } else {
            System.out.println("Insufficient balance or invalid amount.");
        }
    }

    public double getBalance() {
        return balance;
    }
}

// Accountant class extending Person
class Accountant extends Person {
    private long employeeId;
    private List<Customer> customers;

    public Accountant(int pin, long employeeId, String name, String branch, List<Customer> customers) {
        super(pin, name, branch);
        this.employeeId = employeeId;
        this.customers = customers;
    }

    public void viewDetails() {
        System.out.println("Accountant Details:");
        System.out.println("Accountant Name: " + getName());
        System.out.println("Employee ID: " + employeeId);
        System.out.println("Branch: " + getBranch());

        System.out.println("Customer Details:");
        for (Customer customer : customers) {
            System.out.println("---------------");
            System.out.println("Name: " + customer.getName());
            System.out.println("Branch: " + customer.getBranch());
            System.out.println("Balance: " + customer.getBalance());
            System.out.println("---------------");
        }
    }

    public void addCustomer(Customer customer) {
        customers.add(customer);
        System.out.println("New customer added successfully.");
    }

    public void deleteCustomer(Customer customer) {
        if (customers.remove(customer)) {
            System.out.println("Customer with name " + customer.getName() + " has been deleted.");
        } else {
            System.out.println("Customer not found.");
        }
    }
}

// Main BankRV class
public class BankRV {
    private Scanner scanner;
    private List<Customer> customers;
    private Accountant accountant;

    public BankRV() {
        scanner = new Scanner(System.in);
        customers = new ArrayList<>();
        accountant = new Accountant(1234, 123456789, "VIRAT KHOLI", "DELHI Branch", customers);
    }

    public void start() {
        boolean continueBanking = true;

        while (continueBanking) {
            System.out.println("WELCOME TO RV-BANK");
            System.out.println("SELECT YOUR USER TYPE");
            System.out.println("1: CUSTOMER");
            System.out.println("2: ACCOUNTANT");
            System.out.println("3: EXIT");

            int userType = scanner.nextInt();
            switch (userType) {
                case 1:
                    customerOperations();
                    break;
                case 2:
                    accountantOperations();
                    break;
                case 3:
                    System.out.println("THANK YOU FOR USING RV-BANK. HAVE A GREAT DAY!");
                    continueBanking = false;
                    break;
                default:
                    System.out.println("SELECT A CORRECT OPTION");
            }
        }
        scanner.close();
    }

    private void customerOperations() {
        System.out.print("Please Enter Your 4-Digit PIN: ");
        int pin = scanner.nextInt();
        Customer customer = findCustomerByPin(pin);

        if (customer != null && customer.authenticate(pin)) {
            System.out.println("Welcome, " + customer.getName() + "!");
            boolean exit = false;
            while (!exit) {
                System.out.println("---------------");
                System.out.println("Enter Your Choice:");
                System.out.println("1: DEPOSIT");
                System.out.println("2: WITHDRAW");
                System.out.println("3: BALANCE");
                System.out.println("4: EXIT");
                System.out.println("---------------");
                int choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        System.out.print("Enter Amount to Deposit: ");
                        double depositAmount = scanner.nextDouble();
                        customer.deposit(depositAmount);
                        break;
                    case 2:
                        System.out.print("Enter Amount to Withdraw: ");
                        double withdrawAmount = scanner.nextDouble();
                        customer.withdraw(withdrawAmount);
                        break;
                    case 3:
                        System.out.println("YOUR BALANCE IS = " + customer.getBalance());
                        break;
                    case 4:
                        System.out.println("THANK YOU, RETURNING TO MAIN MENU");
                        exit = true;
                        break;
                    default:
                        System.out.println("INVALID INPUT. PLEASE CHOOSE A NUMBER BETWEEN 1 AND 4.");
                }
            }
        } else {
            System.out.println("ACCESS BLOCKED. NO USER FOUND. CREATE ACCOUNT.");
        }
    }

    private void accountantOperations() {
        System.out.print("ENTER YOUR 4-DIGIT PIN: ");
        int pin = scanner.nextInt();
        if (accountant.authenticate(pin)) {
            boolean exit = false;
            while (!exit) {
                System.out.println("---------------");
                System.out.println("Enter Your Choice:");
                System.out.println("1: VIEW DETAILS");
                System.out.println("2: ADD CUSTOMER");
                System.out.println("3: DELETE CUSTOMER");
                System.out.println("4: EXIT");
                System.out.println("---------------");
                int choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        accountant.viewDetails();
                        break;
                    case 2:
                        addCustomer();
                        break;
                    case 3:
                        deleteCustomer();
                        break;
                    case 4:
                        System.out.println("THANK YOU, RETURNING TO MAIN MENU");
                        exit = true;
                        break;
                    default:
                        System.out.println("INVALID INPUT. PLEASE CHOOSE A NUMBER BETWEEN 1 AND 4.");
                }
            }
        } else {
            System.out.println("ACCESS BLOCKED. PLEASE CONTACT BANK SUPPORT.");
        }
    }

    private void addCustomer() {
        System.out.println("ADDING A NEW CUSTOMER");

        System.out.print("Please Enter Customer's 4-Digit PIN: ");
        int pin = scanner.nextInt();
        scanner.nextLine();  // consume newline

        System.out.print("Enter Customer's Name: ");
        String name = scanner.nextLine();

        System.out.print("Enter Customer's Branch: ");
        String branch = scanner.nextLine();

        Customer customer = new Customer(pin, name, branch);
        accountant.addCustomer(customer);
    }

    private void deleteCustomer() {
        System.out.println("DELETING A CUSTOMER");
        System.out.print("Please Enter Customer PIN: ");
        int pin = scanner.nextInt();

        Customer customer = findCustomerByPin(pin);
        if (customer != null) {
            accountant.deleteCustomer(customer);
        } else {
            System.out.println("Customer not found.");
        }
    }

    private Customer findCustomerByPin(int pin) {
        for (Customer customer : customers) {
            if (customer.authenticate(pin)) {
                return customer;
            }
        }
        return null;
    }

    public static void main(String[] args) {
        BankRV bank = new BankRV();
        bank.start();
    }
}
