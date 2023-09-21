# CVIP-Intern
 import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Bank {
    private Map<String, Double> accounts;

    public Bank() {
        accounts = new HashMap<>();
    }

    public void createAccount(String accountNumber, double initialBalance) {
        if (!accounts.containsKey(accountNumber)) {
            accounts.put(accountNumber, initialBalance);
            System.out.println("Account created successfully.");
        } else {
            System.out.println("Account already exists.");
        }
    }

    public void deposit(String accountNumber, double amount) {
        if (accounts.containsKey(accountNumber)) {
            double currentBalance = accounts.get(accountNumber);
            double newBalance = currentBalance + amount;
            accounts.put(accountNumber, newBalance);
            System.out.println("Deposit successful. New balance: " + newBalance);
        } else {
            System.out.println("Account not found.");
        }
    }

    public void withdraw(String accountNumber, double amount) {
        if (accounts.containsKey(accountNumber)) {
            double currentBalance = accounts.get(accountNumber);
            if (currentBalance >= amount) {
                double newBalance = currentBalance - amount;
                accounts.put(accountNumber, newBalance);
                System.out.println("Withdrawal successful. New balance: " + newBalance);
            } else {
                System.out.println("Insufficient funds.");
            }
        } else {
            System.out.println("Account not found.");
        }
    }

    public double getBalance(String accountNumber) {
        if (accounts.containsKey(accountNumber)) {
            return accounts.get(accountNumber);
        } else {
            System.out.println("Account not found.");
            return -1;
        }
    }
}

public class BankingApplication {
    public static void main(String[] args) {
        Bank bank = new Bank();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nBanking Menu:");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Check Balance");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter account number: ");
                    String accountNumber = scanner.nextLine();
                    System.out.print("Enter initial balance: ");
                    double initialBalance = scanner.nextDouble();
                    bank.createAccount(accountNumber, initialBalance);
                    break;
                case 2:
                    System.out.print("Enter account number: ");
                    accountNumber = scanner.nextLine();
                    System.out.print("Enter deposit amount: ");
                    double depositAmount = scanner.nextDouble();
                    bank.deposit(accountNumber, depositAmount);
                    break;
                case 3:
                    System.out.print("Enter account number: ");
                    accountNumber = scanner.nextLine();
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawalAmount = scanner.nextDouble();
                    bank.withdraw(accountNumber, withdrawalAmount);
                    break;
                case 4:
                    System.out.print("Enter account number: ");
                    accountNumber = scanner.nextLine();
                    double balance = bank.getBalance(accountNumber);
                    if (balance >= 0) {
                        System.out.println("Balance: " + balance);
                    }
                    break;
                case 5:
                    System.out.println("Exiting the application.");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
