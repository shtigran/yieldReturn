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

You use a yield return statement to return each element one at a time.
You consume an iterator method by using a foreach statement or LINQ query. Each iteration of the foreach loop calls the iterator method. When a yield return statement is reached in the iterator method, expression is returned, and the current location in code is retained. Execution is restarted from that location the next time that the iterator function is called.
You can use a yield break statement to end the iteration.

----

# Iterator Methods and get Accessors

The declaration of an iterator must meet the following requirements:
The return type must be IEnumerable, IEnumerable<T>, IEnumerator, or IEnumerator<T>.
The declaration can't have any ref or out parameters.
The yield type of an iterator that returns IEnumerable or IEnumerator is object. If the iterator returns IEnumerable<T> or IEnumerator<T>, there must be an implicit conversion from the type of the expression in the yield return statement to the generic type parameter .
You can't include a yield return or yield break statement in methods that have the following characteristics:
Anonymous methods. For more information.
Methods that contain unsafe blocks. 

----

# Exception Handling

A yield return statement can't be located in a try-catch block. A yield return statement can be located in the try block of a try-finally statement.
A yield break statement can be located in a try block or a catch block but not a finally block.
If the foreach body (outside of the iterator method) throws an exception, a finally block in the iterator method is executed.

----

# Technical Implementation

The following code returns an IEnumerable<string> from an iterator method and then iterates through its elements.
```C#
IEnumerable<string> elements = MyIteratorMethod();  
foreach (string element in elements)  
{  
   …  
}  
```
The call to MyIteratorMethod doesn't execute the body of the method. Instead the call returns an IEnumerable<string> into the elements variable.
On an iteration of the foreach loop, the MoveNext method is called for elements. This call executes the body of MyIteratorMethod until the next yield return statement is reached. The expression returned by the yield return statement determines not only the value of the element variable for consumption by the loop body but also the Current property of elements, which is an IEnumerable<string>.
On each subsequent iteration of the foreach loop, the execution of the iterator body continues from where it left off, again stopping when it reaches a yield return statement. The foreach loop completes when the end of the iterator method or a yield break statement is reached.

----

# Example description

The following example has a yield return statement that's inside a for loop. Each iteration of the foreach statement body in Process creates a call to the Power iterator function. Each call to the iterator function proceeds to the next execution of the yield return statement, which occurs during the next iteration of the for loop.
The return type of the iterator method is IEnumerable, which is an iterator interface type. When the iterator method is called, it returns an enumerable object that contains the powers of a number.

# Example code
```C#
static void Main(string[] args)
        {
            // Display powers of 2 up to the exponent of 8:
            foreach (int i in Power(2, 8))
            {
                Console.Write("{0} ", i);
            }

            Console.ReadKey();
        }

        public static IEnumerable<int> Power(int number, int exponent)
        {
            int result = 1;

            for (int i = 0; i < exponent; i++)
            {
                result = result * number;
                yield return result;
            }
        }

        // Output: 2 4 8 16 32 64 128 256
    }
```
----
----

# Speaking popular language

Use yield-return when You calculate the next item in the list (or even the next group of items).

Using your Version 2, you must have the complete list before returning. By using yield-return, you really only need to have the next item before returning.

Among other things, this helps spread the computational cost of complex calculations over a larger time-frame. For example, if the list is hooked up to a GUI and the user never goes to the last page, you never calculate the final items in the list.

Another case where yield-return is preferable is if the IEnumerable represents an infinite set. Consider the list of Prime Numbers, or an infinite list of random numbers. You can never return the full IEnumerable at once, so you use yield-return to return the list incrementally.
