import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class SpellChecker {

    private static List<String> dictionary = new ArrayList<>();

    public static void main(String[] args) {
        loadDictionary("dictionary.txt"); // Load your dictionary file

        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter text to check: ");
        String text = scanner.nextLine();
        scanner.close();

        List<String> misspelledWords = checkSpelling(text);

        if (misspelledWords.isEmpty()) {
            System.out.println("No misspelled words found.");
        } else {
            System.out.println("Misspelled words:");
            for (String word : misspelledWords) {
                System.out.println("- " + word);
            }
        }
    }

    private static void loadDictionary(String dictionaryFile) {
        try (BufferedReader reader = new BufferedReader(new FileReader(dictionaryFile))) {
            String line;
            while ((line = reader.readLine()) != null) {
                dictionary.add(line.trim().toLowerCase());
            }
        } catch (IOException e) {
            System.err.println("Error loading dictionary: " + e.getMessage());
        }
    }

    private static List<String> checkSpelling(String text) {
        List<String> misspelledWords = new ArrayList<>();
        String[] words = text.toLowerCase().split("\\s+"); // Split into words

        for (String word : words) {
            if (!dictionary.contains(word)) {
                misspelledWords.add(word);
            }
        }

        return misspelledWords;
    }
}
