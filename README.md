import java.util.Scanner;

class Customer {
    private String name;
    private String id;

    public Customer(String name, String id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public String getId() {
        return id;
    }

    @Override
    public String toString() {
        return "Customer Name: " + name + ", ID: " + id;
    }
}

class BankAccount {
    private String accountNumber;
    private double balance;
    private Customer customer;

    public BankAccount(String accountNumber, Customer customer) {
        this.accountNumber = accountNumber;
        this.customer = customer;
        this.balance = 0.0; // Initial balance
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited $" + amount + ". New balance: $" + balance);
        } else {
            System.out.println("Deposit amount must be positive.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0) {
            if (balance >= amount) {
                balance -= amount;
                System.out.println("Withdrew $" + amount + ". New balance: $" + balance);
            } else {
                System.out.println("Insufficient funds. Current balance: $" + balance);
            }
        } else {
            System.out.println("Withdrawal amount must be positive.");
        }
    }

    public void checkBalance() {
        System.out.println("Current balance: $" + balance);
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public Customer getCustomer() {
        return customer;
    }
}

public class BankSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        BankAccount account = null;

        while (true) {
            System.out.println("\nBank System Menu:");
            System.out.println("1. Create a new account");
            System.out.println("2. Deposit money");
            System.out.println("3. Withdraw money");
            System.out.println("4. Check balance");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    if (account == null) {
                        System.out.print("Enter customer name: ");
                        String name = scanner.nextLine();
                        System.out.print("Enter customer ID: ");
                        String id = scanner.nextLine();
                        System.out.print("Enter account number: ");
                        String accNum = scanner.nextLine();
                        Customer customer = new Customer(name, id);
                        account = new BankAccount(accNum, customer);
                        System.out.println("Account created successfully for " + customer);
                    } else {
                        System.out.println("An account already exists.");
                    }
                    break;
                case 2:
                    if (account != null) {
                        System.out.print("Enter deposit amount: ");
                        double depositAmount = scanner.nextDouble();
                        account.deposit(depositAmount);
                    } else {
                        System.out.println("No account found. Please create an account first.");
                    }
                    break;
                case 3:
                    if (account != null) {
                        System.out.print("Enter withdrawal amount: ");
                        double withdrawAmount = scanner.nextDouble();
                        account.withdraw(withdrawAmount);
                    } else {
                        System.out.println("No account found. Please create an account first.");
                    }
                    break;
                case 4:
                    if (account != null) {
                        account.checkBalance();
                    } else {
                        System.out.println("No account found. Please create an account first.");
                    }
                    break;
                case 5:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
}
