---
layout: post
title: 'C# 7 New Features'
tags: ['C#']
categories: ['C#']
date: '2017-03-20 23:45'
author: 'GaryNg'
---

# C# 7 New Features

Refer to [New Features in C# 7.0](https://blogs.msdn.microsoft.com/dotnet/2017/03/09/new-features-in-c-7-0/)

GitHub Demo Repo: https://github.com/garyng/csharp_7_new_features

## Xamarin Workbook
A much better way to explore C# 7.0 new features: [https://github.com/xamarin/Workbooks/blob/master/csharp/csharp7/csharp7.workbook](https://github.com/xamarin/Workbooks/blob/master/csharp/csharp7/csharp7.workbook)

# Code
## Out Variables
```csharp
[TestClass]
public class Out_Variables
{
	[TestMethod]
	public void Old_Out_Variables()
	{
		// have to "predeclare"
		int num;
		int.TryParse("123", out num);
		num.Should().Be(123);
	}

	[TestMethod]
	public void New_Out_Variables()
	{
		int.TryParse("123", out int num);
		// subsequent line can use 'num'
		num.Should().Be(123);
	}

	[TestMethod]
	public void New_Out_Variables_Using_Var()
	{
		// compiler can figure out what is the type
		int.TryParse("123", out var num);
		num.Should().Be(123);
	}

	[TestMethod]
	public void Discard_Out_Variables()
	{
		// only the return value is stored
		bool success = int.TryParse("123", out _);
	}
}
```

## Deconstruction
```csharp
[TestClass]
public class Deconstruction
{
	[TestMethod]
	public void Deconstruct_Returned_Tuples()
	{
		(string first, string middle, string last) = LookupName("123123");

		first.Should().Be("123");
		middle.Should().Be("456");
		last.Should().Be("789");
	}

	[TestMethod]
	public void Deconstruct_Returned_Tuples_Using_Multiple_Var()
	{
		(var first, var middle, var last) = LookupName("123123");

		first.Should().Be("123");
		middle.Should().Be("456");
		last.Should().Be("789");
	}

	[TestMethod]
	public void Deconstruct_Returned_Tuples_Using_Single_Var()
	{
		var (first, middle, last) = LookupName("123123");

		first.Should().Be("123");
		middle.Should().Be("456");
		last.Should().Be("789");
	}

	(string, string, string) LookupName(string id)
	{
		return ("123", "456", "789");
	}

	[TestMethod]
	public void Deconstructing_Other_Type()
	{
		// Deconstruction is not just for tuples.
		// Any type can be deconstructed, as long as it has an (instance or extension) deconstructor method
		// of the form:
		// public void Deconstruct(out T1 x1, ..., out Tn xn) { ... }

		var (x, y) = new Point(1, 2);
		x.Should().Be(1);
		y.Should().Be(2);
	}

	[TestMethod]
	public void Deconstruction_Other_Type_With_Discards()
	{
		var (x, _) = new Point(1, 2);
		x.Should().Be(1);
	}

	public class Point
	{
		public int X { get; set; }
		public int Y { get; set; }

		public Point(int x, int y)
		{
			X = x;
			Y = y;
		}

		public void Deconstruct(out int x, out int y)
		{
			x = X;
			y = Y;
		}
	}
}
```

## More Expression Bodied Members
```csharp
[TestClass]
public class Expression_Bodied_Members
{
  public class Person
  {
    private static ConcurrentDictionary<int, string> names = new ConcurrentDictionary<int, string>();
    private int id = 1;

    // Constructors
    public Person(string name) => names.TryAdd(id, name);

    // Deconstructors
    ~Person() => names.TryRemove(id, out _);

    public string Name
    {
      // Getters
      get => names[id];

      // Setters
      set => names[id] = value;
    }
  }
}
```

## Generalized Async Return Types
Refer to SO: [In C#7, how can I “roll my own” Task-like type to use with async?](http://stackoverflow.com/a/42753797/1023180)

## Literal Improvements
```csharp
[TestClass]
public class Literal_Improvements
{
  [TestMethod]
  public void Digit_Seperators_Have_No_Effect_On_The_Value()
  {
    var d = 123_456;
    d.Should().Be(123456);
  }

  [TestMethod]
  public void Binary_Literals()
  {
    var b = 0b1111_1111;
    b.Should().Be(0xFF);
  }
}
```

## Local Functions
```csharp
[TestClass]
public class Local_Functions
{
  [TestMethod]
  public void Fibonacci_First_Term_Should_Be_1()
  {
    Fibonacci(0).Should().Be(1);
  }

  [TestMethod]
  public void Fibonacci_2nd_Term_Should_Be_1()
  {
    Fibonacci(1).Should().Be(1);
  }

  [TestMethod]
  public void Fibonacci_5th_Term_Should_Be_5()
  {
    Fibonacci(4).Should().Be(5);
  }

  public int Fibonacci(int x)
  {
    if (x < 0) throw new ArgumentException("Must larger than 0", nameof(x));
    return Fib(x).current;

    (int current, int previous) Fib(int i)
    {
      if (i == 0) return (1, 0);
      var (c, p) = Fib(i - 1);
      return (c + p, c);
    }
  }

  // other example from MSDN article: https://blogs.msdn.microsoft.com/dotnet/2017/03/09/new-features-in-c-7-0/

  public IEnumerable<T> Filter<T>(IEnumerable<T> source, Func<T, bool> filter)
  {
    if (source == null) throw new ArgumentNullException(nameof(source));
    if (filter == null) throw new ArgumentNullException(nameof(filter));

    return Iterator();

    IEnumerable<T> Iterator()
    {
      foreach (var element in source)
      {
        if (filter(element)) { yield return element; }
      }
    }
  }
}
```
## Pattern Matching

> Not very well written, refer to original article on .NET Blog

```csharp
[TestClass]
public class Pattern_Matching
{
  // test a value whether it has certain "shape"
  // and extract information from the value when it does

  [TestMethod]
  public void Null_Variable_Should_Be_Null()
  {
    object o = null;
    bool check = o is null;
    check.Should().BeTrue();
  }

  [TestMethod]
  public void Int_Variable_Should_Be_Int()
  {
    object o = 123;
    bool check = o is int;
    check.Should().BeTrue();
  }

  [TestMethod]
  public void Non_Int_Variable_Should_Not_Be_Int()
  {
    object o = "123";
    bool check = o is int;
    check.Should().BeFalse();
  }

  [TestMethod]
  public void Pattern_Variables()
  {
    object o = 123;
    // must ensure o is an int
    // otherwise compiler will throw "Use of unassigned local variable i"
    //bool check = o is int i;
    //i.Should().Be(123);

    // i is introduced by a pattern
    // it is called a "pattern variable"
    if (o is int i)
    {
      i.Should().Be(123);
    }
    else
    {
      Assert.Fail();
    }
  }

  [TestClass]
  public class Patterns_With_TryXXX_Methods
  {
    [TestMethod]
    public void Object_Which_Is_An_Int_Should_Be_Unboxed_To_Int()
    {
      object o = 123;
      if (o is int i ||
        (o is string s && int.TryParse(s, out i)))
      {
        i.Should().Be(123);
      }
    }

    [TestMethod]
    public void Object_Which_Is_A_String_Should_Be_Parsed_To_Int()
    {
      object o = "123";
      if (o is int i ||
        (o is string s && int.TryParse(s, out i)))
      {
        i.Should().Be(123);
      }
    }
  }

  [TestClass]
  public class Switch_Statements_With_Patterns
  {
    // 1. the order of case clauses now matters
    // 2. the default clause is always evaluated last

    [TestMethod]
    public void Shape_Is_A_Circle()
    {
      Shape shape = new Circle()
      {
        Radius = 10
      };

      switch (shape)
      {
        case Circle c:
          c.Radius.Should().Be(10);
          break;
        case Rectangle r when (shape.Length == shape.Height):
          r.Length.Should().Be(r.Height);
          break;
        case Rectangle r:
          r.Length.Should().Be(10);
          r.Length.Should().Be(20);
          break;
        default:
          Assert.Fail("Unknown shape");
          break;
        case null:
          Assert.Fail("Should not be null");
          break;
      }
    }

    [TestMethod]
    public void Shape_Is_A_Square()
    {
      Shape shape = new Rectangle()
      {
        Length = 10,
        Height = 10
      };

      switch (shape)
      {
        case Circle c:
          c.Radius.Should().Be(10);
          break;
        case Rectangle r when (shape.Length == shape.Height):
          r.Length.Should().Be(r.Height);
          break;
        case Rectangle r:
          r.Length.Should().Be(10);
          r.Height.Should().Be(20);
          break;
        default:
          Assert.Fail("Unknown shape");
          break;
        case null:
          Assert.Fail("Should not be null");
          break;
      }
    }

    [TestMethod]
    public void Shape_Is_A_Rectangle()
    {
      Shape shape = new Rectangle()
      {
        Length = 10,
        Height = 20
      };

      switch (shape)
      {
        case Circle c:
          c.Radius.Should().Be(10);
          break;
        case Rectangle r when (shape.Length == shape.Height):
          r.Length.Should().Be(r.Height);
          break;
        case Rectangle r:
          r.Length.Should().Be(10);
          r.Height.Should().Be(20);
          break;
        default:
          Assert.Fail("Unknown shape");
          break;
        case null:
          Assert.Fail("Should not be null");
          break;
      }
    }

    [TestMethod]
    public void Shape_Is_A_Null()
    {
      Shape shape = null;

      switch (shape)
      {
        case Circle c:
          c.Radius.Should().Be(10);
          break;
        case Rectangle r when (shape.Length == shape.Height):
          r.Length.Should().Be(r.Height);
          break;
        case Rectangle r:
          r.Length.Should().Be(10);
          r.Length.Should().Be(20);
          break;
        default:
          Assert.Fail("Unknown shape");
          break;
        case null:
          Assert.Fail("Should not be null");
          break;
      }
    }

    [TestMethod]
    public void Shape_Is_A_Not_A_Shape()
    {
      Shape shape = new NotAShape();

      switch (shape)
      {
        case Circle c:
          c.Radius.Should().Be(10);
          break;
        case Rectangle r when (shape.Length == shape.Height):
          r.Length.Should().Be(r.Height);
          break;
        case Rectangle r:
          r.Length.Should().Be(10);
          r.Length.Should().Be(20);
          break;
        default:
          Assert.Fail("Unknown shape");
          break;
        case null:
          Assert.Fail("Should not be null");
          break;
      }
    }

    public class Shape
    {
      public int Length { get; set; }
      public int Height { get; set; }
    }
    public class Circle : Shape
    {
      public int Radius { get; set; }
    }
    public class Rectangle : Shape
    {
    }
    public class NotAShape : Shape
    {

    }
  }
}
```

## Ref Returns and Ref Locals
```csharp
[TestClass]
public class Ref_Returns_And_Locals
{
  // Return value by reference
  // Store them by reference in local variables

  [TestMethod]
  public void Return_Value_By_Reference_And_Store_It_By_Reference()
  {
    int[] array = { 1, 2, 3, 4, 5, 6 };
    ref int found = ref Find(6, array);
    // change the value
    found = 12;
    array[5].Should().Be(12);
  }

  public ref int Find(int num, int[] numbers)
  {
    foreach (int i in numbers)
    {
      if (numbers[i] == num)
      {
        // return the storage location not the value
        return ref numbers[i];
      }
    }

    throw new IndexOutOfRangeException($"{nameof(num)} not found");
  }
}
```

## Throw Expression
```csharp
[TestClass]
public class Throw_Expressions
{
  public class Person
  {
    public string Name { get; }

    public Person(string name) => Name = name ?? throw new ArgumentNullException(nameof(name));

    public string GetFirstName()
    {
      var parts = Name.Split(' ');
      return (parts.Length > 1) ? parts[0] : throw new InvalidOperationException("No name!");
    }

    public string GetLastName() => throw new NotImplementedException();
  }

  [TestMethod]
  [ExpectedException(typeof(ArgumentNullException))]
  public void Person_With_Null_Name_Should_Throw_Argument_Null_Exception()
  {
    Person p = new Person(null);
  }

  [TestMethod]
  [ExpectedException(typeof(InvalidOperationException))]
  public void GetFirstName_Should_Throw_Invalid_Operation_Exception_When_Name_Is_Empty()
  {
    Person p = new Person("123");
    p.GetFirstName();
  }
}
```

## Tuples
```csharp
[TestClass]
public class Tuples
{
  // require NuGet package "System.ValueTuple" to be installed

  [TestMethod]
  public void Tuple_With_Default_Names()
  {
    var names = LookupName("123123");

    names.Item1.Should().Be("123");
    names.Item2.Should().Be("456");
    names.Item3.Should().Be("789");
  }

  (string, string, string) LookupName(string id)
  {
    return ("123", "456", "789");
  }

  [TestMethod]
  public void Tuple_With_Descriptive_Names()
  {
    var names = LookupNameDescriptive("123123");

    names.First.Should().Be("123");
    names.Middle.Should().Be("456");
    names.Last.Should().Be("789");
  }

  (string First, string Middle, string Last) LookupNameDescriptive(string id)
  {
    return ("123", "456", "789");
  }

}
```
