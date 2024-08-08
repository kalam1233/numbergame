import java.util.Scanner;
import java.util.Random;

public class NumberGuessingGame {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        int minRange = 1;
        int maxRange = 100;
        int maxAttempts = 10; // Limiting the number of attempts per round
        
        int totalAttempts = 0;
        int roundsWon = 0;
        
        boolean playAgain = true;
        
        while (playAgain) {
            System.out.println("\n=== New Game ===");
            int secretNumber = random.nextInt(maxRange - minRange + 1) + minRange;
            System.out.println("Guess the number between " + minRange + " and " + maxRange);
            
            int attempts = 0;
            boolean guessedCorrectly = false;
            
            while (attempts < maxAttempts && !guessedCorrectly) {
                System.out.print("Attempt " + (attempts + 1) + "/" + maxAttempts + ": Enter your guess: ");
                int guess = scanner.nextInt();
                
                if (guess < secretNumber) {
                    System.out.println("Too low! Try guessing a higher number.");
                } else if (guess > secretNumber) {
                    System.out.println("Too high! Try guessing a lower number.");
                } else {
                    System.out.println("Congratulations! You guessed the number " + secretNumber + " correctly!");
                    guessedCorrectly = true;
                }
                
                attempts++;
            }
            
            totalAttempts += attempts;
            
            if (guessedCorrectly) {
                roundsWon++;
            } else {
                System.out.println("Sorry, you've run out of attempts. The correct number was " + secretNumber + ".");
            }
            
            System.out.print("Do you want to play again? (yes/no): ");
            String playChoice = scanner.next().toLowerCase();
            
            if (!playChoice.equals("yes")) {
                playAgain = false;
            }
        }
        
        scanner.close();
        
        System.out.println("\nGame over! You played " + roundsWon + " rounds.");
        if (roundsWon > 0) {
            double averageAttempts = (double) totalAttempts / roundsWon;
            System.out.printf("Average attempts per round: %.2f%n", averageAttempts);
        }
    }
}