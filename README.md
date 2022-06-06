# Black or White Box Testing

## Learning Goals

- Explain black/white box testing

## Black/White Box Testing

As the size and complexity of the software systems you build increases, it's
important to scale the type of testing that is being done with the system with
its complexity.

Unit testing, which we studied in the previous section, is technical testing by
definition in that it concerns itself with the implementation details of the
functionality it's testing. This is very useful and plays a crucial role in
building reliable and maintainable systems. There are two important limitations
with this type of testing, however:

1. Because it's "technical testing", the range of people who can write these
   tests is restricted to people familiar with the implementation details of the
   components being tested. This means we might test that we built the component
   properly, but we are at risk of not testing that we built the right
   component.
2. Unit testing is focused on the workings of a single component. As the system
   grows, these single components interact with each other and the way they
   integrate with each other can be a great source of bugs.

Unit testing is the principle example of "white box" testing, where we care
about the underlying implementation details of what we're testing.

Black box testing, on the other hand, does not care about the implementation
details and focuses on testing functionality based on the defined interface of
that functionality and its intended use. Examples of black box testing include:

- Functional testing: testing specific functional aspects of a system,
  regardless of how many underlying components are involved in implementing that
  functionality.
- Non-functional testing: testing on "non-functional" aspects of the system,
  such as performance and security testing

Non-functional testing, such as performance and security testing, is out of
scope for this section, so let's focus on functional testing.

It may seem like there would be a lot of overlap between "functional testing"
and "unit testing", but the difference between the two is profound:

- Unit testing focuses on making sure the code works as the developer intended
  it to work
- Functional testing focuses on making sure the software works as the users need
  it to work

In other words, one focuses on "building the thing right" while the other
focuses on "building the right thing".

This is a profound distinction because it does not matter if your code runs
perfectly every time if it does not actually solve the problems that its users
need solved.

Let's consider a simplified version of a real-life example. Your team has been
asked to build a "bill splitter" calculator:

- There will be a number of participants
- There will be a total for the bill
- You've been asked to write the method does the division
- You've been told you will always be dealing with integers for all parameters
  and for the return value
- You have not been given the "bill split" context, so you don't know how this
  "divide" method will be used

Here is some sample code you might have written:

```java
    public static int divide(int amountToSplit, int numPeople) {
        return amountToSplit / numPeople;
    }
```

Here is the unit testing code you might have written as well:

```java
    @Test
    void divideEven() {
        int split = SplitCalculator.divide(100, 4);
        assertEquals(25, split);
    }

    @Test
    void divideOdd() {
        int split = SplitCalculator.divide(100, 3);
        assertEquals(33, split);
    }
```

You were careful to test both cases where the result of the division is whole
and where the results is not whole. In doing so, you assumed the default Java
behavior of rounding _down_ when diving two integer numbers and getting a
decimal number back is the proper behavior.

In other words, your unit tests properly validate that the code works in the way
that you, the developer, intended it to work.

It's not until the business gets the entire "split calculator" app that they
realize that decimal numbers are being rounded down and that their customers in
their restaurants consistently come up short when trying to pay their bill based
on what the calculator tells them.

Someone should have done some functional testing on this application to make
sure that the logic to split the bill actually did what the restaurants needed
it to do.
