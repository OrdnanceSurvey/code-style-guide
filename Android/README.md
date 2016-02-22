#Ordnance Survey Android Code Style Guidelines

The aim of this document is to ensure a consistent style guide across our code base, to better promote readability and make it easier to spot potential problems within the code base. 
These guidelines were agreed by the team, and based off of the [Android Code Style Guidelines for Contributors](https://source.android.com/source/code-style.html)

##1. Gradle
All Android projects (including Java libraries developed for use with Android) are to be built using Gradle and structured as per the defaults for those project types. This is to ensure that all builds are prepared, tested and deployed with a consistent set of methods and plugins.
Where appropriate repeated build logic will be moved into Gradle plugins for use within OS projects.

Android Studio will create a Gradle structured project by default. 

For developers moving from and Maven or Ant based build there is a [Gradle - Getting Started Android](https://gradle.org/getting-started-android/) guide to help the transition:


##2. Consistent Code Base

There are a range of checks made against OS Android projects using the base Gradle Quality checks configured for usage with the Android Gradle Plugin.

These are:
- Checkstyle
- Findbugs
- PMD
- Android Lint
- Unit Testing
- Jacoco Unit Test Coverage
- AndroidTest
- AndroidTest Coverage

To aid the configuration and usage of these checks an [Android Checks](https://github.com/OrdnanceSurvey/gradle-plugin-android-checks) gradle plugin has been developed.

The information on how to implement and configure this plugin are contained in the plugin README.

All Android projects (including Java libraries developed for use with Android) will use this plugin to ensure consistency of checks across projects.

As part of the configuration of the plugin any rule-sets used should be drawn from the guidelines described here.

### Rules / Exceptions

- [Checkstyle Rules](https://github.com/OrdnanceSurvey/code-style-guide/tree/android/Android/checkstyle)
- [PMD Rules](https://github.com/OrdnanceSurvey/code-style-guide/tree/android/Android/pmd)

### Android Lint

The android-checks plugin will adhere to any lint configuration that is defined for the RELEASE build type in the build.gradle file.

Full documentation around how to configure lint can be found on the [Android Lint](http://developer.android.com/tools/debugging/improving-w-lint.html) page at Android Developer

Whilst the intention is to have zero lint exceptions there may be occasions where one is required.

For a project wide exception this should be made in the build.gradle file as follows:

      lintOptions {
            disable 'OldTargetApi', 'GradleDependency'
            ... other configuration ...
        }

Where an individual exception is needed it should be made at the smallest possible scope to adequately cover the exception.

In java code use the annotation format (to better match with Findbugs and Support Annotations):

     @SuppressLint("NewApi")

In xml use the namespace format on the element to exclude

    xmlns:tools="http://schemas.android.com/tools"
        tools:ignore="UnusedResources"

Exceptions to lint should be treated as rare cases as the majority of lint issues will be the result of poor code / resource usage that could be designed out.

### Intellij and Android Studio
For these two IDE's there are some shortcuts to help with fixing issues with checkstyle. The following two commands when applied to any .java and Android xml file will eliminate the majority of checkstyle issues:

Optimise Imports:

Mac - 

    ctrl + alt + O

Windows -

    Ctrl + Alt + O

Optimise Code:

Mac -
    
    alt + cmd + L

Windows -

    Ctrl + Alt + L
    
For more keyboard shortcuts for these IDE's choose Help | Default Keymap Reference from the main menu.
