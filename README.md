import java.io.File;
import java.io.FileNotFoundException;
import java.util.InputMismatchException;
import java.util.Scanner;

public class Q1_ATMExceptionDemo {
    static void withdraw(String accountNumber, int amount, int balance) throws FileNotFoundException {
        // Simulate reading the ATM card-reader configuration file.
        Scanner fileReader = new Scanner(new File("card-reader.txt"));
        fileReader.close();

        if (amount <= 0) {
            throw new IllegalArgumentException("Withdrawal amount must be positive.");
        }
        if (amount > balance) {
            throw new ArithmeticException("Insufficient account balance.");
        }
        System.out.println("Withdrawal successful for account " + accountNumber);
        System.out.println("Cash dispensed: Rs. " + amount);
    }

    public static void main(String[] args) {
        try (Scanner input = new Scanner(System.in)) {
            System.out.print("Enter account number: ");
            String account = input.nextLine();

            System.out.print("Enter withdrawal amount: ");
            int amount = input.nextInt();

            int balance = 5000;
            withdraw(account, amount, balance);

        } catch (InputMismatchException e) {
            System.out.println("Input error: Enter numbers only for the withdrawal amount.");
        } catch (FileNotFoundException e) {
            System.out.println("File error: card-reader.txt is missing.");
        } catch (IllegalArgumentException | ArithmeticException e) {
            System.out.println("Transaction failed: " + e.getMessage());
        } finally {
            System.out.println("ATM session ended. Thank you.");
        }
    }
}
