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
