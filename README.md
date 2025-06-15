import java.util.ArrayList;
import java.util.Scanner;

public class StudentGrades {
    public static void main(String[] args) {
        // Probably don't need to use Double, but keeping it for flexibility
        ArrayList<Double> enteredGrades = new ArrayList<>();
        Scanner inputScanner = new Scanner(System.in);

        System.out.println("Please enter student grades one by one.");
        System.out.println("(Use a negative number if you're done)");

        boolean isRunning = true;

        // Basic input loop with guard for invalid entries
        while (isRunning) {
            System.out.print("Grade: ");
            double currentGrade = inputScanner.nextDouble();

            if (currentGrade < 0) {
                isRunning = false;
                // Could use break here, but this looks a bit clearer to me
                continue;
            }

            if (currentGrade > 100) {
                System.out.println("Whoa! Grades can't go over 100. Let's try that again.");
                continue;
            }

            enteredGrades.add(currentGrade);
        }

        // Just a quick check before we try to do math
        if (enteredGrades.size() == 0) {
            System.out.println("Looks like you didn’t enter any valid grades.");
            inputScanner.close();
            return;
        }

        // Initializing stuff for calculations
        double total = 0.0;
        double maxGrade = enteredGrades.get(0);  // start assuming the first is the max
        double minGrade = enteredGrades.get(0);  // same for min

        // Looping manually through the list to do calculations
        for (int i = 0; i < enteredGrades.size(); i++) {
            double score = enteredGrades.get(i);
            total += score;

            // Check if this one's the new max or min
            if (score > maxGrade) {
                maxGrade = score;
            }

            if (score < minGrade) {
                minGrade = score;
            }

            // Uncomment if we want to debug each score
            // System.out.println("Processed grade: " + score);
        }

        double averageScore = total / enteredGrades.size();

        // Nicely formatted output
        System.out.printf("Average grade: %.2f\n", averageScore);
        System.out.printf("Top grade: %.2f\n", maxGrade);
        System.out.printf("Lowest grade: %.2f\n", minGrade);

        // Always close what we open
        inputScanner.close();
    }
}
