# Exceptions Vs Results

Here I'm writing about how to handle error states that happens in functions and how to report the unhandled ones to caller.

The two most popular methods are **Exception** and **Result**.

## Exception

Many languages support throwing exceptions.
Throwing an exception immediately block function execution and bubble through the stack searching for a **try-catch** statement that can handle it.
If in handler is found code execution can resume it's normal flow from there.
If none is found usually program execution is interrupted and it exits with error.
Exception act as a sort of alternative execution flow.

## Result

An other solution is to recognise error states as a valid results of function execution.
A function that can have error states return a **Result<NormalReturnType,Error>** that bundle both _normal_ return value and eventual error state.
Caller function has to check if result is an error value or a non-error value and act accordingly.

## Advantages and disadvantages aka tradeoffs

Theorically both the approaches offer the same potential functionalities.
You can mimic _result_ flow with _exception_ wrapping any function call that can potentially throw within a try-catch construct.
On the other way you mimic _exception_ flow just returning any unhandled error result.

It's important to note that in async programming (callbacks, defer, promises, async functions, etc.) exception flow is handled a bit differently, sometimes similar to result approach.

So if theorically you can coherch one approach to the other the needed effort can be quite significant because you are rowing against the natural flow.

If your error handling has very low granularity and you have only few (if any) top level error handling code areas throwing exceptions can be the right choice.
The automatic exception bubbling can save you much code and complexity.
For example a cli that just terminate on error or a ui app that show generic error message (ex. "An error occurred. Please retry. If the problem persists contact us.") are examples of programs that can take advantage from this approach.

If you want a more granular error management because for example trying to recover and resume normal execution or cleanup inconsistent states, function that return results can be preferable.
Complex applications or that manage a persistent state (ex. DB) usually are in this category.

## An important difference

In many typed languages exceptions have an additional weakness: they aren't part of function signature.
This weakness prevent compiler from checking that exception are correctly handled.
Worst than this function documentation will lack references to throwable exceptions unless developers write down about it in function description and maintain it as code evolves.
Even if function documentation about throwable exceptions is correctly maintained when one change all the other functions calling this one without catching possible exceptions must have its documentation updated.
This goes on recursively aka a mess. Even more considering external libraries.
Without automations possible with exceptions in function signature only, it's a lost war don't worth fighting.

In my opinion Java is an uncommon example of good exception management. In Java methods you have to declare thrown exceptions, including uncatched ones, using keyword **throws**.
This way throwable exceptions get part of method signature, get checked by compiler and automatically updated in documentation.

## My experience and opinion
