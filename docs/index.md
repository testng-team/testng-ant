# TestNG Ant Task

You define the TestNG ant task as follows:

``` xml
<taskdef resource="testngtasks" classpath="testng.jar"/>
```

This task runs TestNG tests and is always run in a forked JVM. It accepts the following attributes:

| Attribute                         | Description                                                                                                                                                                                                                                                                                                                              | Required                                                |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `classfilesetref`                 | A reference to a [ResourceCollection](https://ant.apache.org/manual/Types/resources.html#collection) containing the test classes to be run. Only File based [ResourceCollections](https://ant.apache.org/manual/Types/resources.html#collection) are supported (ie. [FileSet](https://ant.apache.org/manual/Types/fileset.html)).        |                                                         |
| `classpath`                       | A PATH-like structure for the tests to be run.                                                                                                                                                                                                                                                                                           |                                                         |
| `classpathref`                    | A reference to a PATH-like structure for the tests to be run.                                                                                                                                                                                                                                                                            |                                                         |
| `configFailurePolicy`             | Whether TestNG should continue to execute the remaining tests in the suite or skip them if an `@Before*` method fails.                                                                                                                                                                                                                   | No. Defaults to `skip`                                  |
| `dataProviderThreadCount`         | The number of threads to use for data providers for this run. Ignored unless the parallel mode is also specified.                                                                                                                                                                                                                        | 1                                                       |
| `delegateCommandSystemProperties` | Pass the command line properties as system properties.                                                                                                                                                                                                                                                                                   | No. Defaults to `false`                                 |
| `dumpCommand`                     | Print the TestNG launcher command.                                                                                                                                                                                                                                                                                                       | No. Defaults to `false`                                 |
| `failureProperty`                 | The name of a property to set in the event of a failure. It is used only if the `haltonfailure` is not set.                                                                                                                                                                                                                              | No.                                                     |
| `haltonfailure`                   | Stop the build process if a failure has occurred during the test run.                                                                                                                                                                                                                                                                    | No. Defaults to `false`                                 |
| `haltonskipped`                   | Stop the build process if there is at least on skipped test.                                                                                                                                                                                                                                                                             | No. Defaults to `false`                                 |
| `groups`                          | The list of groups to run, separated by spaces or commas.                                                                                                                                                                                                                                                                                |                                                         |
| `excludedgroups`                  | The list of groups to exclude, separated by spaces or commas                                                                                                                                                                                                                                                                             |                                                         |
| `jvm`                             | The JVM to use, which will be run by `Runtime.exec()`                                                                                                                                                                                                                                                                                    | java                                                    |
| `listeners`                       |                                                                                                                                                                                                                                                                                                                                          | No.                                                     |
| `methods`                         | A comma separated list of fully qualified class name and method. For e.g., `com.example.Foo.f1,com.example.Bar.f2`.                                                                                                                                                                                                                      | No.                                                     |
| `mode`                            | Either "testng", "junit" or "mixed". Whether TestNG should run only TestNG tests, JUnit tests or both.                                                                                                                                                                                                                                   | No. Defaults to `testng`.                               |
| `outputdir`                       | Directory for reports output.                                                                                                                                                                                                                                                                                                            | No. Defaults to `test-output`.                          |
| `skippedProperty`                 | The name of a property to set in the event of a skipped test. It is used only if the haltonskipped is not set.                                                                                                                                                                                                                           | No.                                                     |
| `suiteRunnerClass`                | A fully qualified name of a TestNG starter.                                                                                                                                                                                                                                                                                              | No. Defaults to `org.testng.TestNG`                     |
| `suiteThreadPoolSize`             | The size of a thread pool to run suites.                                                                                                                                                                                                                                                                                                 | No. Defaults to 1.                                      |
| `parallel`                        | The parallel mode to use for running the tests - either methods or tests                                                                                                                                                                                                                                                                 | No - if not present, parallel mode will not be selected |
| `suitename`                       | Sets the default name of the test suite, if one is not specified in a suite xml file or in the source code                                                                                                                                                                                                                               | No. Defaults to "Ant suite"                             |
| `testJar`                         | Path to a jar containing tests and a suite definition.                                                                                                                                                                                                                                                                                   |                                                         |
| `testname`                        | Sets the default name of the test, if one is not specified in a suite xml file or in the source code                                                                                                                                                                                                                                     | No. defaults to "Ant test"                              |
| `testnames`                       | A comma separated list of test names, as defined in the \<test\> tag. Only these tests will be run.                                                                                                                                                                                                                                      | No. defaults to "Ant test"                              |
| `threadCount`                     | The number of threads to use for this run. Ignored unless the parallel mode is also specified.                                                                                                                                                                                                                                           | 1                                                       |
| `timeOut`                         | The maximum time out in milliseconds that all the tests should run under.                                                                                                                                                                                                                                                                |                                                         |
| `useDefaultListeners`             | Whether the default listeners and reporters should be used.                                                                                                                                                                                                                                                                              | Defaults to true.                                       |
| `workingDir`                      | The directory where the ant task should change to before running TestNG.                                                                                                                                                                                                                                                                 |                                                         |
| `xmlfilesetref`                   | A reference to a [ResourceCollection](https://ant.apache.org/manual/Types/resources.html#collection) containing the suite definitions to be run. Only File based [ResourceCollections](https://ant.apache.org/manual/Types/resources.html#collection) are supported (i.e., [FileSet](https://ant.apache.org/manual/Types/fileset.html)). |                                                         |
| `xmlPathInJar`                    | The path of the XML file inside the jar file, only applicable if testJar was specified                                                                                                                                                                                                                                                   | testng.xml                                              |

> [!TIP]
> One of attributes `classpath`, `classpathref` or nested `<classpath>` must be used for providing the tests classpath.

> [!TIP]
> One of the attributes `xmlfilesetref`, `classfilesetref` or nested `<xmlfileset>`, respectively `<classfileset>` must be used for providing the tests.

## TestNG modes

The TestNG mode gets applied when tests are passed to TestNG using classfilesetref, methods or nested \<classfileset\> and tells TestNG what kind of tests it should look for and run:

- `testng`: find and run TestNG tests.
- `junit`: find and run JUnit tests.
- `mixed`: run both TestNG and JUnit tests.

> [!NOTE]
> `junit` and `mixed` modes require the JUnit jar file on the classpath.

## Nested Elements

### classpath

The `<testng>` task supports a nested \<classpath\> element that represents a PATH-like structure.

### bootclasspath

The location of bootstrap class files can be specified using this PATH-like structure - will be ignored if fork is not set.

### xmlfileset

The suite definitions (`testng.xml`) can be passed to the task with a FileSet structure.

### classfileset

TestNG can also run directly on classes, also supplied with a FileSet structure.

### jvmarg

Additional parameters may be passed to the new VM via nested \<jvmarg\> elements. For example:

``` xml
<testng>
    <jvmarg value="-Djava.compiler=NONE" />
    <!-- ... -->
</testng>
```

### sysproperty

Use nested `<sysproperty>` elements to specify system properties required by the class. These properties will be made available to the virtual machine during the execution of the test. The attributes for this element are the same as for environment variables:

``` xml
<testng>
    <sysproperty key="basedir" value="${basedir}"/>
    <!-- ... -->
</testng>
```

will run the test and make the basedir property available to the test.

### propertyset

You may also use a nested \<propertyset\> element to specify a set of system properties that are defined outside of the TestNG ant task. This allows for more flexible definitions of system properties, for instance selecting all properties with a specific prefix or matching a regex. See the [PropertySet](https://ant.apache.org/manual/Types/propertyset.html) page in the [Ant manual](https://ant.apache.org/manual/) for full details. Here’s a simple example:

``` xml
<project name="Hello World Project">
    <property name="myprop1" value="value 1"/>
    <property name="myprop2" value="value 2"/>

    <propertyset id="propset1">
        <propertyref name="myprop1"/>
        <propertyref name="myprop2"/>
    </propertyset>

    <testng outputdir="${testng.report.dir}" classpathref="run.cp">
        <xmlfileset dir="${test15.dir}" includes="testng-single3.xml"/>
        <propertyset refid="propset1"/>
    </testng>
</project>
```

In this case, the system properties named "myprop1" and "myprop2" are passed along to the TestNG process.

### reporter

An inner `<reporter>` element is an alternative way to inject a custom report listener allowing the user to set custom properties in order to fine-tune the behavior of the reporter at run-time. The element has one classname attribute which is mandatory, indicating the class of the custom listener. In order to set the properties of the reporter, the `<reporter>` element can contain several nested \<property\> elements which will provide the name and value attributes as seen below:

``` xml
<testng>
    <!--... -->
    <reporter classname="com.test.MyReporter">
        <property name="methodFilter" value="*insert*"/>
        <property name="enableFiltering" value="true"/>
    </reporter>
    <!--... -->
</testng>
```

``` java
public class MyReporter {

  public String getMethodFilter() { /* code */ }
  public void setMethodFilter(String methodFilter) { /* code */ }
  public boolean isEnableFiltering() { /* code */ }
  public void setEnableFiltering(boolean enableFiltering) { /* code */ }
  // code
}
```

You have to consider though that for the moment only a limited set of property types are supported:

- `String`
- `int`
- `boolean`
- `byte`
- `char`
- `double`
- `float`
- `long`
- `short`

### env

It is possible to specify environment variables to pass to the TestNG forked virtual machine via nested `<env>` elements. For a description of the `<env>` element’s attributes, see the description in the [exec](https://ant.apache.org/manual/CoreTasks/exec.html) task.

## Examples

**Suite xml**

``` xml
<testng classpathref="run.cp"  outputDir="${testng.report.dir}"  sourcedir="${test.src.dir}"  haltOnfailure="true">
   <xmlfileset dir="${test14.dir}" includes="testng.xml"/>
</testng>
```

**Class FileSet**

``` xml
<testng classpathref="run.cp" outputDir="${testng.report.dir}" haltOnFailure="true" verbose="2">
    <classfileset dir="${test.build.dir}" includes="**/*.class" />
</testng>
```
