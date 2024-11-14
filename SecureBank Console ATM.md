import java.util.Scanner;

/*
 * SIMPLE JAVA CODE ATM(MACHINE)PURELY ON JAVA NO DATABASE
 */
public class abankapp {
    Scanner scanner = new Scanner(System.in);
    double customerBalance = 0;
    int customerPin;
    int accountantPin;
    String accountantName;
    int accountantAccountNumber;
    double accountantBalance;
    String accountantBranch;

    static {
        System.out.println("WELCOME TO RV-BANK");
    }

    public void start() {
        System.out.println("SELECT YOUR USER TYPE");
        System.out.println("1: CUSTOMER");
        System.out.println("2: ACCOUNTANT");

        int userType = scanner.nextInt();
        if (userType == 1) {
            customerOperations();
        } else if (userType == 2) {
            accountantOperations();
        } else {
            System.out.println("SELECT A CORRECT OPTION");
        }
    }
    
    // CUSTOMER OPERATIONS
    
    private void customerOperations() {
        int attempts = 3;
        while (attempts > 0) {
            System.out.println("Please Enter Your 4-Digit PIN:");
            customerPin = scanner.nextInt();
            if (customerPin >= 1000 && customerPin < 10000) {
                break;
            } else {
                attempts--;
                System.out.println("ERROR: WRONG PASSWORD. REMAINING ATTEMPTS: " + attempts);
            }
            if (attempts == 0) {
                System.out.println("ACCESS BLOCKED. PLEASE CONTACT BANK SUPPORT.");
                return;
            }
        }
        
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
                    deposit();
                    break;
                case 2:
                    withdraw();
                    break;
                case 3:
                    showBalance();
                    break;
                case 4:
                    System.out.println("THANK YOU, VISIT AGAIN");
                    exit = true;
                    break;
                default:
                    System.out.println("INVALID INPUT. PLEASE CHOOSE A NUMBER BETWEEN 1 AND 4.");
            }
        }
    }

    private void deposit() {
        System.out.println("Enter Amount to Deposit:");
        double depositAmount = scanner.nextDouble();
        if (depositAmount > 0) {
            customerBalance += depositAmount;
            System.out.println("AMOUNT DEPOSITED SUCCESSFULLY. CURRENT BALANCE = " + customerBalance);
        } else {
            System.out.println("PLEASE ENTER A VALID AMOUNT");
        }
    }

    private void withdraw() {
        System.out.println("Enter Amount to Withdraw:");
        double withdrawAmount = scanner.nextDouble();
        if (withdrawAmount > 0 && withdrawAmount <= customerBalance) {
            customerBalance -= withdrawAmount;
            System.out.println("WITHDRAWAL SUCCESSFUL. CURRENT BALANCE = " + customerBalance);
        } else if (withdrawAmount > customerBalance) {
            System.out.println("INSUFFICIENT BALANCE. PLEASE ENTER A VALID AMOUNT.");
        } else {
            System.out.println("PLEASE ENTER A VALID AMOUNT.");
        }
    }
     
    private void showBalance() {
        System.out.println("YOUR BALANCE IS = " + customerBalance);
    }

    // ACCOUNTANT OPERATIONS      

    private void accountantOperations() {
        System.out.println("ENTER YOUR 9-DIGIT ACCOUNT NUMBER:");
        accountantAccountNumber = scanner.nextInt();
        if (accountantAccountNumber < 100000000 || accountantAccountNumber > 999999999) {
            System.out.println("PLEASE ENTER A VALID ACCOUNT NUMBER");
            return;
        }

        System.out.println("ENTER YOUR NAME:");
        accountantName = scanner.next();

        System.out.println("ENTER YOUR BRANCH:");
        accountantBranch = scanner.next();

        int attempts = 3;
        while (attempts > 0) {
            System.out.println("ENTER YOUR 4-DIGIT PIN:");
            accountantPin = scanner.nextInt();
            if (accountantPin >= 1000 && accountantPin < 10000) {
                break;
            } else {
                attempts--;
                System.out.println("ERROR: WRONG PASSWORD. REMAINING ATTEMPTS: " + attempts);
            }
            if (attempts == 0) {
                System.out.println("ACCESS BLOCKED. PLEASE CONTACT BANK SUPPORT.");
                return;
            }
        }

        boolean exit = false;
        while (!exit) {
            System.out.println("---------------");
            System.out.println("Enter Your Choice:");
            System.out.println("1: VIEW DETAILS");
            System.out.println("2: DEPOSIT");
            System.out.println("3: WITHDRAW");
            System.out.println("4: BALANCE");
            System.out.println("5: EXIT");
            System.out.println("---------------");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    viewDetails();
                    break;
                case 2:
                    accountantDeposit();
                    break;
                case 3:
                    accountantWithdraw();
                    break;
                case 4:
                    showAccountantBalance();
                    break;
                case 5:
                    System.out.println("THANK YOU, VISIT AGAIN");
                    exit = true;
                    break;
                default:
                    System.out.println("INVALID INPUT. PLEASE CHOOSE A NUMBER BETWEEN 1 AND 5.");
            }
        }
    }

    private void viewDetails() {
        System.out.println("ACCOUNT HOLDER NAME: " + accountantName);
        System.out.println("ACCOUNT NUMBER: " + accountantAccountNumber);
        System.out.println("ACCOUNT BALANCE: " + accountantBalance);
        System.out.println("BRANCH NAME: " + accountantBranch);
    }

    private void accountantDeposit() {
        System.out.println("Enter Amount to Deposit:");
        double depositAmount = scanner.nextDouble();
        if (depositAmount > 0) {
            accountantBalance += depositAmount;
            System.out.println("AMOUNT DEPOSITED SUCCESSFULLY. CURRENT BALANCE = " + accountantBalance);
        } else {
            System.out.println("PLEASE ENTER A VALID AMOUNT");
        }
    }

    private void accountantWithdraw() {
        System.out.println("Enter Amount to Withdraw:");
        double withdrawAmount = scanner.nextDouble();
        if (withdrawAmount > 0 && withdrawAmount <= accountantBalance) {
            accountantBalance -= withdrawAmount;
            System.out.println("WITHDRAWAL SUCCESSFUL. CURRENT BALANCE = " + accountantBalance);
        } else if (withdrawAmount > accountantBalance) {
            System.out.println("INSUFFICIENT BALANCE. PLEASE ENTER A VALID AMOUNT.");
        } else {
            System.out.println("PLEASE ENTER A VALID AMOUNT.");
        }
    }

    private void showAccountantBalance() {
        System.out.println("YOUR BALANCE IS = " + accountantBalance);
    }

    // MAIN METHOD

    public static void main(String[] args) {
        abankapp atm = new abankapp();
        atm.start();
        atm.scanner.close();
    }
}
