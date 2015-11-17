#Ordnance Survey Android Code Style Guidelines

The aim of this document is to ensure a consistent style guide across our code base, to better promote readability and make it easier to spot potential problems within the code base. 
These guidelines were agreed by the team, and based off of the [Android Code Style Guidelines for Contributors](https://source.android.com/source/code-style.html)

##1. Gradle
All Android projects (and accompanying OS produced Java libraries) are to be built using Gradle and structured as per the defaults for those project types. This is to ensure that all builds are prepared, tested and deployed with a consistent set of methods and plugins.
Where appropriate repeated build logic will be moved into Gradle plugins for use within OS projects.

Android Studio will create a Gradle structured project by default. 

For developers moving from and Maven or Ant based build the following documentation from Gradle will help the transition:

[Gradle - Getting Started Android](https://gradle.org/getting-started-android/)

##2. Consistent Code Base
All Android projects (and accompanying OS produced Java libraries) will use the checkstyle plugin in Gradle to ensure consistency across our code base.

There are two checkstyle rules files that are to be used in Android. These are located in the checkstyle folder in this repository.

[Checkstyle Rules](https://github.com/OrdnanceSurvey/mobile-code-style-guide/tree/android/Android/checkstyle)

Android does not support using the default checkstyle configuration so a custom Android set up is required.

In the application build.gradle file apply the checkstyle plugin:

    apply plugin: 'checkstyle'
    
Add the following custom task to the build.gradle file:
````
task checkstyle(type: Checkstyle) {
    group = "Reporting"

    description = "Generate Checkstyle reports"

    configFile new File("${project.rootDir}/config/checkstyle/checkstyle.xml")
    configProperties.checkstyleConfigDir = new File("${project.rootDir}/config", 'checkstyle')
    source 'src'
    include '**/*.java'
    exclude '**/gen/**'
    // empty classpath
    classpath = files()
    //Do not fail build
    ignoreFailures = true
}
````

The task assumes that the rules xml files will be located in a specific location:

    projectRoot/config/checkstyle/

Once the gradle sync is completed the checkstyle task can be run using the following gradle command:

    ./gradlew checkstyle

### Intellij and Android Studio
For these two IDE's there are some shortcuts to help with fixing issues with checkstyle. The following two commands when applied to any .java and Android xml file will eliminate the majority of checkstyle issues:

Optimise Imports:

    ctrl + alt + o

Optimise Code:

    alt + cmd + l







