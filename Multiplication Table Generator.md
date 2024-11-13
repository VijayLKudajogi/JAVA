import java.util.Scanner;

public class Propertable {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.println("Enter a number to generate its multiplication table:");
        int N = scan.nextInt();

        for (int i = 1; i <= 10; i++) {
            System.out.println(N + " x " + i + " = " + (N * i));
        }
        
        scan.close(); // Close the scanner to prevent resource leaks
    }
}
