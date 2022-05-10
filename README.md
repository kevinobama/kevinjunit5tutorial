Kevin gates JUnit5 tutorial

1.1. What is JUnit 5?
Unlike previous versions of JUnit, JUnit 5 is composed of several different modules from three
different sub-projects.
JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage
The JUnit Platform serves as a foundation for launching testing frameworks on the JVM. It also
defines the TestEngine API for developing a testing framework that runs on the platform.
Furthermore, the platform provides a Console Launcher to launch the platform from the command
line and the JUnit Platform Suite Engine for running a custom test suite using one or more test
engines on the platform. First-class support for the JUnit Platform also exists in popular IDEs (see
IntelliJ IDEA, Eclipse, NetBeans, and Visual Studio Code) and build tools (see Gradle, Maven, and
5Ant).
JUnit Jupiter is the combination of the new programming model and extension model for writing
tests and extensions in JUnit 5. The Jupiter sub-project provides a TestEngine for running Jupiter
based tests on the platform.
JUnit Vintage provides a TestEngine for running JUnit 3 and JUnit 4 based tests on the platform. It
requires JUnit 4.12 or later to be present on the class path or module path.
1.2. Supported Java Versions
JUnit 5 requires Java 8 (or higher) at runtime. However, you can still test code that has been
compiled with previous versions of the JDK.


JUnit 5 vs JUnit 4
1. Different Annotations
   Most of the annotations in both versions are the same, but a few differ. Here is a quick comparison.

Feature
JUnit 4
Junit 5
Declare a test method
@Test
@Test
Execute before all test methods in the current class
@BeforeClass
@BeforeAll
Execute after all test methods in the current class
@AfterClass
@AfterAll
Execute before each test method
@Before
@BeforeEach
Execute after each test method
@After
@AfterEach
Disable a test method/class
@Ignore
@Disabled
Test factory for dynamic tests
NA
@TestFactory
Nested tests
NA
@Nested
Tagging and filtering
@Category
@Tag
Register custom extensions
NA
@ExtendWith
2. More differences between JUnit 5 and JUnit 4
   2.1. Architecture
   JUnit 4 has everything bundled into a single jar file.

JUnit 5 is composed of 3 sub-projects i.e. JUnit Platform, JUnit Jupiter and JUnit Vintage.

JUnit Platform: It defines the TestEngine API for developing new testing frameworks that run on the platform.
JUnit Jupiter: It has all new JUnit annotations and TestEngine implementation to run tests written with these annotations.
JUnit Vintage: To support running JUnit 3 and JUnit 4 written tests on the JUnit 5 platform.
2.2. Required JDK Version
Junit 4 requires Java 5 or higher.

Junit 5 requires Java 8 or higher.

2.3. Assertions
In Junit 4, org.junit.Assert has all assert methods to validate expected and resulting outcomes.
They accept extra parameters for error messages as the FIRST argument in the method signature. e.g.

public static void assertEquals(long expected, long actual)
public static void assertEquals(String message, long expected, long actual)
In JUnit 5, org.junit.jupiter.Assertions contain most of assert() methods including additional assertThrows() and assertAll() methods.
JUnit 5 assertions methods also have overloaded methods to support parsing error messages to be printed in case test fails e.g.

public static void assertEquals(long expected, long actual)
public static void assertEquals(long expected, long actual, String message)
public static void assertEquals(long expected, long actual, Supplier messageSupplier)
2.4. Assumptions
In Junit 4, org.junit.Assume contains methods for stating assumptions about the conditions in which a test is meaningful. It has the following five methods:

assumeFalse()
assumeNoException()
assumeNotNull()
assumeThat()
assumeTrue()
In Junit 5, org.junit.jupiter.api.Assumptions contain methods for stating assumptions about the conditions in which a test is meaningful. It has the following three methods:

assumeFalse()
assumingThat​()
assumeTrue()
2.5. Tagging and Filtering
In Junit 4, @category annotation is used.

In Junit 5, @tag annotation is used.

2.6. Test Suites
In Junit 4, @RunWith and @Suite annotation. e.g.

import org.junit.runner.RunWith;
import org.junit.runners.Suite;

@RunWith(Suite.class)
@Suite.SuiteClasses({
ExceptionTest.class,
TimeoutTest.class
})
public class JUnit4Example
{
}
In Junit 5, @Suite, @SelectPackages and @SelectClasses e.g.

import org.junit.platform.runner.JUnitPlatform;
import org.junit.platform.suite.api.SelectPackages;
import org.junit.runner.RunWith;

@Suite
@SelectPackages("com.howtodoinjava.junit5.examples")
public class JUnit5Example
{
}
2.7. Non-public Test Methods are Allowed
JUnit 5 test classes and test methods are not required to be public. We can now make them package protected.
JUnit internally uses reflection to find test classes and test methods. Reflection can discover them even if they have limited visibility so there is no need for them to be public.
JUnit test classes also can have non-public constructors. They can even have arguments. It means having a public no-args constructor is not mandatory in JUnit 5.
class AppTest {

    private AppTest(TestInfo testInfo) {
        System.out.println("Working on test " + testInfo.getDisplayName());
    }

@Test
void test(){
assertTrue(true);
}

}
2.8. 3rd Party Integration
In Junit 4, there is no integration support for 3rd party plugins and IDEs. They have to rely on reflection.

JUnit 5 has a dedicated sub-project for this purpose i.e. JUnit Platform. It defines the TestEngine API for developing a testing framework that runs on the platform.