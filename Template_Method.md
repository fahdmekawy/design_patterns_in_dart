### **What is a Template Method Design Pattern?**


The **Template Method Design Pattern** is a behavioral design pattern that defines the skeleton of an algorithm in a method, deferring some steps to subclasses. This pattern allows subclasses to redefine certain steps of an algorithm without changing its overall structure.

The key idea is to create an abstract class that contains a method with a fixed sequence of steps, but some of those steps are implemented in the subclasses. The template method ensures the sequence remains the same while allowing flexibility in the details.

### Key Concepts
1. **Template Method:** A method in an abstract class that defines the sequence of steps in the algorithm.
2. **Concrete Methods:** Steps of the algorithm that are implemented in the abstract class and are common to all subclasses.
3. **Abstract Methods:** Steps of the algorithm that are left to be implemented by subclasses.

### Example Scenario: Preparing a Beverage

Let's consider a scenario where you want to prepare different types of beverages (Tea and Coffee). The steps to prepare a beverage are generally the same: boil water, brew or steep the beverage, pour it into a cup, and add condiments. However, the brewing and condiments differ between Tea and Coffee. This is a perfect use case for the Template Method pattern.

### Step 1: Define the Abstract Class with the Template Method

```dart
abstract class Beverage {
  // Template method defining the steps
  void prepareRecipe() {
    boilWater();
    brew();
    pourInCup();
    addCondiments();
  }

  // Concrete method common to all beverages
  void boilWater() {
    print("Boiling water");
  }

  // Concrete method common to all beverages
  void pourInCup() {
    print("Pouring into cup");
  }

  // Abstract methods that subclasses need to implement
  void brew();
  void addCondiments();
}
```

### Step 2: Create Concrete Classes (Tea and Coffee)

```dart
class Tea extends Beverage {
  @override
  void brew() {
    print("Steeping the tea");
  }

  @override
  void addCondiments() {
    print("Adding lemon");
  }
}

class Coffee extends Beverage {
  @override
  void brew() {
    print("Dripping coffee through filter");
  }

  @override
  void addCondiments() {
    print("Adding sugar and milk");
  }
}
```

### Step 3: Use the Template Method in Client Code

```dart
void main() {
  Beverage tea = Tea();
  tea.prepareRecipe();
  // Output:
  // Boiling water
  // Steeping the tea
  // Pouring into cup
  // Adding lemon

  Beverage coffee = Coffee();
  coffee.prepareRecipe();
  // Output:
  // Boiling water
  // Dripping coffee through filter
  // Pouring into cup
  // Adding sugar and milk
}
```

### Explanation:

- **Template Method (`prepareRecipe`)**: This method defines the skeleton of the algorithm for preparing a beverage. It calls the steps in a specific order.
- **Concrete Methods (`boilWater`, `pourInCup`)**: These methods are implemented in the abstract class and are common to all beverages.
- **Abstract Methods (`brew`, `addCondiments`)**: These methods are left to be implemented by the subclasses, allowing customization for different types of beverages (Tea and Coffee).

### Advantages:
1. **Code Reuse:** The common steps of the algorithm are implemented once in the abstract class, and the subclasses only need to implement the specific steps.
2. **Consistency:** The algorithm’s structure is preserved across all subclasses, ensuring that the overall sequence of operations is consistent.
3. **Flexibility:** Subclasses can customize specific steps of the algorithm without altering the algorithm’s structure.

### Disadvantages:
1. **Inheritance Complexity:** Since the pattern relies on inheritance, it can become complex if the hierarchy grows too deep.
2. **Less Flexibility for Subclasses:** The structure of the algorithm is fixed, so subclasses can only modify specific steps, not the overall process.

### Another Example: Data Processing

Consider a scenario where you need to process data from different sources (e.g., reading from a file, database, or API). The overall process involves opening the connection, reading the data, processing the data, and closing the connection. However, the steps for opening and closing the connection might differ based on the data source.

#### Step 1: Define the Abstract Class with the Template Method

```dart
abstract class DataProcessor {
  // Template method defining the steps
  void processData() {
    openConnection();
    readData();
    processDataLogic();
    closeConnection();
  }

  // Concrete method common to all data sources
  void processDataLogic() {
    print("Processing data...");
  }

  // Abstract methods that subclasses need to implement
  void openConnection();
  void readData();
  void closeConnection();
}
```

#### Step 2: Create Concrete Classes (File, Database)

```dart
class FileDataProcessor extends DataProcessor {
  @override
  void openConnection() {
    print("Opening file...");
  }

  @override
  void readData() {
    print("Reading data from file...");
  }

  @override
  void closeConnection() {
    print("Closing file...");
  }
}

class DatabaseDataProcessor extends DataProcessor {
  @override
  void openConnection() {
    print("Connecting to the database...");
  }

  @override
  void readData() {
    print("Reading data from database...");
  }

  @override
  void closeConnection() {
    print("Disconnecting from the database...");
  }
}
```

#### Step 3: Use the Template Method in Client Code

```dart
void main() {
  DataProcessor fileProcessor = FileDataProcessor();
  fileProcessor.processData();
  // Output:
  // Opening file...
  // Reading data from file...
  // Processing data...
  // Closing file...

  DataProcessor dbProcessor = DatabaseDataProcessor();
  dbProcessor.processData();
  // Output:
  // Connecting to the database...
  // Reading data from database...
  // Processing data...
  // Disconnecting from the database...
}
```

In this example, the `processData` method ensures that the sequence of steps is the same, but the implementation of opening, reading, and closing the connection is specific to the data source.
