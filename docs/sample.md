# Sample
Here is a very simple test:

```java
package example1;

import org.testng.annotations.*;

public class SimpleTest {

    @BeforeClass
    public void setUp() {
        // code that will be invoked when this test is instantiated
    }

    @Test(groups = {"fast"})
    public void aFastTest() {
        System.out.println("Fast test");
    }

    @Test(groups = {"slow"})
    public void aSlowTest() {
        System.out.println("Slow test");
    }

}
```

Once you have compiled your test class into the build directory, you can invoke your test with the command line, an ant task (shown below) or an XML file:

```xml
<project default="test">

    <path id="cp">
        <pathelement location="lib/testng-testng-5.13.1.jar"/>
        <pathelement location="build"/>
    </path>

    <taskdef name="testng" classpathref="cp"
             classname="org.testng.TestNGAntTask"/>

    <target name="test">
        <testng classpathref="cp" groups="fast">
            <classfileset dir="build" includes="example1/*.class"/>
        </testng>
    </target>

</project>
```

Use ant to invoke it:

```shell
c:> ant
Buildfile: build.xml

test:
[testng] Fast test
[testng] ===============================================
[testng] Suite for Command line test
[testng] Total tests run: 1, Failures: 0, Skips: 0
[testng] ===============================================


BUILD SUCCESSFUL
Total time: 4 seconds
```

Then you can browse the result of your tests (on Windows):

```shell
c:> start test-output\index.html
```
