# Exam Scheduler Program

## Overview

This Java program provides a solution for scheduling exams by assigning courses to available rooms based on capacity constraints. The system includes classes to represent courses, rooms, schedules, and an exam scheduler that uses recursive backtracking to find valid schedules.

## Classes

### 1. Course
Represents a course that needs an exam room.

**Key Features:**
- Stores course name and number of students
- Validates that number of students is non-negative
- Provides getter methods for course information

### 2. Room
Represents an available exam room.

**Key Features:**
- Stores room location and capacity
- Validates that capacity is non-negative
- Provides method to reduce capacity (returns new Room object)
- Provides getter methods for room information

### 3. Schedule
Manages the assignment of courses to rooms.

**Key Features:**
- Tracks which courses are assigned to which rooms
- Ensures room capacities are not exceeded
- Provides methods to:
  - Check assignment status
  - Get room/course information
  - Assign courses to rooms (returns new Schedule object)
  - Check if schedule is complete
- Includes toString() for human-readable schedule representation

### 4. ExamScheduler
Core scheduling logic using recursive backtracking.

**Key Methods:**
- `findSchedule()`: Finds one valid schedule (throws exception if none exists)
- `findAllSchedules()`: Finds all possible valid schedules
- Uses helper methods with recursive backtracking to explore possibilities

### 5. ExamSchedulerTester
Comprehensive test suite for all functionality.

**Test Coverage:**
- Course class validation
- Room class validation
- Schedule accessors and assignment
- ExamScheduler functionality (single and all schedules)

## How It Works

1. **Input**: Provide arrays of Room and Course objects
2. **Scheduling**:
   - ExamScheduler tries to assign each course to a suitable room
   - Uses recursive backtracking to explore possibilities
   - Backtracks when constraints are violated
3. **Output**:
   - `findSchedule()`: Returns one valid schedule or throws exception
   - `findAllSchedules()`: Returns list of all valid schedules

## Usage Example

```java
// Create rooms and courses
Room[] rooms = {
    new Room("AG 125", 200),
    new Room("HUM 3650", 180),
    new Room("CS 1240", 100)
};

Course[] courses = {
    new Course("CS200", 160),
    new Course("CS300", 80),
    new Course("CS400", 120)
};

// Find a schedule
try {
    Schedule schedule = ExamScheduler.findSchedule(rooms, courses);
    System.out.println(schedule.toString());
} catch (IllegalStateException e) {
    System.out.println("No valid schedule found: " + e.getMessage());
}

// Find all possible schedules
ArrayList<Schedule> allSchedules = ExamScheduler.findAllSchedules(rooms, courses);
for (Schedule s : allSchedules) {
    System.out.println(s.toString());
}
```

## Testing

The included `ExamSchedulerTester` class provides comprehensive test coverage:
- Run `testAll()` to execute all tests
- Individual test methods available for specific components

## Design Patterns

- **Immutable Objects**: Course and Room are immutable (methods return new objects rather than modifying state)
- **Recursive Backtracking**: Used to explore all possible valid schedules
- **Defensive Programming**: Extensive input validation and exception handling

## Limitations

- Performance may degrade with large numbers of courses/rooms due to recursive nature
- Currently only considers room capacity as a constraint
- Basic scheduling - doesn't consider time slots or other real-world constraints

## Future Enhancements

- Add time slot considerations
- Include additional constraints (room features, accessibility, etc.)
- Optimize performance for larger datasets
- Add GUI for visualization
