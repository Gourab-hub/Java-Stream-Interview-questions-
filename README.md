# Java-Stream-Interview-questions-

1. Java stream string to char count

import java.util.*;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        String str = "programming";

        Map<Character, Long> map = str.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(
                        Function.identity(),
                        Collectors.counting()
                ));

        System.out.println(map);
    }
}



2. first non-repeating character using Java Streams

import java.util.*;
import java.util.function.Function;
import java.util.stream.Collectors;

class Solution {
    public static Character firstNonRepeating(String s) {

        Map<Character, Long> map = s.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(
                        Function.identity(),
                        LinkedHashMap::new,
                        Collectors.counting()
                ));

        return map.entrySet()
                .stream()
                .filter(entry -> entry.getValue() == 1)
                .map(Map.Entry::getKey)
                .findFirst()
                .orElse(null);
    }

    public static void main(String[] args) {
        System.out.println(firstNonRepeating("programming")); // p
    }
}

3. count character frequency from a string using Java streams,

import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {

        String name = "Gourab Banik";

        Map<Character, Long> charCountMap =
                name.toLowerCase()
                    .chars()                    // IntStream of characters
                    .mapToObj(c -> (char) c)    // convert int to Character
                    .filter(c -> c != ' ')      // ignore spaces
                    .collect(Collectors.groupingBy(
                            c -> c,
                            Collectors.counting()
                    ));

        System.out.println(charCountMap);
    }
}

Or 

import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {

        String name = "Gourab Banik";

        Map<Character, Long> charCountMap =
                Arrays.stream(name.split(" "))   // split by space
                      .map(String::toLowerCase)  // lowercase each word
                      .flatMap(word ->
                              word.chars().mapToObj(c -> (char) c)
                      )
                      .collect(Collectors.groupingBy(
                              c -> c,
                              Collectors.counting()
                      ));

        System.out.println(charCountMap);
    }
}

4. Sort distinct number using stream

import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {

        int[] arr = {5, 3, 1, 2, 3, 5, 4, 2};

        List<Integer> result =
                Arrays.stream(arr)
                      .distinct()
                      .sorted()
                      .boxed()
                      .collect(Collectors.toList());

        System.out.println("Sorted Distinct Numbers:");
        System.out.println(result);
    }
}

5. Reverse Order


import java.util.*;
import java.util.stream.*;

public class Main {

    public static void main(String[] args) {

        int[] arr = {5, 3, 1, 2, 3, 5, 4, 2};

        List<Integer> result =
                Arrays.stream(arr)          // IntStream
                      .boxed()              // convert int -> Integer
                      .distinct()           // remove duplicates
                      .sorted(Comparator.reverseOrder()) // sort descending
                      .collect(Collectors.toList());

        System.out.println("Reverse Sorted Distinct Numbers:");
        System.out.println(result);
    }
}

6. filter even numbers from a list using the Stream API and Lambdas

public class FilterEvenNumbers {
    public static void main(String[] args) {
        
        // 1. Create a list of integers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 24);

        // 2. Use Stream API to filter even numbers
        List<Integer> evenNumbers = numbers.stream()
            .filter(n -> n % 2 == 0)      // Lambda condition for even numbers
            .collect(Collectors.toList()); // Collect results back into a list

        // 3. Print the result
        System.out.println("Even Numbers: " + evenNumbers);
    }
}

7. convert a list of strings to uppercase using the Java 8 Stream API

public class ConvertToUppercase {
    public static void main(String[] args) {
        // Create the initial list
        List<String> words = Arrays.asList("Java", "spring", "Oracle");

        // Convert each string to uppercase using Stream API
        List<String> upperWords = words.stream()
            .map(String::toUpperCase)     // Transformation step
            .collect(Collectors.toList()); // Collection step

        // Print the result
        System.out.println(upperWords); // Output: [JAVA, SPRING, ORACLE]
    }
}

8. maximum value in a list of integers using the Java 8 Stream API.

   public class MaxValueFinder {
    public static void main(String[] args) {
        // 1. Initialize the list
        List<Integer> numbers = Arrays.asList(10, 50, 30, 45, 88);

        // 2. Find max value using Stream API
        Optional<Integer> maxValue = numbers.stream()
            .max(Integer::compareTo); // Compare elements to find the largest

        // 3. Print the result
        // The Optional will print as Optional[88]
        System.out.println("Maximum Value: " + maxValue);
        
        // To get just the number, you can use:
        // maxValue.ifPresent(max -> System.out.println("Max is: " + max));
    }
}

9. group a list of strings by their character length using the Java 8 Stream API

public class GroupByStringLength {
    public static void main(String[] args) {
        // 1. Create a list of strings
        List<String> words = Arrays.asList("Apple", "Banana", "Pear", "Grape", "Kiwi", "Orange");

        // 2. Group strings by their length using Stream API
        Map<Integer, List<String>> groupedByLength = words.stream()
            .collect(Collectors.groupingBy(String::length));

        // 3. Print the resulting map
        System.out.println(groupedByLength);
        // Output:
        // {4=[Pear, Kiwi], 5=[Apple, Grape], 6=[Banana, Orange]}
        
    }
}

10. filter a list of strings to find words starting with the letter 'A' (both uppercase and lowercase) using the Java 8 Stream API.

public static void main(String[] args) {
        // 1. Create a list of words
        List<String> words = Arrays.asList("Amit", "Saurav", "Animesh", "Vikram", "Apple", "Banana", "Kiwi");

        // 2. Filter words starting with 'A' or 'a'
        List<String> startingWithA = words.stream()
            .filter(s -> s.startsWith("A") || s.startsWith("a"))
            .collect(Collectors.toList());

        // 3. Print the result using if-else logic
        if (!startingWithA.isEmpty()) {
            System.out.println("Words starting with A or a: " + startingWithA);
        } else {
            System.out.println("No words starting with A or a found.");
        }
        
        // Output:
        // Words starting with A or a: [Amit, Animesh, Apple]
    }

11. find duplicate elements in a list using the Java 8 Stream API.

import java.util.*;
import java.util.stream.Collectors;

public class FindDuplicates {
    public static void main(String[] args) {
        // 1. Create a list with duplicate numbers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 3, 4, 7, 8, 6);

        // 2. Use a Set to track seen elements
        Set<Integer> seen = new HashSet<>();

        // 3. Filter the stream for duplicates
        List<Integer> duplicates = numbers.stream()
            .filter(n -> !seen.add(n) na) // If add returns false, it's a duplicate
            .distinct()               // Ensure each duplicate is only listed once
            .collect(Collectors.toList());

        // 4. Print the result
        System.out.println("Duplicate Elements: " + duplicates);
        
        // Output:
        // Duplicate Elements: [3, 4, 6]
    }
}

12.  remove null values from a list of strings using the Java 8 Stream API.

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class RemoveNullValues {
    public static void main(String[] args) {
        // 1. Create a list containing strings and null values
        List<String> words = Arrays.asList("Apple", null, "Banana", null, "Grape", "Kiwi", null);

        // 2. Filter out null values using Stream API
        List<String> nonNullWords = words.stream()
            .filter(word -> word != null) // Keep only non-null elements
            .collect(Collectors.toList());

        // 3. Print the result
        System.out.println("List after removing nulls: " + nonNullWords);
        
        // Output: // List after removing nulls: [Apple, Banana, Grape, Kiwi]
    }
}

13. flatten a list of lists into a single list of integers using the Java 8 Stream API.

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FlattenList {
    public static void main(String[] args) {
        // 1. Create individual lists
        List<Integer> list1 = Arrays.asList(1, 2, 3);
        List<Integer> list2 = Arrays.asList(4, 5, 6);
        List<Integer> list3 = Arrays.asList(7, 8, 9);

        // 2. Create a list of lists
        List<List<Integer>> listOfLists = Arrays.asList(list1, list2, list3);

        // 3. Flatten the list of lists using flatMap
        List<Integer> flattenedList = listOfLists.stream()
            .flatMap(List::stream)         // Flatten inner lists into a single stream
            .collect(Collectors.toList()); // Collect results into one list

        // 4. Print the result
        System.out.println("Flattened List: " + flattenedList);
        
        // Output:
        // Flattened List: [1, 2, 3, 4, 5, 6, 7, 8, 9]
    }
}


14. partition numbers into even and odd lists using the Java 8 Stream API

public class PartitionByEvenOdd {
    public static void main(String[] args) {
        // 1. Create a list of numbers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // 2. Partition numbers into even and odd
        Map<Boolean, List<Integer>> partitioned = numbers.stream()
            .collect(Collectors.partitioningBy(n -> n % 2 == 0));

        // 3. Extract and print the results
        List<Integer> evenList = partitioned.get(true);
        List<Integer> oddList = partitioned.get(false);

        System.out.println("Even List: " + evenList);
        System.out.println("Odd List: " + oddList);
        
        // Output:
        // Even List: [2, 4, 6, 8, 10]
        // Odd List: [1, 3, 5, 7, 9]
    }
}

15. frequency of elements (the number of times each word appears) in a list using the Java 8 Stream API.

public class WordFrequency {
    public static void main(String[] args) {
        // 1. Create a list of words with repetitions
        List<String> words = Arrays.asList("apple", "banana", "apple", "orange", "banana", "banana");

        // 2. Create a frequency map using Stream API
        Map<String, Long> frequencyMap = words.stream()
            .collect(Collectors.groupingBy(
                word -> word,           // Group by the word itself
                Collectors.counting()    // Count occurrences in each group
            ));

        // 3. Print the resulting map
        System.out.println("Element Frequencies: " + frequencyMap);
        
        // Output: // Element Frequencies: {orange=1, banana=3, apple=2}
    }
}

16. merge two lists into a single list using the Java 8 Stream API.

public class MergeLists {
    public static void main(String[] args) {
        // 1. Create two lists
        List<String> list1 = Arrays.asList("apple", "banana", "grape");
        List<String> list2 = Arrays.asList("orange", "kiwi", "pear");

        // 2. Merge lists using Stream.concat
        List<String> mergedList = Stream.concat(list1.stream(), list2.stream())
                                        .collect(Collectors.toList());

        // 3. Print the result
        System.out.println("Merged List: " + mergedList);
        
        // Output:
        // Merged List: [apple, banana, grape, orange, kiwi, pear]
    }
}

17. convert a list of integers into their square values using the Java 8 Stream API.

public class SquareList {
    public static void main(String[] args) {
        // 1. Create a list of integers
        List<Integer> numbers = Arrays.asList(2, 3, 4, 5, 6);

        // 2. Convert each number to its square using Stream API
        List<Integer> squareNumbers = numbers.stream()
            .map(n -> n * n)               // Transform each element: n squared
            .collect(Collectors.toList()); // Collect into a new list

        // 3. Print the result
        System.out.println("Squared Numbers: " + squareNumbers);
        
        // Output:
        // Squared Numbers: [4, 9, 16, 25, 36]
    }
}

18.  remove duplicate words from a list using the Java 8 Stream API.

    public class RemoveDuplicateWords {
    public static void main(String[] args) {
        // 1. Create a list with duplicate words
        List<String> words = Arrays.asList("apple", "banana", "apple", "orange");

        // 2. Remove duplicates using the distinct() method
        List<String> uniqueWords = words.stream()
            .distinct()                    // Keep only unique elements
            .collect(Collectors.toList()); // Collect into a new list

        // 3. Print the result
        System.out.println("Unique Words: " + uniqueWords);
        
        // Output:
        // Unique Words: [apple, banana, orange]
    }
}

19. first element of a list using the Java 8 Stream API.

    public class FirstElementFinder {
    public static void main(String[] args) {
        // 1. Create a list of words
        List<String> words = Arrays.asList("apple", "banana", "orange", "kiwi");

        // 2. Find the first element using findFirst()
        // findFirst() returns an Optional to handle empty list cases safely
        Optional<String> firstWord = words.stream().findFirst();

        // 3. Print the result if it exists
        firstWord.ifPresent(word -> System.out.println("First element: " + word));
        
        // Output:
        // First element: apple
    }
}

20. sum of all elements in a list of integers using the Java 8 Stream API.

    public class SumOfElements {
    public static void main(String[] args) {
        // 1. Create a list of integers
        List<Integer> numbers = Arrays.asList(2, 4, 6, 8, 10);

        // 2. Convert to IntStream and calculate sum
        int sum = numbers.stream()
            .mapToInt(Integer::intValue) // Unbox Integer to primitive int
            .sum();                      // Terminal operation to sum values

        // 3. Print the result
        System.out.println("Sum: " + sum);
        
        // Output:
        // Sum: 30
    }
}

Or

public class SumWithReducer {
    public static void main(String[] args) {
        // 1. Create a list of integers
        List<Integer> numbers = Arrays.asList(2, 4, 6, 8, 10);

        // 2. Calculate sum using reduce
        // 0 is the identity (starting value)
        // (a, b) -> a + b is the accumulator (adds each element to the running total)
        int sum = numbers.stream()
            .reduce(0, (a, b) -> a + b);

        // Alternatively, using a method reference:
        // int sum = numbers.stream().reduce(0, Integer::sum);

        // 3. Print the result
        System.out.println("Sum using Reducer: " + sum);
        
        // Output:
        // Sum using Reducer: 30
    }
}

21. Java 8 Stream API Interview Questions: Find Longest String in List Java 8 Stream API

public class LongestStringLengt {
    public static void main(String[] args) {
        // Initializing a list of strings 
        List<String> list = Arrays.asList("Apple", "Banana", "Grapefruit", "Kiwi");

        // Using Java 8 Stream API to find the maximum length 
        int longStrLength = list.stream()
                .mapToInt(String::length) // Mapping each string to its length
                .max()                    // Finding the maximum value
                .orElse(0);               // Returning 0 if the list is empty

        // Printing the result [00:03:23]
        System.out.println("Longest string length: " + longStrLength);
        
        // Output: Longest string length: 10
    }
}

22. Find the Second Highest Element in List using the Java 8

public class SecondHighestElement {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(3, 8, 15, 10, 12, 25, 7);

        // Using Java 8 Stream API to find the second highest element
        Optional<Integer> secondHighestNum = numbers.stream()
                .sorted((a, b) -> b.compareTo(a)) // Sort in descending order
                .skip(1)                         // Skip the first (highest) element
                .findFirst();                    // Get the next element (second highest)

        // Printing the result if present
        secondHighestNum.ifPresent(System.out::println);
        
        // Output: 15
    }
}

23. Java 8 Stream API Interview Questions: Collect Odd Numbers into Set Using Java 8 Stream API

public class CollectOddNumbersToSet {
    public static void main(String[] args) {
        // Initializing a list of integers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Using Java 8 Stream API to filter odd numbers and collect them into a Set
        Set<Integer> oddNumbers = numbers.stream()
                .filter(n -> n % 2 != 0)     // Filter condition for odd numbers
                .collect(Collectors.toSet()); // Collecting the result into a Set

        // Printing the result
        System.out.println(oddNumbers);
        
        // Output: [1, 3, 5, 7, 9]
    }
}

24. Check if All Elements in a List are Positive in Java 8 Stream

public class AllPositiveCheck {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(5, 12, 18, 7, 28, 21);

        // Using Java 8 Stream API to check if all elements are positive
        boolean allPositive = numbers.stream()
                .allMatch(n -> n > 0); // Condition to check if number is greater than 0

        // Printing the result
        System.out.println("All positive? " + allPositive);
        
        // Scenario 1 Output: All positive? true
        
        // Scenario 2: Changing 12 to -12
        // List<Integer> numbersWithNegative = Arrays.asList(5, -12, 18, 7, 28, 21);
        // boolean allPositiveFalse = numbersWithNegative.stream().allMatch(n -> n > 0);
        // Output for Scenario 2: All positive? false
    }
}

25. Skip Elements in Java List with Stream API Java 8

public class SkipFirstThreeElements {
    public static void main(String[] args) {
        // Initializing a list of strings
        List<String> words = Arrays.asList("Apple", "Banana", "Orange", "Grape", "Kiwi");

        // Using Java 8 Stream API to skip the first three elements
        List<String> newList = words.stream()
                .skip(3)                   // Skips "Apple", "Banana", and "Orange"
                .collect(Collectors.toList());

        // Printing the result
        System.out.println(newList);
        
        // Output: [Grape, Kiwi]
    }
}


26.  Check if No Elements in List are Negative Using Java 8 Stream


public class NegativeNumbers {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(1, 5, 10, 15);

        // Using Java 8 Stream API to check if NO elements are negative
        boolean noNegativeNumber = numbers.stream()
                .noneMatch(n -> n < 0); // Condition: none of the numbers are less than 0

        // Printing the result
        System.out.println("No negative numbers: " + noNegativeNumber);
        
        // Scenario 1 Output: No negative numbers: true
        
        // Scenario 2: If we change one number to negative (e.g., -5)
        // Output for Scenario 2: No negative numbers: false
    }
}

27. Find the Smallest Element in a List Using Java 8 Stream API

public class FindMinimum {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(12, 45, 23, 5, 87, 9, 19);

        // Using Java 8 Stream API to find the minimum value
        Optional<Integer> min = numbers.stream()
                .min(Integer::compareTo); // Comparing elements to find the smallest

        // Printing the result if a value is present
        min.ifPresent(value -> System.out.println("Minimum number is: " + value));
        
        // Output: Minimum number is: 5
    }
}


28. Find Average Of Integer from List using the Java 8 Stream API

public class AverageOfList {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        // Using Java 8 Stream API to calculate the average
        double average = numbers.stream()
                .mapToInt(Integer::intValue) // Unboxing Integer to int
                .average()                   // Calculating the average
                .orElse(0.0);                // Default value if list is empty

        // Printing the result
        System.out.println("Average: " + average);
        
        // Output: Average: 3.5
    }
}

29. Filter Strings Containing a Specific Character from List

public class FilterStringsByCharacter {
    public static void main(String[] args) {
        // Initializing the list of strings
        List<String> words = Arrays.asList("apple", "banana", "grape", "kiwi", "orange");

        // Using Java 8 Stream API to filter words containing the character 'a'
        List<String> filteredWords = words.stream()
                .filter(word -> word.contains("a")) // Logic: check if word contains 'a'
                .collect(Collectors.toList());      // Collect results into a new list

        // Printing the result
        System.out.println(filteredWords);
        
        // Output with 'a': [apple, banana, grape, orange]
    }
}

30. Concatenate a List of Strings from List using Java 8 Stream

public class ConcatenateStrings {
    public static void main(String[] args) {
        // Initializing a list of strings
        List<String> words = Arrays.asList("Apple", "Banana", "Orange");

        // Using Java 8 Stream API to concatenate strings with a comma and space
        String concatenatedString = words.stream()
                .collect(Collectors.joining(", ")); // Joining strings with delimiter

        // Printing the result
        System.out.println(concatenatedString);
        
        // Output: Apple, Banana, Orange
    }
}

31. Collect Prime Numbers from a List using Java 8 Stream API

public class PrimeNumberCollector {
    
    // Method to check if a number is prime
    public static boolean isPrime(int num) {
        if (num <= 1) return false;
        if (num == 2) return true; // Special case for 2
        
        // Loop from 2 up to the square root of the number
        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) {
                return false; // Not a prime number
            }
        }
        return true; // Is a prime number
    }

    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Using Java 8 Stream API to filter prime numbers
        List<Integer> primeNumbers = numbers.stream()
                .filter(PrimeNumberCollector::isPrime) // Using method reference to filter
                .collect(Collectors.toList());        // Collecting result into a list

        // Printing the result
        System.out.println("Prime numbers: " + primeNumbers);
        
        // Output: Prime numbers: [2, 3, 5, 7]
    }
}


32. Sort List of Strings by Length from List using Stream API

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class SortByStringLength {
    public static void main(String[] args) {
        // Initializing the list of strings
        List<String> words = Arrays.asList("apple", "banana", "kiwi", "orange", "grape");

        // Using Java 8 Stream API to sort strings by their length
        List<String> sortedByLength = words.stream()
                .sorted((s1, s2) -> Integer.compare(s1.length(), s2.length())) // Custom comparator
                .collect(Collectors.toList());

        // Printing the result
        System.out.println("Sorted words by length: " + sortedByLength);
        
        // Output: Sorted words by length: [kiwi, apple, grape, orange, banana]
    }
}

33. Calculate Product of All Elements in List using Stream API

public class ProductOfList {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Using Java 8 Stream API to calculate the product of all elements
        int product = numbers.stream()
                .reduce(1, (a, b) -> a * b); // Initial value 1, then multiplying a * b

        // Printing the result
        System.out.println("Product: " + product);
        
        // Output: Product: 120
    }
}


34. Find the Second smallest element in a list using Stream API

public class SecondSmallest {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(3, 7, 2, 5, 9, 1, 6);

        // Using Java 8 Stream API to find the second smallest element
        Optional<Integer> secondSmallest = numbers.stream()
                .sorted()             // Step 1: Sort in ascending order (default)
                .skip(1)              // Step 2: Skip the first (smallest) element
                .findFirst();         // Step 3: Get the next element

        // Printing the result if present
        secondSmallest.ifPresent(System.out::println);
        
        // Output: 2
    }
}

35. Find Palindromic Strings in a List using Stream API

public class PalindromicString {
    public static void main(String[] args) {
        // Initializing the list of strings
        List<String> words = Arrays.asList("madam", "apple", "racecar", "banana", "level");

        // Using Java 8 Stream API to filter palindromic strings
        List<String> palindromes = words.stream()
                .filter(word -> word.equals(new StringBuilder(word).reverse().toString()))
                .collect(Collectors.toList());

        // Printing the result
        System.out.println("Palindromic words: " + palindromes);
        
        // Output: Palindromic words: [madam, racecar, level]
    }
}

36. Convert a List of Strings to a Set using Stream API in java 8

public class ConvertListToSet {
    public static void main(String[] args) {
        // Initializing a list of strings with duplicate elements
        List<String> words = Arrays.asList("apple", "banana", "grape", "orange", "banana");

        // Approach 1: Using the HashSet Constructor (as shown in the video)
        Set<String> wordSet = new HashSet<>(words);

        // Approach 2: Using Java 8 Stream API (Alternative for similar tasks)
        // Set<String> wordSetStream = words.stream().collect(Collectors.toSet());

        // Printing the result
        System.out.println("Word Set: " + wordSet);
        
        // Output: [banana, orange, apple, grape] (Order may vary)
    }
}

37. Find the Median Value in a List of Integers using Stream API

public class MedianValue {
    public static void main(String[] args) {
        // Initializing the list of integers
        List<Integer> numbers = Arrays.asList(1, 3, 5, 7, 9);

        // Step 1: Sort the numbers in ascending order using Stream API
        List<Integer> sortedNumbers = numbers.stream()
                .sorted()
                .collect(Collectors.toList());

        int size = sortedNumbers.size();
        double median;

        // Step 2: Calculate median based on whether the size is even or odd
        if (size % 2 == 0) {
            // Even size: Average of the two middle elements
            median = (sortedNumbers.get(size / 2 - 1) + sortedNumbers.get(size / 2)) / 2.0;
        } else {
            // Odd size: The middle element
            median = sortedNumbers.get(size / 2);
        }

        // Printing the result
        System.out.println("Median: " + median);
        
        // Output for [1, 3, 5, 7, 9]: Median: 5.0
        // Output for [1, 3, 5, 7, 9, 11]: Median: 6.0
    }
}

38. Generate List of First 10 Fibonacci Numbers using Stream API

public class FibonacciNumber {
    public static void main(String[] args) {
        int termNumber = 10; // Number of Fibonacci elements to generate

        // Using Java 8 Stream API to generate the Fibonacci series
        List<Integer> fibonacciNumbers = Stream.iterate(new int[]{0, 1}, t -> new int[]{t[1], t[0] + t[1]})
                .limit(termNumber)         // Limiting to first 10 terms
                .map(t -> t[0])            // Extracting the first element of each pair
                .collect(Collectors.toList());

        // Printing the result
        System.out.println(fibonacciNumbers);
        
        // Output for termNumber = 10: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
    }
}


39.  Count Palindromes in a List using Stream API in Java

public class CountPalindromes {
    public static void main(String[] args) {
        // Initializing the list of strings
        List<String> words = Arrays.asList("madam", "apple", "racecar", "banana", "level");

        // Using Java 8 Stream API to count palindromic strings
        long count = words.stream()
                .filter(word -> word.equals(new StringBuilder(word).reverse().toString())) // Check if palindrome
                .count(); // Count the filtered results

        // Printing the result
        System.out.println("Number of palindromes: " + count);
        
        // Output: Number of palindromes: 3
    }
}

40. Find All Subsets of a List using Stream API Java 8

public class AllSubsets {
    public static void main(String[] args) {
        // Initializing the input list
        List<Integer> list = Arrays.asList(1, 2, 3);

        // List of lists to store all subsets
        List<List<Integer>> subsets = new ArrayList<>();
        
        // Step 1: Add the empty set to the list of subsets
        subsets.add(new ArrayList<>());

        // Step 2: Iterate through each element in the input list
        for (Integer element : list) {
            // Temporary list to store new subsets generated in this iteration
            List<List<Integer>> newSubsets = new ArrayList<>();
            
            // For every existing subset, create a new one by adding the current element
            for (List<Integer> subset : subsets) {
                List<Integer> newSubset = new ArrayList<>(subset);
                newSubset.add(element);
                newSubsets.add(newSubset);
            }
            
            // Add all newly created subsets to the main list
            subsets.addAll(newSubsets);
        }

        // Printing the result
        System.out.println("All Subsets: " + subsets);
        
        // Output for [1, 2, 3]: [[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]
    }
}


41. Reverse a List of Strings using Stream API

public class ReverseListStream {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "orange", "grape", "kiwi");

        // Stream API logic to reverse the list
        List<String> reverseWords = words.stream()
                .collect(Collectors.collectingAndThen(Collectors.toList(), list -> {
                    Collections.reverse(list);
                    return list;
                }));

        System.out.println("Reversed (Stream): " + reverseWords);
        // Output: [kiwi, grape, orange, banana, apple]
    }
}

42. Count Number of Characters in a List of Strings using Stream

public class CountCharacters {
    public static void main(String[] args) {
        // Initializing the list of strings
        List<String> words = Arrays.asList("apple", "banana", "orange", "grape");

        // Using Java 8 Stream API to count total characters
        int totalCharacters = words.stream()
                .mapToInt(String::length) // Convert each string to its length (int)
                .sum();                   // Sum all lengths

        // Printing the result
        System.out.println("Total number of characters: " + totalCharacters);
        
        // Output for ["apple", "banana", "orange", "grape"]: 22
    }
}


43. Find the First Non Repeated Character in String using Streams

public class FirstNonRepeatedCharacter {
    public static void main(String[] args) {
        String input = "saurabh"; // Sample input

        // Step 1: Count character occurrences while preserving order using LinkedHashMap
        Map<Character, Integer> characterCount = new LinkedHashMap<>();
        for (char c : input.toCharArray()) {
            characterCount.put(c, characterCount.getOrDefault(c, 0) + 1);
        }

        // Step 2: Use Stream API to find the first character with a count of 1
        characterCount.entrySet().stream()
                .filter(entry -> entry.getValue() == 1) // Keep only non-repeated characters
                .map(Map.Entry::getKey)                 // Extract the character
                .findFirst()                           // Get the first one in the map
                .ifPresent(System.out::println);       // Print the result

        // Output for "saurabh": s
    }
}


or 

public class FirstNonRepeatedCharacter {
    public static void main(String[] args) {
        String input = "saurabh";

        input.chars() // Returns an IntStream of characters
            .mapToObj(c -> (char) c) // Convert int to Character
            .collect(Collectors.groupingBy(
                Function.identity(), 
                LinkedHashMap::new, // Maintains insertion order
                Collectors.counting()
            ))
            .entrySet().stream()
            .filter(entry -> entry.getValue() == 1)
            .map(Map.Entry::getKey)
            .findFirst()
            .ifPresent(System.out::println);
            
        // Output: s
    }
}

44. Count Occurrences of Each Element in a List using Streams API

public class CountOccurrences {
    public static void main(String[] args) {
        // Initializing the list with repeating strings
        List<String> words = Arrays.asList("apple", "banana", "apple", "grape", "banana", "orange", "banana");

        // Approach 1: Resulting in a Map<String, Long>
        Map<String, Long> occurrencesLong = words.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));

        // Approach 2: Resulting in a Map<String, Integer> using collectingAndThen
        Map<String, Integer> occurrencesInt = words.stream()
                .collect(Collectors.groupingBy(
                        Function.identity(),
                        Collectors.collectingAndThen(Collectors.counting(), Long::intValue)
                ));

        // Printing results
        System.out.println("Occurrences (Long): " + occurrencesLong);
        System.out.println("Occurrences (Integer): " + occurrencesInt);
        
        // Output: {orange=1, banana=3, apple=2, grape=1}
    }
}

45. identifies how many times each character appears while keeping them in order

public class CharGroup {
    public static void main(String[] args) {
        String input = "saurabh";

        Map<Character, Long> counts = input.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(
                Function.identity(), 
                LinkedHashMap::new, 
                Collectors.counting()
            ));

        System.out.println(counts);
        // Output: {s=1, a=2, u=1, r=1, b=1, h=1}
    }
}



46. Check If a List Contains a Sub-list using Java 8 Streams API

public class CheckSubList {
    public static void main(String[] args) {
        // Main list and the sub-list to search for
        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6);
        List<Integer> subList = Arrays.asList(3, 4, 5);

        // logic to check if subList exists within list
        boolean containsSubList = IntStream.rangeClosed(0, list.size() - subList.size())
                .anyMatch(i -> list.subList(i, i + subList.size()).equals(subList));

        // Result
        System.out.println("Contains sub-list: " + containsSubList);
        
        // Output for [1,2,3,4,5,6] and [3,4,5]: true
    }
}

47. Find Common Elements Between Two Lists using Java 8 Streams

public class FindCommonElements {
    public static void main(String[] args) {
        // Defining the two lists
        List<String> list1 = Arrays.asList("apple", "banana", "grape", "orange");
        List<String> list2 = Arrays.asList("banana", "grape", "kiwi");

        // Using Stream API to find common elements
        Set<String> commonElements = list1.stream()
                .filter(list2::contains)  // Keep elements that are also present in list2
                .collect(Collectors.toSet()); // Collect result into a Set to ensure uniqueness

        // Printing the result
        System.out.println("Common list elements: " + commonElements);
        
        // Output for the sample input: [banana, grape]
    }
}

48. Find Element Closest to a Given Value from List using Java 8

public class FindClosestValue {
    public static void main(String[] args) {
        // Sample list of numbers
        List<Integer> numbers = Arrays.asList(10, 22, 35, 41);
        int targetValue = 30;

        // Using Stream API to find the closest element
        int closestValue = numbers.stream()
                .min((n1, n2) -> Integer.compare(
                        Math.abs(n1 - targetValue), // Distance of n1 from target
                        Math.abs(n2 - targetValue)  // Distance of n2 from target
                ))
                .orElse(0); // Default value if the list is empty

        // Printing the result
        System.out.println("Closest value to " + targetValue + ": " + closestValue);
        
        // Output for [10, 22, 35, 41] and target 30: 35
    }
}


49. Find First Longest Word in A Sentence using the Java 8 Stream


public class FindFirstLongestWord {
    public static void main(String[] args) {
        String sentence = "my name is saurabh kumar and i work at capgemini as a java developer";

        // Approach 1: Using Arrays.stream and a custom comparator logic
        String longestWord1 = Arrays.stream(sentence.split(" "))
                .max((w1, w2) -> Integer.compare(w1.length(), w2.length()))
                .orElse("");

        // Approach 2: Using Comparator.comparingInt (more concise)
        String longestWord2 = Arrays.stream(sentence.split(" "))
                .max(Comparator.comparingInt(String::length))
                .orElse("");

        System.out.println("Longest Word: " + longestWord2);
        
        // Output for the sample sentence: capgemini
    }
}

50. Count Vowels in a List of Strings using Java 8 Streams API

public class CountVowels {
    public static void main(String[] args) {
        // Sample list of strings
        List<String> words = Arrays.asList("apple", "banana", "grape", "orange");

        // Reference string containing all vowels (case-insensitive)
        String vowels = "AEIOUaeiou";

        // Using Stream API to count total vowels
        long count = words.stream()
                .flatMapToInt(String::chars) // Convert each string to an IntStream of characters
                .filter(c -> vowels.indexOf(c) != -1) // Keep only characters found in the vowels string
                .count(); // Count the occurrences

        // Output the result
        System.out.println("Total Vowels: " + count);
        
        // Output for ["apple", "banana", "grape", "orange"]: 10
    }
}

51.  Find the Shortest String in a List using Java 8 Stream API


public class FindShortestString {
    public static void main(String[] args) {
        // Sample list of strings
        List<String> words = Arrays.asList("apple", "banana", "kiwi", "orange", "grape");

        // Using Stream API to find the shortest string
        Optional<String> shortestString = words.stream()
                .min((s1, s2) -> Integer.compare(s1.length(), s2.length()));

        // Display the result if present
        shortestString.ifPresent(word -> 
            System.out.println("Shortest string in list: " + word)
        );
        
        // Output for ["apple", "banana", "kiwi", "orange", "grape"]: kiwi
    }
}

52. Find First Repeated Element in a List using Java 8 Stream API

public class FindFirstRepeated {
    public static void main(String[] args) {
        // Sample input list with duplicates
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 4, 2, 5, 3, 6);

        // A Set to store unique elements as we process the stream
        Set<Integer> seen = new HashSet<>();

        // Logic to find the first repeated element
        int firstRepeated = numbers.stream()
                .filter(n -> !seen.add(n)) // If add(n) returns false, the number is already in the set
                .findFirst()                // Get the very first one that triggers the filter
                .orElse(-1);               // Default value if no repeats are found

        // Result Output
        System.out.println("First repeated element: " + firstRepeated);
        
        // Output for [1, 2, 3, 4, 5, 4, 2, 5, 3, 6]: 4
    }
}

53. Sort Strings by Their Last Character using Java 8 Streams API

public class SortByLastChar {
    public static void main(String[] args) {
        // Sample list of strings
        List<String> words = Arrays.asList("apple", "banana", "grape", "orange", "kiwi");

        // Using Stream API to sort by the last character
        List<String> sortedWords = words.stream()
                .sorted(Comparator.comparingInt(s -> s.charAt(s.length() - 1)))
                .collect(Collectors.toList());

        // Printing the result
        System.out.println("Sorted by last character: " + sortedWords);
        
        // Output: [banana, apple, grape, orange, kiwi]
        // Note: banana ends in 'a' (first). apple, grape, orange end in 'e' (original order maintained).
    }
}


54. Find Difference Between Two Lists using Java 8 Streams API

public class FindListDifference {
    public static void main(String[] args) {
        // Sample input lists
        List<Integer> list1 = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> list2 = Arrays.asList(3, 4, 5, 6, 7);

        // Finding the difference (elements in list1 but not in list2)
        List<Integer> difference = list1.stream()
                .filter(n -> !list2.contains(n)) // Keep if NOT in list2
                .collect(Collectors.toList());

        // Result output
        System.out.println("Difference value: " + difference);
        
        // Output for [1, 2, 3, 4, 5] and [3, 4, 5, 6, 7]: [1, 2]
    }
}


55. Reverse the Characters of Each String in a List using Java 8

public class ReverseCharacters {
    public static void main(String[] args) {
        // Sample input list
        List<String> words = Arrays.asList("apple", "banana", "cherry");

        // Using Stream API to reverse each string
        List<String> reversedWords = words.stream()
                .map(word -> new StringBuilder(word).reverse().toString())
                .collect(Collectors.toList());

        // Printing the result
        System.out.println("Reverse word: " + reversedWords);
        
        // Output for ["apple", "banana", "cherry"]: [elppa, ananab, yrrehc]
    }
}


56. Find All Unique Characters in String using Java 8 Streams API


public class FindUniqueCharacters {
    public static void main(String[] args) {
        String str = "hello world";

        // Using Stream API to find unique characters
        Set<Character> uniqueChars = str.chars() // Returns an IntStream of character codes
                .mapToObj(c -> (char) c)         // Convert int codes back to Character objects
                .filter(c -> c != ' ')           // Optional: Exclude spaces
                .collect(Collectors.toCollection(LinkedHashSet::new)); // Maintain insertion order

        // Printing the result
        System.out.println("Unique characters: " + uniqueChars);
        
        // Output: [h, e, l, o, w, r, d]
    }
}


56. Find Longest Words in a Sentence Using Java 8 Streams API

public class FindLongestWords {
    public static void main(String[] args) {
        String sentence = "my name is saurabh and i work at capgemini as a java developer";

        // Step 1: Find the maximum length in the sentence
        int maxLength = Arrays.stream(sentence.split(" "))
                .mapToInt(String::length)
                .max()
                .orElse(0);

        // Step 2: Collect all words that have this maximum length
        List<String> longestWords = Arrays.stream(sentence.split(" "))
                .filter(word -> word.length() == maxLength)
                .collect(Collectors.toList());

        // Printing the result
        System.out.println("Longest word(s): " + longestWords);
        
        // Output for the sample sentence: [capgemini, developer]
    }
}


57. Find Longest Palindrome in a List using Java 8 Streams API

public class LongestPalindrome {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("madam", "hello", "civic", "noon", "level", "racecar", "cap");

        // Step 1: Filter the list to find all palindromes
        List<String> palindromes = words.stream()
                .filter(word -> word.equalsIgnoreCase(new StringBuilder(word).reverse().toString()))
                .collect(Collectors.toList());

        if (palindromes.isEmpty()) {
            System.out.println("No palindrome found");
        } else {
            // Step 2: Find the maximum length among the found palindromes
            int maxLength = palindromes.stream()
                    .mapToInt(String::length)
                    .max()
                    .orElse(0);

            // Step 3: Collect all palindromes that match the maximum length
            List<String> longestPalindromes = palindromes.stream()
                    .filter(p -> p.length() == maxLength)
                    .collect(Collectors.toList());

            System.out.println("Longest palindrome: " + longestPalindromes);
        }
        
        // Output for the sample list: [racecar]
    }
}


58. Calculate Factorials of a List of Numbers using Java 8 Stream

public class CalculateFactorial {
    public static void main(String[] args) {
        // Sample input list
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        // Using Stream API to map each number to its factorial
        List<Integer> factorials = numbers.stream()
                .map(CalculateFactorial::factorial) // Method reference to the recursive method
                .collect(Collectors.toList());

        // Printing the result
        System.out.println("Factorials: " + factorials);
        
        // Output: [1, 2, 6, 24, 120, 720]
    }

    // Recursive method to calculate factorial of a number
    private static int factorial(int n) {
        return (n == 0) ? 1 : n * factorial(n - 1);
    }
}

59. Find the Average Length of Strings in List in Java 8 Streams

public class FindAverageLength {
    public static void main(String[] args) {
        // Sample input list
        List<String> words = Arrays.asList("apple", "banana", "kiwi");

        // Using Stream API to find the average string length
        double averageLength = words.stream()
                .mapToInt(String::length) // Convert words to their lengths (IntStream)
                .average()                // Calculate the average
                .orElse(0.0);             // Default to 0.0 if the list is empty

        // Printing the result
        System.out.println("Average string length: " + averageLength);
        
        // Output for ["apple", "banana", "kiwi"]: 5.0
        // apple (5) + banana (6) + kiwi (4) = 15. Total words = 3. 15 / 3 = 5.0
    }
}

60. Find the Most Frequent Element in List using Java 8

public class MostFrequentElement {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 2, 1, 3);

        // Validation for empty list
        if (numbers.isEmpty()) {
            System.out.println("The list is empty; no frequent element to find.");
            return;
        }

        // Step 1: Create a frequency map {element -> count}
        Map<Integer, Long> frequencyMap = numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));

        // Step 2: Find the maximum frequency value
        long maxFrequency = frequencyMap.values().stream()
                .max(Long::compare)
                .orElse(0L);

        // Step 3: Collect all elements that have the maximum frequency
        List<Integer> mostFrequent = frequencyMap.entrySet().stream()
                .filter(entry -> entry.getValue() == maxFrequency)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());

        System.out.println("Most frequent element(s): " + mostFrequent);
        
        // Output for [1, 2, 3, 2, 1, 3]: [1, 2, 3] (since all appear twice)
    }
}

61. Count the Number of Digits in a String in Java 8 Streams API

public class CountStringDigits {
    public static void main(String[] args) {
        String str = "hello 123";

        // Using Stream API to count digits
        long digitCount = str.chars()            // Returns an IntStream of character codes
                .filter(Character::isDigit)      // Filters for characters that are digits
                .count();                        // Returns the total count

        // Printing the result
        System.out.println("Digit count: " + digitCount);
        
        // Output for "hello 123": 3
    }
}

62.Create a Map from Two Lists using Java 8 Stream API

public class CreateMapFromTwoLists {
    public static void main(String[] args) {
        // List 1: Keys
        List<String> keys = Arrays.asList("a", "b", "c");
        
        // List 2: Values
        List<Integer> values = Arrays.asList(1, 2, 3);

        // Creating a map using Stream API
        Map<String, Integer> map = keys.stream()
                .collect(Collectors.toMap(
                        key -> key,                                // Key mapper
                        key -> values.get(keys.indexOf(key))        // Value mapper using index
                ));

        // Printing the result
        System.out.println("Created map: " + map);
        
        // Output: {a=1, b=2, c=3}
    }
}

63. Group strings by their length using the Java 8 Streams API


public class GroupByLength {
    public static void main(String[] args) {
        // Sample input list
        List<String> words = Arrays.asList("apple", "bat", "cat", "banana", "crab");

        // Using Stream API to group strings by length
        Map<Integer, List<String>> groupedByLength = words.stream()
                .collect(Collectors.groupingBy(String::length)); // Grouping by string length

        // Printing the result using forEach
        groupedByLength.forEach((length, group) -> {
            System.out.println(length + ": " + group);
        });

        /*
        Expected Output:
        3: [bat, cat]
        5: [apple, crab]
        6: [banana]
        */
    }
}

64. Find Numbers Starting with 1 in Java 8 Stream API


public class NumbersStartingWithOne {
    public static void main(String[] args) {
        // Sample input list
        List<Integer> numbers = Arrays.asList(10, 15, 8, 49, 25, 98, 32);

        // Using Stream API to find numbers starting with '1'
        numbers.stream()
                .map(s -> s + "")             // Convert each integer to a String
                .filter(s -> s.startsWith("1")) // Filter strings that start with "1"
                .forEach(System.out::println);  // Print each matching result

        // Output for the sample list:
        // 10
        // 15
    }
}

65. Sum and Sort Transactions by Date in Java 8 Streams API

import java.util.*;
import java.util.stream.Collectors;

public class TransactionByDate {
    public static void main(String[] args) {
        // List of transactions (Date, Amount)
        List<TransactionRecord> transactions = Arrays.asList(
            new TransactionRecord("2024-12-23", 100),
            new TransactionRecord("2024-12-24", 200),
            new TransactionRecord("2024-12-25", 300),
            new TransactionRecord("2024-12-24", 400),
            new TransactionRecord("2024-12-25", 500)
        );

        // Step 1: Group by date and sum the amounts
        Map<String, Integer> sumByDate = transactions.stream()
                .collect(Collectors.groupingBy(
                        TransactionRecord::getDate,
                        Collectors.summingInt(TransactionRecord::getAmount)
                ));

        // Step 2: Sort the results by date and print
        System.out.println("Date\t\tAmount");
        sumByDate.entrySet().stream()
                .sorted(Map.Entry.comparingByKey())
                .forEach(entry -> System.out.println(entry.getKey() + "\t" + entry.getValue()));
    }
}

// Custom class for transaction records
class TransactionRecord {
    private String date;
    private int amount;

    public TransactionRecord(String date, int amount) {
        this.date = date;
        this.amount = amount;
    }

    public String getDate() { return date; }
    public int getAmount() { return amount; }
}

66. Find Employees by Department using the Java 8 Streams API


public class FindEmployeeByDepartment {
    public static void main(String[] args) {
        // Step 1: Initialize a list of employees
        List<Employee> employeeList = Arrays.asList(
            new Employee("Saurabh", "IT"),
            new Employee("Shubham", "HR"),
            new Employee("Sony", "IT"),
            new Employee("Rahul", "HR")
        );

        // Step 2: Use Stream API to filter by department (e.g., "IT")
        List<Employee> itEmployees = employeeList.stream()
                .filter(e -> "IT".equals(e.getDepartment())) // Filter by department name
                .collect(Collectors.toList());               // Collect results into a list

        // Step 3: Print the results
        itEmployees.forEach(System.out::println);
        
        /* Output for "IT":
        Employee{name='Saurabh', department='IT'}
        Employee{name='Sony', department='IT'}
        */
    }
}

// Custom Employee class
class Employee {
    private String name;
    private String department;

    public Employee(String name, String department) {
        this.name = name;
        this.department = department;
    }

    public String getDepartment() { return department; }

    @Override
    public String toString() {
        return "Employee{name='" + name + "', department='" + department + "'}";
    }
}
