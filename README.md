
### AOP: Combining Pointcuts - Overview

**Problem**
+ How to apply multiple pointcut expressions to single advice?
+ Execute an advice only if certain conditions are met
+ For example
  + All methods in a package EXCEPT getter/setter methods





**Combining Pointcut Expressions**
+ Combine pointcut expressions using logic operations
  + AND(&&)
  + OR(||)
  + NOT(!)

+ Works like an "if" statement
+ Execution happens only if it evaluates to true

```JAVA
@Before("expressionOne() && expressionTwo()")
@Before("expressionOne() || expressionTwo()")
@Before("expressionOnw() && !expressionTwo()")
```

**Example**
+ All methods in package EXCEPT getter/setter methods

**Development Process**
1. Create a pointcut declarations
2. Combine pointcut declarations
3. Apply pointcut declaration to advice(s)


_Step 1:Create Pointcut Declaration_
```JAVA
@Pointcut("execution(* com.tilmeez.appdemo.*.*(..))")
private void forDaoPackage() {}

// create pointcut for getter methods
@Pointcut("execution(* com.tilmeez.aopdemo.dao.*.get*(..))")
private void getter() {}

// create pointcut for setter methods
@Pointcut("execution(* com.tilmeez.appdemo.dao.*.set*(..))")
private void setter() {}
```


_Step 2:Combine Pointcut Declarations_
```JAVA
@Pointcut("execution(* com.tilmeez.appdemo.*.*(..))")
private void forDaoPackage() {}

// create pointcut for getter methods
@Pointcut("execution(* com.tilmeez.aopdemo.dao.*.get*(..))")
private void getter() {}

// create pointcut for setter methods
@Pointcut("execution(* com.tilmeez.appdemo.dao.*.set*(..))")
private void setter() {}

// combine pointcut: including package ...
@Pointcut("forDaoPackage() && !(getter() || setter())")
private void forDaoPackageNotGetterSetter() {}
```


_Step 3:Apply Pointcut Declaration to Advice(s)_

```JAVA
...
// cobkine pointcut: including package ... exclude getter/setter
@Pointcut("forDaoPackage() && !(getter() || setter())")
private void forDaoPackageNotGetterSetter() {}

@Before("forDaoPackageNotGetterSetter()")
public void beforeAddAccountAdvice() {
 ... 
}
```

