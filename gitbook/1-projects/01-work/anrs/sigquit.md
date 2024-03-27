

 [Termination Signals (The GNU C Library)](https://www.gnu.org/software/libc/manual/html_node/Termination-Signals.html)
- Termination signals are used to instruct a process to terminate gracefully, allowing it to tidy up before exiting.
- SIGTERM is a generic signal for program termination that can be blocked, handled, or ignored, commonly used to politely ask a program to terminate.
- SIGINT is sent when the user types Ctrl+C, indicating a program interrupt.
- **SIGQUIT**, triggered by Ctrl+, is similar to SIGINT but produces a core dump when terminating, useful for user-detected program error conditions.
- SIGKILL causes immediate and unblockable program termination, typically used as a last resort after other signals fail.
- SIGHUP signals a hang-up, such as a terminal disconnection or termination of the controlling process, affecting all processes associated with the session.




When running sleep 10
```
sleep 10
```

when we stop it with ctrl + c, then the return code is 130 
130 - **Command terminated by user**.

`$?` is a built-in variable that stores the exit status of a command, function, or the script itself.

`$?` reads the exit status of the last command executed. After a function returns, `$?` gives the exit status of the last command executed in the function. This is Bash's way of giving functions a "return value." It returns `0` on success or an integer in the range `1 - 255` on error.

```
echo $? 
```

this gives the return type.
