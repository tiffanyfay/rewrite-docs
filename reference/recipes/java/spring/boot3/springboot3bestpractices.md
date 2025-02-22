# Spring Boot 3.x best practices

**org.openrewrite.java.spring.boot3.SpringBoot3BestPractices**

_Applies best practices to Spring Boot 3 applications._

### Tags

* spring
* boot

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-spring/blob/main/src/main/resources/META-INF/rewrite/spring-boot-32.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-spring/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-spring/5.3.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-spring
* version: 5.3.0

{% hint style="info" %}
This recipe is composed of more than one recipe. If you want to customize the set of recipes this is composed of, you can find and copy the GitHub source for the recipe from the link above.
{% endhint %}

## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-spring:5.3.0` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.7.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.spring.boot3.SpringBoot3BestPractices")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-spring:5.3.0")
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
        rewrite("org.openrewrite.recipe:rewrite-spring:5.3.0")
    }
    rewrite {
        activeRecipe("org.openrewrite.java.spring.boot3.SpringBoot3BestPractices")
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
            <recipe>org.openrewrite.java.spring.boot3.SpringBoot3BestPractices</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-spring</artifactId>
            <version>5.3.0</version>
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
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-spring:RELEASE -Drewrite.activeRecipes=org.openrewrite.java.spring.boot3.SpringBoot3BestPractices
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe SpringBoot3BestPractices
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Spring Boot 2.x best practices](../../../java/spring/boot2/springboot2bestpractices.md)
* [Migrate to Java 21](../../../java/migrate/upgradetojava21.md)
* [Migrate to Spring Boot 3.2](../../../java/spring/boot3/upgradespringboot_3_2.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.spring.boot3.SpringBoot3BestPractices
displayName: Spring Boot 3.x best practices
description: Applies best practices to Spring Boot 3 applications.
tags:
  - spring
  - boot
recipeList:
  - org.openrewrite.java.spring.boot2.SpringBoot2BestPractices
  - org.openrewrite.java.migrate.UpgradeToJava21
  - org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_2

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.spring.boot3.SpringBoot3BestPractices)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.

## Contributors
Tyler Van Gorder, [Knut Wannheden](mailto:knut@moderne.io), [Nick McKinney](mailto:mckinneynichoals@gmail.com), [Patrick](mailto:patway99@gmail.com), Chuka Obinabo, [Alex Boyko](mailto:aboyko@vmware.com), [Jonathan Schneider](mailto:jkschneider@gmail.com), [Sam Snyder](mailto:sam@moderne.io), Patrick Way, Kun Li, [Nick McKinney](mailto:mckinneynicholas@gmail.com), [traceyyoshima](mailto:tracey.yoshima@gmail.com), [Tim te Beek](mailto:tim.te.beek@jdriven.com), [Kyle Scully](mailto:scullykns@gmail.com), [Tim te Beek](mailto:tim@moderne.io), [Aaron Gershman](mailto:aegershman@gmail.com), [Jonathan Schnéider](mailto:jkschneider@gmail.com), [Satvika Eda](mailto:satvika164.reddy@gmail.com), [Shannon Pamperl](mailto:shanman190@gmail.com), [Kevin McCarpenter](mailto:kevin@moderne.io), [Kun Li](mailto:kun@moderne.io), [Tracey Yoshima](mailto:tracey.yoshima@gmail.com), [Greg Adams](mailto:gadams@gmail.com), [Yifeng Jin](mailto:yifeng.jyf@alibaba-inc.com), Adam Slaski, [Greg Adams](mailto:greg@moderne.io), Aaron Gershman, Fabian Krüger, [Johannes Jank](mailto:johannes.wengert@googlemail.com), [magicwerk](mailto:magicwerk@gmail.com), [Joan Viladrosa](mailto:joan@moderne.io), [Tim te Beek](mailto:timtebeek@gmail.com), nbruno, ranuradh, Sandeep Nagaraj, [BoykoAlex](mailto:aboyko@pivotal.io), [Simon Verhoeven](mailto:verhoeven.simon@gmail.com), [Sofia Britto Schwartz](mailto:sofia.b.schwartz@gmail.com), Aakarshit Uppal, John Burns, Josh Soref, [Michael Keppler](mailto:bananeweizen@gmx.de), [Scott Jungling](mailto:scott.jungling@gmail.com), Peter Puškár, [Mike Solomon](mailto:mikesol@hey.com)
