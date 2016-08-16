#Java 8 —— 功能接口
功能接口只有一个功能显示。比如，有一个compareTo方法的Comparable接口被使用为了比较。Java 8已经定义了大量功能接口，在Lambda表达式中广泛使用。以下是定义在java.util.Function包中的功能接口列表：
```
S. No.	Interface & Description
1	BiConsumer<T,U>
Represents an operation that accepts two input arguments, and returns no result.

2	BiFunction<T,U,R>
Represents a function that accepts two arguments and produces a result.

3	BinaryOperator<T>
Represents an operation upon two operands of the same type, producing a result of the same type as the operands.

4	BiPredicate<T,U>
Represents a predicate (Boolean-valued function) of two arguments.

5	BooleanSupplier
Represents a supplier of Boolean-valued results.

6	Consumer<T>
Represents an operation that accepts a single input argument and returns no result.

7	DoubleBinaryOperator
Represents an operation upon two double-valued operands and producing a double-valued result.

8	DoubleConsumer
Represents an operation that accepts a single double-valued argument and returns no result.

9	DoubleFunction<R>
Represents a function that accepts a double-valued argument and produces a result.

10	DoublePredicate
Represents a predicate (Boolean-valued function) of one double-valued argument.

11	DoubleSupplier
Represents a supplier of double-valued results.

12	DoubleToIntFunction
Represents a function that accepts a double-valued argument and produces an int-valued result.

13	DoubleToLongFunction
Represents a function that accepts a double-valued argument and produces a long-valued result.

14	DoubleUnaryOperator
Represents an operation on a single double-valued operand that produces a double-valued result.

15	Function<T,R>
Represents a function that accepts one argument and produces a result.

16	IntBinaryOperator
Represents an operation upon two int-valued operands and produces an int-valued result.

17	IntConsumer
Represents an operation that accepts a single int-valued argument and returns no result.

18	IntFunction<R>
Represents a function that accepts an int-valued argument and produces a result.

19	IntPredicate
Represents a predicate (Boolean-valued function) of one int-valued argument.

20	IntSupplier
Represents a supplier of int-valued results.

21	IntToDoubleFunction
Represents a function that accepts an int-valued argument and produces a double-valued result.

22	IntToLongFunction
Represents a function that accepts an int-valued argument and produces a long-valued result.

23	IntUnaryOperator
Represents an operation on a single int-valued operand that produces an int-valued result.

24	LongBinaryOperator
Represents an operation upon two long-valued operands and produces a long-valued result.

25	LongConsumer
Represents an operation that accepts a single long-valued argument and returns no result.

26	LongFunction<R>
Represents a function that accepts a long-valued argument and produces a result.

27	LongPredicate
Represents a predicate (Boolean-valued function) of one long-valued argument.

28	LongSupplier
Represents a supplier of long-valued results.

29	LongToDoubleFunction
Represents a function that accepts a long-valued argument and produces a double-valued result.

30	LongToIntFunction
Represents a function that accepts a long-valued argument and produces an int-valued result.

31	LongUnaryOperator
Represents an operation on a single long-valued operand that produces a long-valued result.

32	ObjDoubleConsumer<T>
Represents an operation that accepts an object-valued and a double-valued argument, and returns no result.

33	ObjIntConsumer<T>
Represents an operation that accepts an object-valued and an int-valued argument, and returns no result.

34	ObjLongConsumer<T>
Represents an operation that accepts an object-valued and a long-valued argument, and returns no result.

35	Predicate<T>
Represents a predicate (Boolean-valued function) of one argument.

36	Supplier<T>
Represents a supplier of results.

37	ToDoubleBiFunction<T,U>
Represents a function that accepts two arguments and produces a double-valued result.

38	ToDoubleFunction<T>
Represents a function that produces a double-valued result.

39	ToIntBiFunction<T,U>
Represents a function that accepts two arguments and produces an int-valued result.

40	ToIntFunction<T>
Represents a function that produces an int-valued result.

41	ToLongBiFunction<T,U>
Represents a function that accepts two arguments and produces a long-valued result.

42	ToLongFunction<T>
Represents a function that produces a long-valued result.

43	UnaryOperator<T>
Represents an operation on a single operand that produces a result of the same type as its operand.
```