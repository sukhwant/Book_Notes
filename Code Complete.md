

[TOC]



# Working Classes

A class is a collection of data and routines that share a cohesive, well defined responsibility.

## Benifts of Using ADT

1. You can hide the implementation.
2. Changes do not affect the whole program.
3. You can make the interface more informative.
4. It is easier to improve performance.
5. The program is more obviously correct.
6. You don't have to pass data all over your program.
7. You are able to work with real world entities rather than low level implementations.

Example of ADT:

```java

collingSystem.getTemperature();
collingSystem.setCircular();
collingSystem.openValve();
collingSystem.closeValue();
```



ADT form the foundation for the concept of classes. One way to think about class is an abstract data type with inheritance and polymorphism.



## Good Class Interface

1. **Good Abstraction -** 

   1. Abstraction is the ability to view a complex operation in a simplified form.
   2. The class's interface should offer a group of routines that clearly belong together.
   3. Present a consistent level of abstraction in the class interface.
   4. Be sure what abstraction the class is implementing.
   5. Provide services in pairs with their opposites.
   6. Move unrelated information to another class.
   7. Make interface programmatic rather than semantic(assumptions etc.) when possible. The semantic part should be documented.Use Assertions to make semantic programmatic.
   8. Beware of erossion of the interface's abstraction under modification.
   9. DOn't add public methods that are inconsistent with the interface abstraction.
   10. Consider abstraction and cohesion together.

   Ex - Good Abstraction

   ```c++
   class Employee {
   public:
      // public constructors and destructors
      Employee();
      Employee(
         FullName name,
         String address,
         String workPhone,
         String homePhone,
         TaxId taxIdNumber,
         JobClassification jobClass
      );
      virtual ~Employee();
      // public routines
      FullName GetName() const;
      String GetAddress() const;
      String GetWorkPhone() const;
      String GetHomePhone() const;
      TaxId GetTaxIdNumber() const;
      JobClassification GetJobClassification() const;
      ...
   private:
      ...
   ```

   Ex -  Bad Abstraction

   ```c++
   class Program {
   public:
      ...
      // public routines
      void InitializeCommandStack();
      void PushCommand( Command command );
      Command PopCommand();
      void ShutdownCommandStack();
      void InitializeReportFormatting();
      void FormatReport( Report report );
      void PrintReport( Report report );
      void InitializeGlobalData();
      void ShutdownGlobalData();
      ...
   private:
      ...
   };
   ```

   - Expose only what is needed.
   - There should be consistency in what all the class is exposing.
   - Do not expose private methods.

   Ex -  Class interface with moxed level of Abstraction

   ```c++
   class EmployeeCenus: public ListContainer {
   public:
      ...
      // public routines
      void AddEmployee( Employee employee );       <-- 1
      void RemoveEmployee( Employee employee );    <-- 1
   
      Employee NextItemInList();                   <-- 2
      Employee FirstItem();              
      Employee LastItem();                  		<-- 2
      ...
   private:
      ...
   };
   ```

   - The abstraction of these routines is at the "employee" level.
   - The abstraction of these routines is at the "list" level.

2. **Good Encapsulation - **

   1. Minimize accessibility of classes and members.
   2. Don't expose member data in public.
   3. Avoid putting private implementation details into a class's interface.
   4. DOn't make assumptions about the class users.
   5. Avoid friend functions.
   6. Don't put a routine into the public interface just because it uses onlu public routines.
   7. Favor read time convenience to write time convenience.
   8. Be very very wary of semantic violations of encapsulation.
   9. Watch for coupling that's too tight.
      - minimize accessibility of classes and members.
      - Avoid friend classes.
      - Make data private rather than protected in the base class to make derived classes less tightly coupled to the base class.
      - Avoid exposing member data in the class's public interface.
      - Observe the Law of Demeter.

## Design and Implementation Issues

1. **Containment("has a") -** 

   1. Implement "has a" through containment.
   2. Implement "has a" through private inheritance as a last resort.
   3. Be critical of classes that contain more about seven members.

2. **Inheritance("is a") -**

   1. Implement "is a" through public inheritance.

      If the derived class isn't going to adher completely to the same interface contract defined by base class, inheritance is not the right implementation technique.

   2. Design and document for inheritance or prohibit it.

      If a class isn't designed to be inherited from, make its member non-virtual in C++, final in Java.

   3. Adher to Liskov Substitution Principle(LSP)

      Subclasses must be usable through the base interface without the need for the user to know the difference.

   4. Be sure to inherit only what you want to inherit.

   5. Don't "override" a non-overridable member function.

      Don't reuse names of non-overridable base-class routines in derived class.

   6. Move common interface, data and behaviour as high as possible in the inheritance tree.

   7. Be suspicious of classes that override a routine and do nothing inside the derived class.

   8. Avoid deep inheritance tree.

   9. Prefer polymorphism to extensive type checking.

   10. Make all data private not protected.

   Ex - Case statement that should be replaced.

   ``` c++
   switch ( shape.type ) {
      case Shape_Circle:
         shape.DrawCircle();
         break;
      case Shape_Square:
         shape.DrawSquare();
         break;
      ...
   }
   ```

   ** When to use Inheritence and when to use Containment?**

   - If multiple classes share common data but not behaviour, create a common object that those classes can contain.

   - If multiple classes share common behaviour but no data, derive them from a common base class that defines the common behaviour.

   - If multiple classes share common data and behaviour, inherit from a common base class that defines the common routines.

   - Inherit when you want the base class to control your interface, contain when you want to control your interface.

     

3. **Member Function and Data -**

   1. Keep the number of routines in a class as small as possible.

   2. Disallow implicitly generated member functions and operators you don't want.

   3. Minimize the number of different routines called by a class.

   4. Minimize the number of different routines called by a class.

   5. Minimize indirect routine calls to other classes.

      Law of Demeter - Object A can call any of its own routines. If object A instantiates an object B, it can call any object B's routines. But it should avoid calling routines on objects provided by object B.

   6. Minimize the extent to which a class collaborates with other classes.

      

4. Constructors

   1. Initialize all member data in all constructors, if possible.
   2. Enforce the singleton property by using a private constructor.
   3. Prefer deep copies to shallow copies untill proven.



## Reason to Create a Class

1. Model real world objects.
2. Model abstract object.
3. Reduce complexity.
4. Isolate complexity.
5. Hide implementation details.
6. Limit effect of change.
7. Hide global data.
8. Streamline parameter passing.
9. Make central point of control.
10. Faciliate reusable code.
11. Plan for a family of program.
12. Package related operations.
13. Accompalish a specific refactoring.



**Classes to avoid:**

- Avoid creating GOD classes.

- Eleminate irrelevant classes.

- Avoid classes named after verbs.

  

## Other's on Classes:

The single most important rule in object-oriented programming with C++ is this: public inheritance means "is a." Commit this rule to memory. 

​								— Scott Meyers

The one indisputable fact about multiple inheritance in C++ is that it opens up a Pandora's box of complexities that simply do not exist under single inheritance. 

​								— Scott Meyers

It ain't abstract if you have to look at the underlying implementation to understand what's going on.

​								— P. J. Plauger

The single most important factor that distinguishes a well-designed module from a poorly designed one is the degree to which the module hides its internal data and other implementation details from other modules. 

​								— Joshua Bloch



# High Quality Routine

Ex - Low quality routine

```c++
void HandleStuff( CORP_DATA & inputRec, int crntQtr, EMP_DATA empRec,
   double & estimRevenue, double ytdRevenue, int screenX, int screenY,
   COLOR_TYPE & newColor, COLOR_TYPE & prevColor, StatusType & status,
   int expenseType )
{
int i;
for ( i = 0; i < 100; i++ ) {
   inputRec.revenue[i] = 0;
   inputRec.expense[i] = corpExpense[ crntQtr ][ i ];
   }
UpdateCorpDatabase( empRec );
estimRevenue = ytdRevenue * 4.0 / (double) crntQtr;
newColor = prevColor;
status = SUCCESS;
if ( expenseType == 1 ) {
     for ( i = 0; i < 12; i++ )
           profit[i] = revenue[i] - expense.type1[i];
     }
else if ( expenseType == 2 ) {
          profit[i] = revenue[i] - expense.type2[i];
          }
else if ( expenseType == 3 )
          profit[i] = revenue[i] - expense.type3[i];
          }
```



## Valid Reasons to Create a Routine

1. Reduce complexity
2. Introduce an intermediate, understandable abstraction.
3. Avoid duplicate code.
4. Support subclassing.
5. Hide sequences.
6. Hide pointer operations
7. Improve portability.
8. Simplify complicated boolean tests.
9. Improve performance.



## Design at Routine Level

Cohesion - How operations in a routine are closely related.

Kinds of Cohesion to keep in mind:-

1. 