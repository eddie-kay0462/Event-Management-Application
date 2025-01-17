### README Documentation

# 1. Event Class

## Overview

The `Event` class is used to manage events with details like title, date, time, location, and description. It automatically assigns a unique ID to each event and supports different date formats.

## Features

- **Unique ID:** Each event gets a unique ID for easy identification.
- **Flexible Date Parsing:** Can handle various date formats, including:
  - `yyyy-MM-dd` (ISO format)
  - `yyyy/MM/dd` (Slash separator)
  - `MM/dd/yyyy` (US format)
  - `dd-MM-yyyy` (Day-Month-Year format)
  - `dd/MM/yyyy` (Alternative Day-Month-Year format)
- **Constructors:**
  - **Primary Constructor:** Accepts `priority`, `title`, `dateString`, `time`, `location`, and `description`. It parses the date string and handles errors for invalid formats.
  - **Secondary Constructor:** Accepts `priority`, `title`, `date` (as `LocalDate`), `time`, `location`, and `description`, making it easy to use a `LocalDate` directly.

## Usage

Create an event by using one of the constructors with the required details. The class will handle the unique ID assignment and date parsing for you.

### Example

```java
Event event1 = new Event(1, "Meeting", "2024-08-03", "10:00 AM", "Conference Room", "Monthly team meeting.");
Event event2 = new Event(2, "Workshop", LocalDate.of(2024, 8, 5), "2:00 PM", "Main Hall", "Workshop on new software.");
```

## Error Handling

If you provide an invalid date format, an `IllegalArgumentException` will be thrown. Make sure your date string matches one of the supported formats.

For more information or help, check the class documentation or contact support.


# 2. SortingCalendar Class

## Overview

The `SortingCalendar` class provides a command-line interface for managing events using a linked list. It supports creating, modifying, deleting, viewing, searching, sorting, and summarizing events. Each event is uniquely identified by an ID, and the class allows for flexible manipulation and management of these events.

## Features

- **Create Event:** Add a new event to the linked list with details such as title, date, time, location, and description.
- **Modify Event:** Update existing events based on their ID. You can change attributes like title, date, time, location, and description.
- **Delete Event:** Remove an event from the list by its ID.
- **View Events:** Display all events currently in the list. Filtering options can be implemented to view events based on specific criteria.
- **Search Event:** Find events based on attributes like title, date, or location.
- **Sort Events:** Organize events based on a specified attribute in either ascending or descending order.
- **Generate Summary:** Create a summary of events within a specified date range. (Summary generation logic needs to be implemented.)

## Usage

Run the `SortingCalendar` class and use the following commands to interact with the event list:

- **create_event** `title date time location description`  
  Example: `create_event Meeting 2024-08-03 10:00 AM Conference Room Monthly team meeting.`
  
- **modify_event** `id attribute newValue`  
  Example: `modify_event 1 title New Meeting Title`
  
- **delete_event** `id`  
  Example: `delete_event 1`
  
- **view_events** `filter`  
  Example: `view_events`

- **search_event** `attribute value`  
  Example: `search_event title Meeting`

- **sort_events** `attribute` or `-attribute`  
  Example: `sort_events date` for ascending order, `sort_events -date` for descending order

- **generate_summary** `dateRange`  
  Example: `generate_summary 2024-08-01 to 2024-08-31`

## Error Handling

- For invalid commands or malformed input, appropriate error messages will be displayed.
- If an attempt is made to modify or delete an event that does not exist, a message indicating the event was not found will be shown.

## Example

```java
Event event1 = new Event(1, "Meeting", LocalDate.of(2024, 8, 3), "10:00 AM", "Conference Room", "Monthly team meeting.");
Event event2 = new Event(2, "Workshop", LocalDate.of(2024, 8, 5), "2:00 PM", "Main Hall", "Workshop on new software.");
```

## Requirements

- Java Development Kit (JDK) 8 or higher
- LinkedList class implementation (should be included in your project)

For more details, refer to the class documentation or contact support.

# 3. Calendar Class

## Overview

The `Calendar` class provides tools for creating and managing a calendar structure for a specified year. It supports the creation of a calendar with months and days, handling leap years, and sorting events by various attributes. The calendar is implemented using nested `HashMap` structures to map months and days to lists of events.

## Features

- **Leap Year Calculation:** Determines if a given year is a leap year, adjusting the number of days in February accordingly.
- **Create Calendar:** Constructs a calendar for a specified year with months and days. Each day has an associated list to store `Event` objects.
- **Sort Events:** Allows sorting of events within the calendar by attributes such as title, date, or priority. Sorting is performed using the `EventSorter` class and supports both ascending and descending order.
- **Print Calendar Structure:** Provides a way to print the structure of the calendar, displaying months and their days.

## Methods

- **`isLeapYear(int year)`**  
  Checks if the given year is a leap year. Returns `true` if it is, otherwise `false`.

- **`createCalendar(int year)`**  
  Creates a `HashMap` representing the calendar for the specified year. Each month maps to another `HashMap` of days, with each day initially holding an empty list of `Event` objects.

- **`sortEvents(HashMap<String, HashMap<Integer, ArrayList<Event>>> calendar, String attribute, boolean reverse)`**  
  Sorts events in the calendar based on the specified attribute (title, date, or priority) and order (ascending or descending). Uses the `EventSorter` class for sorting.

- **`main(String[] args)`**  
  Demonstrates the creation of a calendar for the year 2024 and prints the calendar structure, showing months and their respective days.

## Usage

1. **Creating a Calendar:**
   ```java
   int year = 2024;
   HashMap<String, HashMap<Integer, ArrayList<Event>>> calendar = Calendar.createCalendar(year);
   ```

2. **Sorting Events:**
   ```java
   Calendar.sortEvents(calendar, "title", false); // Sort events by title in ascending order
   ```

3. **Printing Calendar Structure:**
   ```java
   for (String month : calendar.keySet()) {
       System.out.println(month + ": " + calendar.get(month).keySet());
   }
   ```

## Requirements

- Java Development Kit (JDK) 8 or higher
- `Event` class and `EventSorter` class implementations

For more information, consult the class documentation or reach out for support.

# 4. EventSorter Class

## Overview

The `EventSorter` class provides functionality to sort a list of `Event` objects using the merge sort algorithm. This class is designed to handle sorting by different attributes of the events, such as date, title, and priority. It supports both ascending and descending order sorting.

## Features

- **Merge Sort Implementation:** The class uses the merge sort algorithm, which is stable and efficient with a time complexity of O(n log n).
- **Flexible Attribute Sorting:** Allows sorting by different attributes: date, title, or priority.
- **Order Specification:** Supports sorting in both ascending and descending order.

## Methods

### `mergeSort`

```java
public static void mergeSort(ArrayList<Event> events, String attribute, boolean reverse)
```

- **Description:** Recursively splits the list of events into smaller sublists, sorts each sublist, and merges them back together in sorted order.
- **Parameters:**
  - `events`: The list of `Event` objects to be sorted.
  - `attribute`: The attribute by which to sort the events (`date`, `title`, or `priority`).
  - `reverse`: A boolean indicating whether to sort in descending order.

### `merge`

```java
private static void merge(ArrayList<Event> events, ArrayList<Event> left, ArrayList<Event> right, String attribute, boolean reverse)
```

- **Description:** Merges two sorted sublists into a single sorted list.
- **Parameters:**
  - `events`: The original list to store the merged result.
  - `left`: The left sublist.
  - `right`: The right sublist.
  - `attribute`: The attribute by which to sort the events.
  - `reverse`: A boolean indicating whether to sort in descending order.

### `compareByAttribute`

```java
private static int compareByAttribute(Event a, Event b, String attribute)
```

- **Description:** Compares two `Event` objects based on the specified attribute.
- **Parameters:**
  - `a`: The first `Event` object.
  - `b`: The second `Event` object.
  - `attribute`: The attribute by which to compare the events.
- **Returns:** An integer indicating the comparison result.

## Usage

### Example

```java
import java.util.ArrayList;

public class EventSorterExample {
    public static void main(String[] args) {
        ArrayList<Event> events = new ArrayList<>();
        // Add events to the list

        EventSorter.mergeSort(events, "date", false);
        for (Event event : events) {
            System.out.println(event.title + " " + event.date + " " + event.priority);
        }
    }
}
```

In this example, the `EventSorter` class is used to sort a list of `Event` objects by their date attribute in ascending order. The sorted list is then printed out.

## License

This project is licensed under the MIT License. See the LICENSE file for details.


# 5. HashMap Class

## Overview

The `java.util.HashMap` class provides the implementation of the Map interface, offering efficient key-value pair storage and retrieval. It uses a hash table for storing entries, which allows for quick access to elements based on their keys. The class permits null values and a null key but does not guarantee any specific order of entries.

## Features

- **Efficient Storage:** Uses a hash table to store key-value pairs, providing average O(1) time complexity for basic operations like adding, removing, and retrieving entries.
- **Flexible Key and Value Types:** Supports null values and a null key.
- **Standard and Advanced Operations:** Includes methods for basic operations (`put()`, `get()`, `remove()`, `containsKey()`) and advanced operations (`putIfAbsent()`, `computeIfAbsent()`, `merge()`).

## Usage

### Example

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();

        // Adding entries to the map
        map.put("one", 1);
        map.put("two", 2);
        map.put("three", 3);

        // Retrieving and printing an entry
        int value = map.get("two");
        System.out.println("Value for key 'two': " + value);

        // Checking for the presence of a key
        boolean containsKey = map.containsKey("three");
        System.out.println("Map contains key 'three': " + containsKey);

        // Removing an entry
        map.remove("one");

        // Iterating over the map entries
        for (String key : map.keySet()) {
            System.out.println("Key: " + key + ", Value: " + map.get(key));
        }
    }
}
```

In this example, the `HashMap` class is used to store, retrieve, and manage key-value pairs. The example demonstrates adding entries, retrieving values, checking for key presence, removing entries, and iterating over the map.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

The `SearchingEvent` class provides functionality to manage and search for events based on various attributes such as title, date, and location. The class leverages binary search algorithms to efficiently find events within a sorted list. This ensures quick and accurate retrieval of events, making it ideal for applications that require frequent searching of large event datasets. The methods in the class are designed to target specific attributes, allowing for precise querying.

The methods in the class definition are as follows:

- **`searchEventsByMeeting(String title)`:** This method searches for an event by its title.
  - **Parameters:** `title` - The title of the event to search for.
  - **Returns:** `Event` - The event with the specified title.

- **`searchEventByDate(LocalDate date)`:** This method searches for an event by its date.
  - **Parameters:** `date` - The date of the event to search for.
  - **Returns:** `Event` - The event with the specified date.

- **`searchEventByLocation(String location)`:** This method searches for an event by its location.
  - **Parameters:** `location` - The location of the event to search for.
  - **Returns:** `Event` - The event with the specified location.

---


# 6. SearchingEvent Class

## Overview

The `SearchingEvent` class provides tools to manage and search for events based on attributes like title, date, and location. It uses binary search algorithms for efficient and quick retrieval of events from a sorted list.

## Methods

### `searchEventsByMeeting(String title)`

- **Description:** Searches for an event by its title.
- **Parameters:** `title` - The title of the event to search for.
- **Returns:** `Event` - The event with the specified title.

### `searchEventByDate(LocalDate date)`

- **Description:** Searches for an event by its date.
- **Parameters:** `date` - The date of the event to search for.
- **Returns:** `Event` - The event with the specified date.

### `searchEventByLocation(String location)`

- **Description:** Searches for an event by its location.
- **Parameters:** `location` - The location of the event to search for.
- **Returns:** `Event` - The event with the specified location.

## Usage

### Example

```java
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.Collections;

public class SearchingEvent {
    private ArrayList<Event> events;

    public SearchingEvent() {
        events = new ArrayList<>();
    }

    public void addEvent(Event event) {
        events.add(event);
        Collections.sort(events, Comparator.comparing(Event::getDate)); // Assuming Event has a getDate method
    }

    public Event searchEventsByMeeting(String title) {
        for (Event event : events) {
            if (event.getTitle().equalsIgnoreCase(title)) {
                return event;
            }
        }
        return null;
    }

    public Event searchEventByDate(LocalDate date) {
        int index = Collections.binarySearch(events, new Event(date), Comparator.comparing(Event::getDate)); // Assuming Event has a constructor that takes LocalDate
        if (index >= 0) {
            return events.get(index);
        }
        return null;
    }

    public Event searchEventByLocation(String location) {
        for (Event event : events) {
            if (event.getLocation().equalsIgnoreCase(location)) {
                return event;
            }
        }
        return null;
    }
}
```

In this example, the `SearchingEvent` class is used to add events, and search for events by title, date, and location. The events are stored in a sorted list to facilitate efficient searching.

## License

This project is licensed under the MIT License. See the LICENSE file for details.


# 7. AutomateMain Class

## Overview

The `AutomateMain` class is a comprehensive Java program designed to manage and search for events based on various attributes such as title, date, and location. It reads event data from an input file, organizes it into a structured calendar, and provides an interactive menu for users to search and sort events efficiently.

## Features

- **Loading Events from File:** Reads events from a specified file and stores them in a nested `HashMap` structure.
- **Interactive Menu:** Provides options to search for events by title, date, or location, and to sort events by date, title, or priority.
- **Efficient Searching and Sorting:** Utilizes binary search algorithms and sorting mechanisms to manage events efficiently.
- **User Feedback:** Displays time taken for search and sort operations and provides clear feedback for invalid inputs.

## Usage

1. **Run the Program:**
   - Execute the `main` method of the `AutomateMain` class.
   - Enter the input file name when prompted (e.g., `events.txt`).

2. **Interactive Menu:**
   - The program will display a menu with options to search for events, sort events, or exit.
   - Choose an option by entering the corresponding number.

3. **Search for Events:**
   - Choose to search by title, date, or location.
   - Enter the search term when prompted.
   - The program will display the event details if found.

4. **Sort Events:**
   - Enter the attribute to sort by (date, title, or priority).
   - Specify whether to sort in reverse order (true/false).
   - The program will sort the events and display the time taken for the operation.

## Example

```java
// Sample code to run the AutomateMain class
public class Main {
    public static void main(String[] args) {
        AutomateMain.main(args);
    }
}
```

## Methods

### `main(String[] args)`

The entry point of the program. Initializes the interactive menu and handles user input for searching and sorting events.

### `loadEventsFromFile(String fileName)`

Reads event data from the specified file and organizes it into a nested `HashMap` structure.

#### Parameters:
- `fileName`: The name of the input file containing event details.

#### Returns:
- A `HashMap` representing the calendar with events organized by month and day.

## Additional Notes

- Ensure the input file is in the correct format, with event attributes separated by commas.
- The program handles invalid inputs and provides appropriate feedback to the user.

Certainly! Here’s the README documentation for the `Year_Calendar` class:

---

# 8. Year_Calendar Class

## Overview

The `Year_Calendar` class is designed to manage and print calendar data for multiple years. It utilizes a nested `HashMap` structure to organize and store calendar information by year, month, and day. This class provides methods to add years, retrieve calendar data for specific years, and print the calendar structure in a readable format.

## Features

- **Add Year:** Initializes and adds a new year to the calendar if it does not already exist. Uses the `Calendar.createCalendar(year)` method to generate the calendar structure for the specified year.
- **Get Calendar:** Retrieves the calendar for a specified year. If the year is not present, it automatically adds it.
- **Print Calendar:** Prints the calendar structure for a specified year, displaying the months and days.

## Usage

To use the `Year_Calendar` class, follow these steps:

1. **Initialize:** Create an instance of `Year_Calendar`.
2. **Add and Print:** Add multiple years to the calendar and print the calendar structure.

### Example

```java
public class Main {
    public static void main(String[] args) {
        Year_Calendar yearCalendar = new Year_Calendar();

        // Add and print calendars for multiple years
        int[] years = {2024, 2025, 2026, 2027, 2028};
        for (int year : years) {
            yearCalendar.addYear(year);
            yearCalendar.printCalendar(year);
        }
    }
}
```

## Methods

- **`addYear(int year)`**: Adds the specified year to the calendar. Initializes the calendar if it is not already present.
- **`getCalendar(int year)`**: Retrieves the calendar for the specified year. Adds the year if it is not present.
- **`printCalendar(int year)`**: Prints the calendar structure for the specified year, including months and days.

## Requirements

- Ensure that the `Calendar` class is available and properly implemented with the `createCalendar` method to generate calendar data.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
