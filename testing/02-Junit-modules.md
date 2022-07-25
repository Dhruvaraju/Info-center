## JUnit Module
- **JUnit Platform:** Used for launching testing frameworks on jvm. Allows tests to be run from a Console Launcher or build tools such as maven or gradle.
- **JUnit Jupiter:** Programming module for writing tests and extensions to JUnit.
- **JUnit Vintage:** Provides test engine for older versions of JUnit.

## JUnit Annotations
- **@Test:** marks a method as test.
- **@ParameterizedTest:** Marks test as a parameterized test.
- **@RepeatedTest:** Repeats test N times.
- **@TestFactory:** Test Factory for dynamic tests.
- **@TestInstance:** Used to configure test instance lifecycle.
- **@TestTemplate:** creates a test template to be used by multiple tests.
- **@DisplayName:** Human friendly name for test.
- **@BeforeEach:** Method to run before each Testcase.
- **@AfterEach:** Method to run after each testcase.
- **@BeforeAll:** Static method to run before all test cases in current class.
- **@AfterAll:** Static method to run after all test cases in current class.
- **@Nested:** Creates a nested test class.
- **@Tag:** Declares tags for filtering testing.
- **@Disabled:** Disables a test or test class.
- **@ExtendedWith:** Used to register extensions.

## JUnit Lifecycle:
1) @BeforeAll will run before everything.
2) @BeforeEach will run before executing every test.
3) @Test will run a test.
4) @AfterEach will run after the test execution.
5) @AfterAll will run after all the test are executed and last @AfterEach is run.