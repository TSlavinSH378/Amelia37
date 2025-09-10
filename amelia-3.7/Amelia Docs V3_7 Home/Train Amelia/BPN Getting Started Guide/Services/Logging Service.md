-   [Methods](#LoggingService-Methods)
    -   [debug](#LoggingService-debug)
    -   [info](#LoggingService-info)
    -   [warn](#LoggingService-warn)
    -   [error](#LoggingService-error)
-   [Examples](#LoggingService-Examples)
The logging service provides Script tasks and libraries the ability to add log entries.
# Methods
## debug
    void debug(Object somethingOrThrowable)
Logs a message as debug.

| Parameter | Description |
| ----|----|
| somthingOrThrowable | String, object, or link Throwable |

## info
    void info(Object somethingOrThrowable
Logs a message for information.

| Parameter | Description |
| ----|----|
| somthingOrThrowable | String, object, or link Throwable |

## warn
    void warn(Object somethingOrThrowable)
Logs a message as a warning.

| Parameter | Description |
| ----|----|
| somthingOrThrowable | String, object, or link Throwable |

## error
    void error(Object somethingOrThrowable)
Logs a message as an error.

| Parameter | Description |
| ----|----|
| somthingOrThrowable | String, object, or link Throwable |

# Examples
The logging service is available in Script tasks and libraries.
``` groovy
log.info("Hello world!")
```
``` groovy
try {
    foo()
} catch(TestException e) {
    log.info("Error fooing", e)
}
```
