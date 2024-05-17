# gradle-aggregate-javadocs-plugin
================================

This is a fork of [nebula gradle-aggregate-javadocs-plugin](https://github.com/nebula-plugins/gradle-aggregate-javadocs-plugin).


In a multi-project setup containing one or many Java-based projects, Javadocs are only created for individual subprojects.
There are certain use cases that requires you merge Javadocs for all subprojects of your build. Creating a reusable library
that is partitioned into sub-functionality but shipped together is a typical example. This plugin adds a task to the root
project of the build allowing to aggregate Javadocs across all subprojects.

## Usage

### Applying the Plugin

To include, add the following to your build.gradle

```groovy
buildscript {
    repositories {
        maven { url = "https://ssl.lunadeer.cn:14454/repository/maven-releases/" }
    }
    dependencies {
        classpath 'cn.lunadeer:gradle-aggregate-javadocs-plugin:1.6'
    }
}

apply plugin: 'cn.lunadeer.aggregate-javadocs'
```

### **NEW+** Exclude specific subprojects

In subprojects that you want to exclude from the aggregation, add the following to the build.gradle

```groovy
project.ext.excludeFromJavadocAggregation = true
```

### Aggregating Javadocs

To aggregate Javadocs across all subprojects, execute the task `aggregateJavadocs` available to the root project. The task
declares a task dependencies on the task `javadoc` provided by the Java plugin. The resulting Javadoc report is located
in the directory `project.buildDir/docs/javadoc`.