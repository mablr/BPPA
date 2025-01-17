# Best Practices for Programming Assignments

**Duration**: 30 min.  
**Topics**: Code Quality, Readability, Documentation, Structure, Reproducibility, and Testing

## Introduction: Why doing things right?

Establishing and adopting programming best practices is especially useful for:

- Writing clean, maintainable code.
- Ensuring reproducibility and reliability.
- Working effectively with others.

Adopting this rigorous approach to good programming practices will benefit you on all levels, both academically and professionally.

## Best practices

### Code Quality and Readability

- Use **meaningful** names for your variables and functions.
- Follow **consistent** indentation and formatting.

**Before**

```python
def f(n):
 if n <= 1:
    return n
 else:
    return(f(n-1) + f(n-2))
```

**After**

```python
def fibonacci(number):
    if number <= 1:
        return number
    else:
        return fibonacci(number - 1) + fibonacci(number - 2)
```

### Documentation & Comments

- Write concise and relevant comments.
- Use docstrings for functions/classes to describe their purpose, inputs, and outputs.

**Before**

```python
class Dog:
    def __init__(self, name, age):
        # Dog's constructor
        self.name = name
        self.age = age

    def bark(self):
        return "Woof!"

    def dog_years(self):
        # Return dog's age
        return self.age * 7
```

**After**

```python
class Dog:
    """
    A class to represent a dog.

    Attributes:
    name (str): The name of the dog.
    age (int): The age of the dog in human years.

    Methods:
    bark(): Returns the sound the dog makes.
    dog_years(): Calculates the dog's age in dog years.
    """

    def __init__(self, name, age):
        """
        Constructs all the necessary attributes for the dog object.

        Parameters:
        name (str): The name of the dog.
        age (int): The age of the dog in human years.
        """
        self.name = name
        self.age = age

    def bark(self):
        """
        Returns the sound the dog makes.

        Returns:
        str: The sound "Woof!".
        """
        return "Woof!"

    def dog_years(self):
        """
        Calculates the dog's age in dog years.

        Returns:
        int: The age of the dog in dog years.
        """
        return self.age * 7
```

### Code Structure

- Organize code into functions, objects, and modules.
- Avoid duplication (DRY principle: Don’t Repeat Yourself).

**Before**

```python
data = [1, 2, 3, 4, 5]

# Calculate the square of each number
squares = []
for num in data:
    squares.append(num ** 2)

# Calculate the cube of each number
cubes = []
for num in data:
    cubes.append(num ** 3)
```

**After**

```python
class DataProcessor:
    def __init__(self, data):
        self.data = data

    def calculate_squares(self):
        return [num ** 2 for num in self.data]

    def calculate_cubes(self):
        return [num ** 3 for num in self.data]

data = [1, 2, 3, 4, 5]
processor = DataProcessor(data)
squares = processor.calculate_squares()
cubes = processor.calculate_cubes()
```

### Input Validation and Error Handling

- Always validate and sanitize inputs to ensure they are safe and expected.
- Verify input correctness and handle invalid inputs appropriately.
- Implement comprehensive error handling to manage all potential failure cases.

**Before**

```python
def divide(a, b):
    return a / b

a = float(input("Enter the numerator: "))
b = float(input("Enter the denominator: "))

result = divide(a, b)
print(result)
```

**After**

```python
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Error: Division by zero is not allowed."
    except TypeError:
        return "Error: Both inputs must be numbers."

def sanitize_input(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Invalid input. Please enter a valid number.")

a = sanitize_input("Enter the numerator: ")
b = sanitize_input("Enter the denominator: ")

result = divide(a, b)
print(result)
```

*Ensure that error messages do not reveal sensitive information such as system details, session identifiers, or account information.*

### Reproducibility

- Include clear instructions for setting up and running the program.
- Create requirements files for dependencies.

**Setting up a Python Virtual Environment**

1. **Create a virtual environment**:
    ```bash
    python3 -m venv venv
    ```

2. **Activate the virtual environment**:
    - On Windows:
        ```bash
        .\venv\Scripts\activate
        ```
    - On macOS and Linux:
        ```bash
        source venv/bin/activate
        ```

3. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4. **Freeze the installed dependencies**:
    ```bash
    pip freeze > requirements.txt
    ```

**Example `requirements.txt` file**:
```
numpy==2.2.1
pandas==2.2.3
matplotlib==3.10.0
```

### Unit Tests

- **Characteristics**:
    - **Isolation**: Each test should be independent and not rely on the state left by other tests.
    - **Repeatability**: Tests should produce the same results every time they are run.
    - **Clarity**: Tests should be easy to read and understand.
    - **Coverage**: Aim to cover as many code paths as possible, including edge cases.

- **Structure**: the **AAA** pattern
    - **Arrange**: Prepare the environment and inputs for the test.
    - **Act**: Run the code being tested.
    - **Assert**: Verify that the result matches the expected one.

**Example using `unittest` in Python**: in `math_operations.py`

```python
import unittest

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

class TestMathOperations(unittest.TestCase):

    def setUp(self):
        """Setup any state specific to the execution of the given class."""
        self.a = 10
        self.b = 5

    def test_add(self):
        """Test the add function."""
        result = add(self.a, self.b)
        self.assertEqual(result, 15)

    def test_subtract(self):
        """Test the subtract function."""
        result = subtract(self.a, self.b)
        self.assertEqual(result, 5)

    def tearDown(self):
        """Clean up any resources used during the test."""
        pass

if __name__ == '__main__':
    unittest.main()
```

**Running the tests**:
```bash
python -m unittest math_operations.py
```

## Conclusion

By adhering to these best practices, you will enhance the quality, readability, and maintainability of your code. This will not only make your programming assignments more robust and reliable but also prepare you for professional software development. Consistently applying these principles will lead to better collaboration, easier debugging, and a more enjoyable coding experience.

## Acknowledgements

The code snippets were generated automatically thanks to GitHub Copilot.