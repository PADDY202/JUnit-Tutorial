# JUnit-Tutorial
Test-Driven Development (TDD)
Comp47480: JUnit Tutorial

This practical involves an introduction to Test-Driven Development (TDD). We'll be using JUnit 4.x with Eclipse. This tutorial Using JUnit With Eclipse provides useful advice on setting up JUnit in Eclipse and JUnit syntax.

Test-driven development is a method of developing software, not merely a method of testing. The technique involves the following three steps being repeatedly applied:
Step 1: Write a test case and try to run it. It probably won't even compile, so write just enough code to make it compile. Now run it. It will of course fail, so you'll get a red bar.

Step 2: Now you implement only the code necessary to make the test pass, nothing more. This code can be as quick-and-dirty as you like, once it makes the testcases pass. You'll know it's right when you run your testcases and you see the green bar.

Step 3: Now you tidy up your code by refactoring. You don't change what the code does, but you make it easier to understand and tighten the implementation wherever necessary. Avoid commenting the code. If you feel it needs a comment, refactor it so the comment becomes unnecessary. Run your testcases at any stage to confirm that behaviour hasn't changed. Do this again when you're finished refactoring to make sure that you haven't accidentally introduced any bugs.

Remember the mantra! red green refactor If a demonstrator asks you, you should immediately know what state you are in.

TDD is often formulated as three simple rules: 
1. You are not allowed to write any production code unless it is to make a failing unit test pass. 
2. You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures. 
3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

Preliminaries

Ensure that you have Eclipse installed along with the JUnit plugin. Any JUnit 4.x will work fine -- we're just using the very basics of what JUnit provides. Also install the EclEmma coverage plug-in. Create a new workspace project by clicking File -> New -> Java Project and click Next. Type in a project name -- for example, ProjectWithJUnit. Click Finish. The new project will be generated in your IDE.

Part 1: A Simple Example

Using TDD, develop a class called Weather that has a single public method called isFreezing that returns true if the temperature is <= 0.0, and false otherwise. Its constructor takes the current temperature as an argument. This class is trivial to implement of course, but apply TDD carefully and precisely to make sure you understand the process.

The first thing you do is write a testcase that exercises the Weather class. To create such a testcase, right-click on the ProjectWithJUnit title, select New -> JUnitTestCase. (This may also prompt you to add junit.jar to the project path).

Choose a name for your testcase -- for example, TestWeather.	You can leave the "Class under test:" box empty as the class you're to test doesn't exist yet. Click on Finish.

A possible first testcase for the TestWeather class is as follows:

  import org.junit.*;

  public class TestWeather {
    @Test  // this annotation tells JUnit that this is a test case
    public void testIfFreezingAtZeroDegrees(){
      Weather w = new Weather(0.0);
      assertTrue("temp was zero, but weather not freezing", w.isFreezing());
    }
  }
Study this code and make sure you understand it.

In keeping with the TDD approach, we now run our test to confirm that it fails. Highlight TestWeather.java in Package Explorer. Now click Run -> Run as -> JUnit Test . In the left window, instead of Package Explorer, you will see the JUnit window, which shows a red bar, the failed tests, and details of those failures.

Now implement just enough of the Weather class to make this testcase pass. You will probably be inclined to add too much implementation, breaking Rule 3 above. All that is required to make this testcase pass is:

  public class Weather {
    public boolean isFreezing() {
      return true;
    }
  }
Re-run the test and it should pass. Experiment with this, e.g., return false and see what happen when the test is run.
Continue applying the TDD process to this example, until you have a complete implementation of the Weather class.

Reflect on what's been achieved. The implementation is very simple, so what has the use of TDD given us?

Developing testcases first made us define the problem clearly.
Testcases makes it clear when we were finished.
When we change our code to add a new requirement, we can rerun the testcases to make sure that existing functionality hasn't been affected. This gives immense freedom in refactoring.
We needn't document for a maintenance programmer what the required behaviour of isFreezing is -- the testcase does this and is an executable test to boot.
Part 2: A More Challenging Example

A class Triangle has a constructor that takes 3 integer arguments representing the lengths of the side of the triangle. The data may be invalid (e.g. 8,2,3) -- the constructor doesn't check this. The Triangle class has a single method called typeOf that returns a string (use an enum if you prefer) representing the type of the triangle as follows:
equilateral: all sides same length 
isosceles: two sides same length 
scalene: all sides unequal length 
invalid: not a valid triangle 
Do NOT start thinking about how to implement the typeOf method, nor think about what sequence of testcases to develop. Apply TDD rigorously, testcase by testcase. The refactoring phase will be important here to keep the code elegant and clean.

If you're doing this with a partner, you might take it in turns to develop a testcase. One develops the testcase and implements the code to make it pass, while the other watches the process and makes sure that TDD is being applied correctly.

Part 3: Code Coverage

Use the EclEmma tool to determine the level of code coverage achieved by your testcases. If it's less than 100%, you definitely took shortcuts in applying TDD. Work out what went wrong.

If you achieved 100% coverage, you may have used TDD correctly, but it is no guarantee! To illustrate this, see if you can remove a testcase and still have 100% coverage. If you can do this, it means that a bug could be introduced into the typeOf method without the test cases reporting any problem, even though coverage is at 100%. Thus regression could occur, even though all testcases are passing. So you see that code coverage is not sufficient to prevent bugs.

Another way to assess your testcases, apart from coverage, is to use mutation testing. Make a small change (a mutation) to the typeOf method and run the testcases. One or more should fail. If they don't, there is a feature of the typeOf method that they are not testing. If they pass, undo the change you made and try another one.

Submission

The artefact for this practical is your solution to Part 2. Part 1 is a warm-up exercise, and Part 3 comprises exercises you can write about in your lab journal. Jacek will give you details of where to submit your solution to Part 2.

As usual, submit also a rough journal entry. It can just be a set of bullet points about what you did and some reflections. You'll submit this as a polished report at the end of the semester. Ask Jacek in the lab if you have any questions about this.

