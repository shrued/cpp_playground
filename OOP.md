# OOP Concepts in C++

## 1. Introduction to OOP

- **Definition**: OOP is a programming paradigm based on the concept of "objects", which are instances of classes.
- **Four Pillars of OOP**:
  - **Encapsulation**
  - **Abstraction**
  - **Inheritance**
  - **Polymorphism**

## 2. Classes and Objects

- **Class**: A blueprint for objects.
- **Object**: An instance of a class.
- **Syntax**:

```
  class ClassName {
  public:
  // Access specifier
  // Data Members
  // Member Functions
  };
```

## 3. Encapsulation

- **Definition**: Encapsulation is the bundling of data and methods that operate on that data within one unit (class), and restricting access to some of the object's components.
- **Access Specifiers**:
  - `public`
  - `private`
  - `protected`
- **Example**:

```
  class EncapsulatedClass {
  private:
  int x;
  public:
  void setX(int a) { x = a; }
  int getX() { return x; }
  };
```

## 4. Abstraction

- **Definition**: Abstraction is the concept of hiding the complex implementation details and showing only the essential features of the object.
- **Abstract Class**: A class that cannot be instantiated.
- **Pure Virtual Function**:

```
  class AbstractClass {
  public:
  virtual void pureVirtualFunction() = 0;
  };
```

## 5. Inheritance

- **Definition**: Inheritance is the mechanism by which one class (derived class) inherits the properties and behavior of another class (base class).
- **Types of Inheritance**:
  - Single Inheritance
  - Multiple Inheritance
  - Multilevel Inheritance
  - Hierarchical Inheritance
  - Hybrid Inheritance
- **Syntax**:

```
  class BaseClass {
  // Base class code
  };

  class DerivedClass : public BaseClass {
  // Derived class code
  };
```

NOTE:

- Inheritance: Allows a subclass to override methods defined in its superclass, promoting code reuse and specialization.
- Interfaces: Define a contract where implementing classes must provide concrete implementations for all methods declared in the interface, promoting loose coupling and polymorphic behavior.

## 6. Polymorphism

- **Definition**: Polymorphism allows objects to be treated as instances of their parent class rather than their actual class.
- **Types of Polymorphism**:
  - Compile-time Polymorphism (Function Overloading and Operator Overloading)
  - Run-time Polymorphism (Virtual Functions)
- **Function Overloading**:

```
  class FunctionOverload {
  public:
  void func(int x) { /_ ... _/ }
  void func(double y) { /_ ... _/ }
  };
```

- **Virtual Functions**:

```
  class BaseClass {
  public:
  virtual void display() { /_ ... _/ }
  };

  class DerivedClass : public BaseClass {
  public:
  void display() override { /_ ... _/ }
  };
```

NOTE:

- **Why `delete test` is Necessary**:
- Dynamic Memory Allocation:
  When you use new to create an object, memory for that object is allocated on the heap (dynamic memory).
  A* test = new B(); allocates memory for an object of type B and returns a pointer to it. The test pointer is of type A*.

- Memory Management:
  Memory allocated with new must be explicitly freed using delete to avoid memory leaks.
  If you do not call delete, the memory allocated for the object remains allocated until the program terminates, which can lead to memory leaks, especially in long-running programs or those that frequently allocate memory dynamically.

- Calling Destructors:
  When delete is called, the destructor of the object is invoked to perform any necessary cleanup.
  If the destructor is virtual, the correct destructor for the actual object type (in this case, B) is called, ensuring proper resource release and cleanup.

## 7. Constructors and Destructors

- **Constructor**: Special member function that initializes objects.

```
  class MyClass {
  public:
  MyClass() { /_ Constructor code _/ }
  };
```

- **Destructor**: Special member function that is executed when an object goes out of scope.

```
  class MyClass {
  public:
  ~MyClass() { /_ Destructor code _/ }
  };
```

- **Default Destructors**:
If you do not define a destructor, the compiler provides a default destructor that performs a shallow cleanup (deallocates the object but does not handle dynamic memory or resources specifically allocated within the object).

- **Non-Virtual Destructors**:
If a base class destructor is not virtual and you delete an object through a base class pointer, only the base class destructor will be called, leading to potential resource leaks in derived classes.

- **Virtual Destructors**:
Declaring a destructor as virtual in a base class ensures that the destructor of the derived class is called when an object is deleted through a base class pointer. This ensures proper cleanup of resources.

## 8. Operator Overloading

- **Definition**: Operator overloading allows you to redefine the way operators work for user-defined types.
- **Example**:

```
  class Complex {
  private:
  int real, imag;
  public:
  Complex operator + (const Complex& obj) {
  Complex temp;
  temp.real = real + obj.real;
  temp.imag = imag + obj.imag;
  return temp;
  }
  };
```

## 9. Inheritance and Access Control

- **Public Inheritance**: Derived class inherits public and protected members of the base class as public and protected members.
- **Protected Inheritance**: Derived class inherits public and protected members of the base class as protected members.
- **Private Inheritance**: Derived class inherits public and protected members of the base class as private members.

## 10. Static Members

- **Static Data Members**: Shared among all objects of a class.

```
  class MyClass {
  public:
  static int staticVar;
  };
  int MyClass::staticVar = 0;
```

- **Static Member Functions**: Can be called without an object.

```
  class MyClass {
  public:
  static void staticFunction() { /_ ... _/ }
  };
```

## 11. Friend Functions and Classes

- **Friend Function**: A function that is not a member of the class but has access to its private and protected members.

```
  class MyClass {
  private:
  int x;
  public:
  friend void friendFunction(MyClass &obj);
  };

  void friendFunction(MyClass &obj) {
  obj.x = 10;
  }
```

- **Friend Class**: A class that has access to the private and protected members of another class.

```
  class ClassA {
  private:
  int x;
  public:
  friend class ClassB;
  };

  class ClassB {
  public:
  void setX(ClassA &obj, int value) {
  obj.x = value;
  }
  };
```

## 12. Exception Handling

- **Try, Catch, and Throw**:

```
  try {
  // Code that may throw an exception
  } catch (Type exception) {
  // Code to handle the exception
  }

  throw exception;
```

## 13. Templates

- **Function Templates**:

```
  template <typename T>
  T myMax(T a, T b) {
  return (a > b) ? a : b;
  }
```

- **Class Templates**:

```
  template <class T>
  class MyClass {
  private:
  T data;
  public:
  MyClass(T a) : data(a) {}
  T getData() { return data; }
  };
```

## 14. STL (Standard Template Library)

- **Containers**: Vector, List, Deque, Set, Map, etc.
- **Algorithms**: Sort, Search, Count, etc.
- **Iterators**: To traverse containers.

## 15. Lambda Expressions

- **Syntax**:

```
  auto lambda = [](int x, int y) { return x + y; };
  int result = lambda(2, 3); // result = 5
```

## 16. Smart Pointers

- **Types**:
  - `std::unique_ptr`
  - `std::shared_ptr`
  - `std::weak_ptr`
- **Example**:

```
  std::unique_ptr<int> ptr(new int(10));
  std::shared_ptr<int> ptr2 = std::make_shared<int>(20);
```

## 17. Move Semantics

- **Move Constructor**:

```
  class MyClass {
  public:
    MyClass(MyClass&& other) noexcept {
      // Move resources
    }
  };
```

- **Move Assignment Operator**:

```
  MyClass& operator=(MyClass&& other) noexcept {
    if (this != &other) {
      // Release current resources
      // Acquire other's resources
    }
    return \*this;
  }
```

## 18. Concurrency

- **Threads**:

```
  std::thread t1(functionName);
  t1.join();
```

## 19. Design Patterns

- **Singleton**:

```
  class Singleton {
  private:
    static Singleton* instance;
    Singleton() {}
  public:
    static Singleton* getInstance() {
      if (!instance)
        instance = new Singleton();
      return instance;
    }
  };
  Singleton\* Singleton::instance = nullptr;
```

## 20. Best Practices

- Use `const` keyword wherever applicable.
- Prefer `auto` for type inference.
- Initialize member variables.
- Follow RAII (Resource Acquisition Is Initialization) principle.
