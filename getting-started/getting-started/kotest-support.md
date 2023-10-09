---
description: Make Kotest work with Konsist
---

# Kotest Support

Konsist can't obtain the current [kotest](https://kotest.io/) test's name, unlike JUnit. It's suggested to supply the test name using the `testName` parameter. Doing so will enable:

* Correct test names are displayed when the test is failing
* Test suppression (See [suppress-konsist-test.md](../../writing-tests/suppress-konsist-test.md "mention"))

It is recommended to utilize the name derived from the Kotest context as the value for the `testName` argument:

```kotlin
class UseCaseTest : FreeSpec({
    "useCase test" {
        Konsist
            .scopeFromProject()
            .classes()
            .assertTrue (testName = this.testCase.name.testName) {  }
    }
})
```

{% hint style="info" %}
This example is used [FreeSpec](https://kotest.io/docs/framework/testing-styles.html#free-spec) however Kotest provides [multiple testing styles](https://kotest.io/docs/framework/testing-styles.html).
{% endhint %}

To facilitate test name retrieval you can add this custom `koTestName` extension:

```kotlin
val TestScope.koTestName: String
    get() = this.testCase.name.testName
```

This extension enables more concise syntax to providing Kotest test name:

```kotlin
class UseCaseTest : FreeSpec({
    "useCase test" {
        Konsist
            .scopeFromProject()
            .classes()
            .assertTrue (testName = koTestNamee) {  }
    }
})
```

{% hint style="info" %}
In the future, this extension will be added to the Konsist.
{% endhint %}