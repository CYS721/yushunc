# README for Pet Project

---

## 1. Project Overview:

This project is a simple implementation of Cat and Dog objects with basic functionalities such as setting attributes, speaking, and interacting with a fake database. Additionally, there are unit tests to ensure the methods work as expected, including random age initialization, name tracking, and the ability to persist data in a fake database. The project is designed with object-oriented programming principles and follows Python best practices.


## 2. File Structure
```bash
.
├── Cat.py               # Contains the Cat class definition (Part 1).
├── Data.py              # Simulates a database connection and operations (Part 1).
├── main.py              # Initial demonstration of Cat class functionality (Part 1).
├── main_part2.py        # Extended demonstration of Cat and Dog functionalities (Part 2).
├── pet.py               # Contains Pet class, and Cat and Dog subclasses for Part 2.
├── petShop.py           # Functions to save pets and print logs of actions (Part 3).
├── test_pets.py         # Unit tests for Cat, Dog, and database operations.
├── homework.sql         # SQL file to define schema and sample insert statements.
└── README.md            # This documentation.
```

## 3. How to Run the Project:

### a. Prerequisites:
- Python 3.1 or above
- `unittest` library 
- `random` library

### b. Running the main demonstration scripts:
1. To run the initial Cat functionality (Part 1):
   - This demonstrates basic functionality for Cat and Data classes (initialization, name setting, and fake database operations).
   
     
   ```bash
   python main.py
   ```
   Expected Output:

   ```
   Name is currently None
   Name has been changed to Garfield
   Connecting to database
   Inserting Garfield into table Cat
   ```

   
2. To run the extended version demonstrating both Cat and Dog functionalities (Part 2):

   - For the extended functionality that includes new methods like speak, random age initialization, and working with both Cat and Dog classes.
   
     
    ```bash
    python main_part2.py
    ```
   Expected Output:

   ```
    Cat's initial name: cat1
    Cat's initial age: 9
    Cat speaks:
    meow
    Cat speaks custom sound:
    cat_sound1
    Cat's name history: ['cat1', 'cat2']
    Cat's new name: cat2
    meow
    meow
    meow
    meow
    meow
    Cat's age after speaking 5 times: 10
    Average name length: 4.0
    
    Dog's initial name: dog1
    Dog's initial age: 8
    Dog speaks:
    woof
    Dog speaks custom sound:
    dog_sound1
    Dog's new name: ['dog1', 'dog2']
    woof
    woof
    woof
    woof
    woof
    Dog's age after barking 5 times: 9
   ```
    
3. To run the pet shop script which saves multiple pets (Part 3):
   - This script demonstrates saving multiple pets (cats and dogs) into a fake database with atomic transactions. If any operation fails, all pets are rolled back.
   
     
   ```bash
    python petShop.py
   ```
   Expected Output:

   ```
    Running saveTest...
    Connecting to fake_database
    Inserting Garfield into table Cat
    Inserting Snoopy into table Dog
    saveTest complete
    
    Running savePetShop...
    Connecting to fake_database
    Beginning a transaction
    Inserting None into table Cat
    Inserting None into table Cat
    Inserting None into table Cat
    Inserting None into table Dog
    Inserting None into table Dog
    Inserting None into table Dog
    Committing transaction
    All pets saved successfully
    savePetShop complete
    
    ---- Execution Statistics ----
    Total number of cats created: 4
    Total number of dogs created: 4
    Names of the cats created:
      Cat 1: cat1
      Cat 2: None
      Cat 3: None
      Cat 4: None
    Names of the dogs created:
      Dog 1: dog1
      Dog 2: None
      Dog 3: None
      Dog 4: None
    Transaction status: committed
    -------------------------------
   ```

    
### c. Running the Unit Tests
To run all the unit tests, execute the following:
    ```bash
    python -m unittest test_pets.py
    ```

Expected Output:

   ```
    meow
    meow
    meow
    meow
    meow
    Connecting to fake_database
    Connecting to fake_database
    
    
    Ran 8 tests in 0.025s
    
    OK
   ```
    


### d. Running the SQL statements
The `homework.sql` SQL schema is tested in PostgreSQL. As it is generic, the SQL statements can also be tested using other SQL client.

1. Load and execute `homework.sql` in a SQL environment.
2. Review the table creation and insert queries for correctness by quering the created table `animals`.
  ```sql
  SELECT * FROM animals;
  ```

## 4. Detailed File Descriptions

### File: Cat.py (Part 1)

The `Cat` class represents a cat with attributes for `name`, `age`, and `favorite_food`, all initially set to `None`. It includes methods for getting and setting these attributes: 

- **`get_name()`**: Returns the cat's name.
- **`get_age()`**: Returns the cat's age.
- **`get_favorite_food()`**: Returns the cat's favorite food.
- **`set_name(new_name)`**: Updates the cat's name.
- **`set_age(new_age)`**: Updates the cat's age.
- **`set_favorite_food(new_favorite_food)`**: Updates the cat's favorite food.

### File: Data.py (Part 1)
The `Data` class simulates a database connection, allowing operations like transactions and insertions. However, no actual database connection is required, as it's designed for the assignment.

- **`__init__(self, database)`**: Initializes the connection, printing a message.
- **`begin_tran(self)`**: Starts a transaction with a print statement.
- **`commit(self)`**: Commits the current transaction, indicating success.
- **`rollback(self)`**: Rolls back the transaction, indicating an undo.
- **`insert(self, table, obj)`**: Inserts an object into a specified table, printing the object's name.

### File: main.py (Part 1)

The `main.py` file demonstrates the basic functionality of the `Cat` and `Data` classes.

1. **Imports**: 
   - Imports the `Cat` class from `Cat.py` and the `Data` class from `Data.py`.

2. **Main Functionality**:
   - Creates a new `Cat` object and prints its initial name (which is `None`).
   - Sets the name of the cat to "Garfield" and prints the updated name.
   - Creates a `Data` object to simulate a database connection, using "database" as the name.
   - Inserts the `Cat` object into the simulated database, printing an insertion message.

### File: pet.py (Part 2)

The `pet.py` file defines a hierarchy of classes for modeling pets, specifically `Cat` and `Dog`, inheriting from a generic `Pet` class.

#### Class: Pet
- **Attributes**:
  - **`name`**: Optional initial name of the pet.
  - **`age`**: Randomly assigned between 5 and 10 upon initialization.
  - **`favorite_food`**: Initially set to `None`.
  - **`names_history`**: List tracking all names the pet has had.
  - **`speak_count`**: Counter for the number of times the pet has spoken.
  - **`sound`**: The default sound the pet makes (e.g., "meow" for cats, "woof" for dogs).

- **Methods**:
  - **`__init__(self, name=None, sound="")`**: Initializes the pet's attributes.
  - **`get_name()`**: Returns the pet's name.
  - **`get_age()`**: Returns the pet's age.
  - **`get_favorite_food()`**: Returns the favorite food.
  - **`set_name(new_name)`**: Updates the pet's name and records it.
  - **`set_age(new_age)`**: Sets the pet's age.
  - **`set_favorite_food(new_favorite_food)`**: Sets the pet's favorite food.
  - **`speak(sound=None)`**: Prints the sound the pet makes. Increments age every five speaks.
  - **`get_names()`**: Returns the history of names.
  - **`get_average_name_length()`**: Computes the average length of the names in the history.

#### Class: Cat
- Inherits from `Pet`.
- **`__init__(self, name=None)`**: Calls the parent constructor with "meow" as the default sound.

#### Class: Dog
- Inherits from `Pet`.
- **`__init__(self, name=None)`**: Calls the parent constructor with "woof" as the default sound.

### File: main_part2.py (Part 2)

This file serves as an interactive demonstration of the `Cat` and `Dog` classes, showcasing their attributes and methods. It highlights name changes, speaking behavior, and age increments while providing a clear example of how to manage pet objects in a program.

1. **Imports**:
   - Imports `Cat` and `Dog` classes from `pet.py`.

2. **Main Logic**:
   - **Creating a Cat**:
     - Initializes a `Cat` object named "cat1".
     - Prints the cat’s initial name and age.
     - Calls the `speak()` method to demonstrate the default sound ("meow").
     - Calls `speak()` again with a custom sound.

   - **Changing Cat's Name**:
     - Updates the cat’s name to "cat2" and prints the name history.
     - Displays the most recent name in the history.

   - **Age Increment**:
     - Calls `speak()` five times to increment the cat's age.
     - Prints the cat’s age after speaking.

   - **Average Name Length**:
     - Calculates and prints the average length of the cat’s names.

3. **Creating a Dog**:
   - Initializes a `Dog` object named "dog1".
   - Prints the dog’s initial name and age.
   - Calls the `speak()` method to demonstrate the default sound ("woof").
   - Calls `speak()` with a custom sound.

4. **Changing Dog's Name**:
   - Updates the dog’s name to "dog2" and prints the updated name history.

5. **Age Increment for Dog**:
   - Calls `speak()` five times to increment the dog’s age.
   - Prints the dog’s age after barking.


### File: petShop.py (Part 3)

The `petShop.py` file manages the creation and storage of `Cat` and `Dog` objects in a simulated database environment. It includes functions for saving pets and logging execution statistics.


1. **Imports**:
   - Imports `Cat` and `Dog` classes from `pet.py`.
   - Imports the `Data` class from `Data.py`.

2. **Global Variables**:
   - **`saved_cats`**: List to track cats that have been created and saved.
   - **`saved_dogs`**: List to track dogs that have been created and saved.
   - **`transaction_status`**: String to track the status of the database transaction (e.g., "pending", "committed", "rolled back").

3. **Functions**:
   - **`saveTest()`**:
     - Creates one `Cat` and one `Dog`, inserts them into the database, and updates the transaction status to "committed".
     - Prints messages indicating the progress and completion of the test.

   - **`savePetShop()`**:
     - Creates three nameless cats and three nameless dogs, attempting to insert them into the database within a transaction.
     - Commits the transaction if successful or rolls back if an error occurs, ensuring atomicity.
     - Prints messages about the saving process and any errors encountered.

   - **`logStats()`**:
     - Prints statistics about the execution, including the total number of cats and dogs created.
     - Lists the names of the saved cats and dogs.
     - Displays the current transaction status.

4. **Main Execution**:
   - The script runs `saveTest()` to create and save one cat and one dog.
   - Then, it runs `savePetShop()` to save multiple pets.
   - Finally, it calls `logStats()` to display the execution statistics.


### File: test_pets.py

The `test_pets.py` file contains unit tests for the `Cat` and `Dog` classes, as well as for the `Data` class. It uses the `unittest` framework to ensure the correctness of methods and behaviors.

1. **TestCat**:
   - **`test_initial_age`**: Verifies that a new cat's age is a random number between 5 and 10.
   - **`test_speak`**: Tests the `speak()` method for default and custom sounds using mocking to capture printed output.
   - **`test_speak_increments_age`**: Confirms that the cat's age increases by 1 after speaking 5 times.
   - **`test_set_name`**: Checks that the `set_name()` method correctly tracks all previous names.
   - **`test_average_name_length`**: Validates the calculation of the average length of all names assigned to the cat.

2. **TestDog**:
   - **`test_speak`**: Similar to the `Cat` test, this verifies that the `Dog` class's `speak()` method outputs the correct default and custom sounds.

3. **TestDatabaseOperations**:
   - **`setUp`**: Initializes a fake database connection before each test.
   - **`test_insert_cat`**: Tests the insertion of a cat into the database, validating the printed output.
   - **`test_insert_dog`**: Tests the insertion of a dog into the database, checking the printed output as well.


### File: homework.sql

The `homework.sql` file contains table creation statements for storing the animals and sample insert statements to persist animal data. The schema is written and tested in PostgreSQL, but it is generic and can be used in most other SQL environments.

  ```sql
CREATE TABLE animals (
    "id" SERIAL PRIMARY KEY,     -- Unique ID for each animal
    "name" VARCHAR(50),          -- The animal's name (nullable)
    age INT,                     -- The animal's age
    favorite_food VARCHAR(50),   -- The animal's favorite food 
    "type" VARCHAR(10) NOT NULL  -- Type of animal (e.g., Cat, Dog)
);
```

## 5. Design Decisions
- **Inheritance for Pets**: I used inheritance to avoid code duplication. Both Cat and Dog inherit common behaviors from a parent Pet class, ensuring the code follows the DRY (Don't Repeat Yourself) principle.

- **Database Simulation**: Instead of setting up a real database connection, a fake database class (Data.py) is used to simulate the behavior. This allowed us to meet the requirement of not needing a physical database while keeping the structure close to reality.

- **Naming Standard**: The variable, class, and method names were named to meet and align with Python's PEP8 style guide. 

- **Testing**: A variety of unit tests were implemented, including random age assertion, method functionality checks (like `speak()`), and database operations to ensure that every crucial aspect of the code has coverage in the tests.

## 6. Future Improvements
- **Persistence**: A potential future improvement could involve implementing real database connectivity and persisting the pets in a true database environment.

- **Error Handling**: While the current implementation simulates errors using prints, more robust error handling could be added (e.g., raising exceptions).

- **Extending Pet Functionality**: We could further extend Pet to include more types of animals or introduce more behaviors and attributes (e.g., health, energy).

## 7. Reflections on the Assignment
- **Why Inheritance**: Inheritance is used for Dog and Cat because it reduced redundancy and allowed shared functionality. For example, both animals share attributes like name and methods like `speak`, so it was logical to define them once in a parent class.

- **Database Simulation**: The requirement not to use an actual database connection seemed limiting at first, but the fake database simulation allows testing without the complexity of real-world persistence.

- **Suggested Changes**: While the random age generation works, it might be beneficial to make it more configurable. Future improvements could allow setting a custom age range rather than hard-coding 5-10.
