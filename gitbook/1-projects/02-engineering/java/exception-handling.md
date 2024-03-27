
The Java Virtual Machine (JVM) handles exceptions through a process that involves the creation, throwing, and catching of exceptions. Here's a detailed explanation:

1. **Creation**: Exceptions in Java are objects. When an error occurs within a method, the method creates an object and hands it off to the runtime system. The object, called an exception object, contains information about the error, including its type and the state of the program when the error occurred.

2. **Throwing**: After an exception object is created, it is thrown by the method using the `throw` keyword. The runtime system (the JVM) then takes over and begins the process of exception handling.

3. **Catching**: To catch exceptions, a portion of code is placed within a `try` block. If an exception is thrown within the `try` block, it is caught and handled by an `catch` block. The `catch` block is a block of code that specifies the type of exception it can handle and what to do with it.

4. **Propagation**: If a method does not catch an exception (i.e., does not have an appropriate `catch` block), the method ends and the exception is thrown to the previous method on the call stack. This continues until the exception is caught or until it propagates to the `main()` method and causes the program to terminate.

5. **Finally Block**: There is also a `finally` block that can be used with `try` and `catch`. The `finally` block always executes when the `try` block exits, regardless of how the `try` block exits (unless the JVM exits while the `try` or `catch` code is being executed or an exception is thrown in the `finally` block). This makes it useful for cleanup activities that should always be performed, like closing a file or releasing a network connection.

6. **Checked and Unchecked Exceptions**: In Java, there are two types of exceptions: checked and unchecked exceptions. Checked exceptions are exceptions that are checked at compile time. If a method throws a checked exception, it must either handle the exception or it must specify the exception using the `throws` keyword. Unchecked exceptions are not checked at compile time, they are checked at runtime. These are also called runtime exceptions.

This is a high-level overview of how the JVM handles exceptions. The actual process involves many more details and complexities.

----
Examples of both checked and unchecked exceptions in Java:

Checked Exception:
```java
import java.io.*;

public class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("NonExistentFile.txt");
            BufferedReader fileInput = new BufferedReader(file);
            
            // Print first 3 lines of file "NonExistentFile.txt"
            for (int counter = 0; counter < 3; counter++) 
                System.out.println(fileInput.readLine());
            
            fileInput.close();
        } catch (FileNotFoundException fnfe) {
            // Handle the exception
            System.out.println("The specified file does not exist");
        } catch (IOException ioe) {
            // Handle the exception
            System.out.println("I/O Exception occurred");
        }
    }
}
```
In this example, `FileNotFoundException` and `IOException` are checked exceptions. The Java compiler forces you to handle these exceptions with a `try-catch` block or a `throws` clause in the method signature.

Unchecked Exception:
```java
public class UncheckedExceptionExample {
    public static void main(String[] args) {
        int[] arr = new int[3];
        try {
            // This line of code will throw an ArrayIndexOutOfBoundsException
            System.out.println(arr[5]);
        } catch (ArrayIndexOutOfBoundsException aioobe) {
            // Handle the exception
            System.out.println("Array index is out of bounds");
        }
    }
}
```
In this example, `ArrayIndexOutOfBoundsException` is an unchecked exception. The Java compiler does not force you to handle these exceptions. They are typically programming errors, like accessing an out-of-bounds array element as shown above.