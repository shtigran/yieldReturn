# Yield 
# C#6.0  .NET FRAMEWORK 4.6

----

![alt text](https://image.slidesharecdn.com/theevolutionofasyncprogramminggztechpartycsharp-120225233445-phpapp01/95/the-evolution-of-async-programming-gz-techparty-c-17-728.jpg?cb=1330213317)

----

# Description

When you use the yield keyword in a statement, you indicate that the method, operator, or get accessor in which it appears is an iterator. Using yield to define an iterator removes the need for an explicit extra class (the class that holds the state for an enumeration, see IEnumerator<T> for an example) when you implement the IEnumerable and IEnumerator pattern for a custom collection type.
The following example shows the two forms of the yield statement.
```C#
yield return <expression>;  
yield break;  
```
# Remarks
----
You use a yield return statement to return each element one at a time.
You consume an iterator method by using a foreach statement or LINQ query. Each iteration of the foreach loop calls the iterator method. When a yield return statement is reached in the iterator method, expression is returned, and the current location in code is retained. Execution is restarted from that location the next time that the iterator function is called.
You can use a yield break statement to end the iteration.
