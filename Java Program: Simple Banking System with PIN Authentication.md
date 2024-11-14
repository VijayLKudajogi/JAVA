import java.util.Scanner;

public class atm {
    Scanner scanner = new Scanner(System.in);
    double balance = 0;
    int pin;

    static {
        System.out.println("WELCOME TO RV-BANK");
    }

    public void start() {
        // Allow user 3 attempts to enter the correct PIN
        int attempts = 3;
        while (attempts > 0) {
            System.out.println("Enter PIN:");
            pin = scanner.nextInt();

            if (pin < 1000 || pin >= 10000) {
                attempts--;
                System.out.println("ERROR: WRONG PASSWORD. Remaining attempts: " + attempts);
                if (attempts == 0) {
                    System.out.println("ACCESS BLOCKED. PLEASE CONTACT BANK SUPPORT.");
                    return; // Exit if attempts are exhausted
                }
            } else {
                break; // Correct PIN, exit the loop
            }
        }

        boolean exit = false;
        while (!exit) {
            System.out.println("Enter the Choice:");
            System.out.println("1: DEPOSIT");
            System.out.println("2: WITHDRAW");
            System.out.println("3: BALANCE");
            System.out.println("4: EXIT");
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
                    System.out.println("INVALID INPUT");
            }
        }
    }

    private void deposit() {
        System.out.println("Enter amount to deposit:");
        double depositAmount = scanner.nextDouble();
        if (depositAmount > 0) {
            balance += depositAmount;
            System.out.println("AMOUNT DEPOSITED SUCCESSFULLY. CURRENT BALANCE = " + balance);
        } else {
            System.out.println("PLEASE ENTER A VALID AMOUNT");
        }
    }

    private void withdraw() {
        System.out.println("Enter amount to withdraw:");
        double withdrawAmount = scanner.nextDouble();
        if (withdrawAmount > 0 && withdrawAmount <= balance) {
            balance -= withdrawAmount;
            System.out.println("WITHDRAWAL SUCCESSFUL. CURRENT BALANCE = " + balance);
        } else if (withdrawAmount > balance) {
            System.out.println("INSUFFICIENT BALANCE. PLEASE ENTER A VALID AMOUNT.");
        } else {
            System.out.println("PLEASE ENTER A VALID AMOUNT.");
        }
    }

    private void showBalance() {
        System.out.println("YOUR BALANCE IS = " + balance);
    }

    public static void main(String[] args) {
        atm bankApp = new atm();
        bankApp.start();
    }
}
