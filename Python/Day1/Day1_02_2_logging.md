### Using the `logging` Module

The `logging` module in Python provides a flexible framework for emitting log messages from Python programs. It is used to track events that happen when some software runs. The module helps you keep track of when and where certain parts of your code are executed, making it easier to debug and understand program flow.

### Basic Setup and Usage

1. **Basic Configuration**: Setting up basic logging configuration to log messages to the console.
2. **Logging Levels**: Understanding different logging levels (`DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`).
3. **Logging Messages**: Logging messages at various levels.

### Example Code

```python
import logging

# Basic configuration for logging
logging.basicConfig(level=logging.DEBUG,
                    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# Create a logger object
logger = logging.getLogger(__name__)

# Log messages at different levels
logger.debug('This is a debug message')
logger.info('This is an info message')
logger.warning('This is a warning message')
logger.error('This is an error message')
logger.critical('This is a critical message')
```

### Explanation

1. **Basic Configuration**:
    - `level=logging.DEBUG`: Sets the logging level to `DEBUG`, which means all levels (`DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`) will be logged.
    - `format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'`: Specifies the format of the log messages, including the timestamp, logger name, log level, and the message.

2. **Logging Levels**:
    - `DEBUG`: Detailed information, typically of interest only when diagnosing problems.
    - `INFO`: Confirmation that things are working as expected.
    - `WARNING`: An indication that something unexpected happened, or indicative of some problem in the near future (e.g., ‘disk space low’). The software is still working as expected.
    - `ERROR`: Due to a more serious problem, the software has not been able to perform some function.
    - `CRITICAL`: A very serious error, indicating that the program itself may be unable to continue running.

3. **Logging Messages**:
    - Use `logger.debug()`, `logger.info()`, `logger.warning()`, `logger.error()`, and `logger.critical()` to log messages at different levels.

### Example Output

```plaintext
2024-08-01 12:00:00,123 - __main__ - DEBUG - This is a debug message
2024-08-01 12:00:00,124 - __main__ - INFO - This is an info message
2024-08-01 12:00:00,125 - __main__ - WARNING - This is a warning message
2024-08-01 12:00:00,126 - __main__ - ERROR - This is an error message
2024-08-01 12:00:00,127 - __main__ - CRITICAL - This is a critical message
```

This output shows log messages at different levels, formatted with a timestamp, logger name, log level, and the actual message.

### Additional Configuration

The `logging` module can also be configured to log messages to a file, handle different formats, and more advanced use cases. Here is an example of logging to a file:

```python
import logging

# Basic configuration for logging to a file
logging.basicConfig(filename='app.log',
                    level=logging.DEBUG,
                    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# Create a logger object
logger = logging.getLogger(__name__)

# Log messages at different levels
logger.debug('This is a debug message')
logger.info('This is an info message')
logger.warning('This is a warning message')
logger.error('This is an error message')
logger.critical('This is a critical message')
```

This setup logs all messages to a file named `app.log` instead of the console.

By using the `logging` module, you can keep track of what your code is doing, which helps in debugging and maintaining your software.
