# Migrate SLF4J to Log4j 2.x API.

**org.openrewrite.java.logging.log4j.Slf4jToLog4j**

_Transforms code written using SLF4J to use Log4j 2.x API._

### Tags

* slf4j
* logging
* log4j

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-logging-frameworks/blob/main/src/main/resources/META-INF/rewrite/log4j.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-logging-frameworks/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-logging-frameworks/2.4.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-logging-frameworks
* version: 2.4.1

{% hint style="info" %}
This recipe is composed of more than one recipe. If you want to customize the set of recipes this is composed of, you can find and copy the GitHub source for the recipe from the link above.
{% endhint %}

## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-logging-frameworks:2.4.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.7.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.logging.log4j.Slf4jToLog4j")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-logging-frameworks:2.4.1")
}
```
{% endcode %}
2. Run `gradle rewriteRun` to run the recipe.
{% endtab %}

{% tab title="Gradle init script" %}
1. Create a file named `init.gradle` in the root of your project.
{% code title="init.gradle" %}
```groovy
initscript {
    repositories {
        maven { url "https://plugins.gradle.org/m2" }
    }
    dependencies { classpath("org.openrewrite:plugin:6.7.0") }
}
rootProject {
    plugins.apply(org.openrewrite.gradle.RewritePlugin)
    dependencies {
        rewrite("org.openrewrite.recipe:rewrite-logging-frameworks:2.4.1")
    }
    rewrite {
        activeRecipe("org.openrewrite.java.logging.log4j.Slf4jToLog4j")
    }
    afterEvaluate {
        if (repositories.isEmpty()) {
            repositories {
                mavenCentral()
            }
        }
    }
}
```
{% endcode %}
2. Run `gradle --init-script init.gradle rewriteRun` to run the recipe.
{% endtab %}
{% tab title="Maven POM" %}
1. Add the following to your `pom.xml` file:
{% code title="pom.xml" %}
```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>5.20.0</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.java.logging.log4j.Slf4jToLog4j</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-logging-frameworks</artifactId>
            <version>2.4.1</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
2. Run `mvn rewrite:run` to run the recipe.
{% endtab %}

{% tab title="Maven Command Line" %}
{% code title="shell" %}
You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-logging-frameworks:RELEASE -Drewrite.activeRecipes=org.openrewrite.java.logging.log4j.Slf4jToLog4j
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe Slf4jToLog4j
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.LoggerFactory getLogger(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.LogManager`
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.MarkerFactory getMarker(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.MarkerManager`
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.MDC putCloseable(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.CloseableThreadContext`
* [Change method name](../../../java/changemethodname.md)
  * methodPattern: `org.apache.logging.log4j.CloseableThreadContext putCloseable(..)`
  * newMethodName: `put`
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.MDC clear(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.ThreadContext`
* [Change method name](../../../java/changemethodname.md)
  * methodPattern: `org.apache.logging.log4j.ThreadContext clear(..)`
  * newMethodName: `clearAll`
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.MDC put(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.ThreadContext`
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.MDC get(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.ThreadContext`
* [Change method target to static](../../../java/changemethodtargettostatic.md)
  * methodPattern: `org.slf4j.MDC remove(..)`
  * fullyQualifiedTargetTypeName: `org.apache.logging.log4j.ThreadContext`
* [Change method name](../../../java/changemethodname.md)
  * methodPattern: `org.slf4j.spi.LoggingEventBuilder addMarker(..)`
  * newMethodName: `withMarker`
* [Change method name](../../../java/changemethodname.md)
  * methodPattern: `org.slf4j.spi.LoggingEventBuilder setCause(..)`
  * newMethodName: `withThrowable`
* [Change type](../../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.slf4j.Logger`
  * newFullyQualifiedTypeName: `org.apache.logging.log4j.Logger`
* [Change type](../../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.slf4j.event.Level`
  * newFullyQualifiedTypeName: `org.apache.logging.log4j.Level`
* [Change type](../../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.slf4j.spi.LoggingEventBuilder`
  * newFullyQualifiedTypeName: `org.apache.logging.log4j.LogBuilder`
* [Change type](../../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.slf4j.Marker`
  * newFullyQualifiedTypeName: `org.apache.logging.log4j.Marker`
* [Change type](../../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.slf4j.MDC.MDCCloseable`
  * newFullyQualifiedTypeName: `org.apache.logging.log4j.CloseableThreadContext.Instance`
* [Change type](../../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.slf4j.MDC`
  * newFullyQualifiedTypeName: `org.apache.logging.log4j.CloseableThreadContext`
* [Change Gradle or Maven dependency](../../../java/dependencies/changedependency.md)
  * oldGroupId: `org.slf4j`
  * oldArtifactId: `slf4j-api`
  * newGroupId: `org.apache.logging.log4j`
  * newArtifactId: `log4j-api`
  * newVersion: `latest.release`
* [Replace any Lombok log annotations with target logging framework annotation](../../../java/logging/changelomboklogannotation.md)
  * loggingFramework: `Log4j2`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.logging.log4j.Slf4jToLog4j
displayName: Migrate SLF4J to Log4j 2.x API.
description: Transforms code written using SLF4J to use Log4j 2.x API.
tags:
  - slf4j
  - logging
  - log4j
recipeList:
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.LoggerFactory getLogger(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.LogManager
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.MarkerFactory getMarker(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.MarkerManager
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.MDC putCloseable(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.CloseableThreadContext
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: org.apache.logging.log4j.CloseableThreadContext putCloseable(..)
      newMethodName: put
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.MDC clear(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.ThreadContext
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: org.apache.logging.log4j.ThreadContext clear(..)
      newMethodName: clearAll
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.MDC put(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.ThreadContext
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.MDC get(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.ThreadContext
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: org.slf4j.MDC remove(..)
      fullyQualifiedTargetTypeName: org.apache.logging.log4j.ThreadContext
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: org.slf4j.spi.LoggingEventBuilder addMarker(..)
      newMethodName: withMarker
  - org.openrewrite.java.ChangeMethodName:
      methodPattern: org.slf4j.spi.LoggingEventBuilder setCause(..)
      newMethodName: withThrowable
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.slf4j.Logger
      newFullyQualifiedTypeName: org.apache.logging.log4j.Logger
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.slf4j.event.Level
      newFullyQualifiedTypeName: org.apache.logging.log4j.Level
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.slf4j.spi.LoggingEventBuilder
      newFullyQualifiedTypeName: org.apache.logging.log4j.LogBuilder
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.slf4j.Marker
      newFullyQualifiedTypeName: org.apache.logging.log4j.Marker
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.slf4j.MDC.MDCCloseable
      newFullyQualifiedTypeName: org.apache.logging.log4j.CloseableThreadContext.Instance
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.slf4j.MDC
      newFullyQualifiedTypeName: org.apache.logging.log4j.CloseableThreadContext
  - org.openrewrite.java.dependencies.ChangeDependency:
      oldGroupId: org.slf4j
      oldArtifactId: slf4j-api
      newGroupId: org.apache.logging.log4j
      newArtifactId: log4j-api
      newVersion: latest.release
  - org.openrewrite.java.logging.ChangeLombokLogAnnotation:
      loggingFramework: Log4j2

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.logging.log4j.Slf4jToLog4j)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.

## Contributors
[Tim te Beek](mailto:tim@moderne.io)
