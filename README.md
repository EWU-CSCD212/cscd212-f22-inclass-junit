# cscd212-f22-inclass-junit


[JUnit Website](https://junit.org/junit5/)

Run before each test
```java
@BeforeEach
void setUp() {
    // your code
}
```

Test
```java
@Test
@DisplayName("Name of test")
void example() {
    // your code
    // some assert
}
```

Nested used to organize tests
```java
@Nested
class example {
    @Test
    //...
}
```

Some Assert we use
```java
assertEquals(Expected, Actual, Fail-Message);
assertEquals(0, Double.compare(Expected, Actual), Fail-Message); // When using doubles
assertTrue(Actual, Fail-Message);
assertFalse(Actual, Fail-Message);
assertNull(Actual, Fail-Message);
Throwable throwable = assertThrows(ExpectedException.class, () -> {
    // Actual, code that will throw exception
}, Fail-Message);
throwable.getMessage() // is the message with the exception
```

## Use tool to make tests for you

```java
@ParameterizedTest
@MethodSource("getTestsValues")
@DisplayName("Name of set of tests")
void testing(Arg...) {
    // your code
    // some assert
}
static Stream<Arguments> getTestsValues() {
    // your code gen arguments for testing
}
```

Ex.
```java
@ParameterizedTest
@MethodSource("getTestsValues")
@DisplayName("Example Add")
void testingAdd(final double num1, final double num2, final double expectedValue) {
    double actual = new Cal(num1, num2).add();
    assertEquals(0, Double.compare(expectedValue, actual), num1 + " + " + num2 + " not equal to " + actual);
}
static Stream<Arguments> getTestsValues() {
    double[] num1s = new double[10];
    double[] num2s = new double[10];
    double[] values = new double[10];
    Random random = new Random();
    for (int i = 0; i < 10; i++) {
        num1s[i] = random.nextDouble();
        num2s[i] = random.nextDouble();
        values[i] = num1s[i] + num2s[i];
    }
    Arguments[] arguments = new Arguments[10];
    for (int i = 0; i < 10; i++) {
        arguments[i] = Arguments.of(num1s[i], num2s[i], values[i]);
    }
    return Stream.of(arguments);
}
```