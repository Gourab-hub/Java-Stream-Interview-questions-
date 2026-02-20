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
