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
