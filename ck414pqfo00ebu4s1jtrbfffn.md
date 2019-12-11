## How to fix Android X error with firebase plugin in your flutter application

One of the current challenges as of the time I'm writing this article is using firebase in flutter application, using firebase in your flutter application at default return error. Firebase returns different errors base on the context of what you are doing, but the fix for any kind of error you might encounter is to enable AndroidX into your flutter project.  In this article, I will be showing step by step process on how to fix this issue.

# Steps to fix firebase plugin error

- 

** Enable multiDex in your defaultConfig build.gradle file.**

To enable multiDex, navigate to your android project folder. Inside your app folder, open your build.gradle file at the app level then add google support service at the defaultConfig section

```
multiDexEnabled true
```

overall default config should look like below

```
 defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.bloc_demo"
        minSdkVersion 16
        targetSdkVersion 28
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
        multiDexEnabled true
    }

```
In your targetSdkVersion in the defaultConfig object change the value to 28 and in your compileSdkVersion at the android level declaration change the value to 28.

Add google service to your gradle file if not present, you can do so by using the below snippet

```
apply plugin: 'com.google.gms.google-services'
```
But in case you have any issue, below is how my gradle file look like:

```
def localProperties = new Properties()
def localPropertiesFile = rootProject.file('local.properties')
if (localPropertiesFile.exists()) {
    localPropertiesFile.withReader('UTF-8') { reader ->
        localProperties.load(reader)
    }
}

def flutterRoot = localProperties.getProperty('flutter.sdk')
if (flutterRoot == null) {
    throw new GradleException("Flutter SDK not found. Define location with flutter.sdk in the local.properties file.")
}

def flutterVersionCode = localProperties.getProperty('flutter.versionCode')
if (flutterVersionCode == null) {
    flutterVersionCode = '1'
}

def flutterVersionName = localProperties.getProperty('flutter.versionName')
if (flutterVersionName == null) {
    flutterVersionName = '1.0'
}

apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply from: "$flutterRoot/packages/flutter_tools/gradle/flutter.gradle"
apply plugin: 'com.google.gms.google-services'

android {
    compileSdkVersion 28

    sourceSets {
        main.java.srcDirs += 'src/main/kotlin'
    }

    lintOptions {
        disable 'InvalidPackage'
    }

    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.bloc_demo"
        minSdkVersion 16
        targetSdkVersion 28
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
        multiDexEnabled true
    }

    buildTypes {
        release {
            // TODO: Add your own signing config for the release build.
            // Signing with the debug keys for now, so `flutter run --release` works.
            signingConfig signingConfigs.debug
        }
    }
}

flutter {
    source '../..'
}

dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
    implementation 'com.google.firebase:firebase-analytics:17.2.0'

}


```


- 
**Fixing and adding google service to build.gradle file at the project level**

At the dependencies section in the build.gradle file, add google service to it if not present.

```
 classpath 'com.google.gms:google-services:4.2.0'

```
Below is how my build.gradle file at the project level look like in case you have any issue with the file

```
buildscript {
    ext.kotlin_version = '1.2.71'
    repositories {
        google()
        jcenter()
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:3.2.1'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath 'com.google.gms:google-services:4.2.0'

    }
}

allprojects {
    repositories {
        google()
        jcenter()
    }
}

rootProject.buildDir = '../build'
subprojects {
    project.buildDir = "${rootProject.buildDir}/${project.name}"
}
subprojects {
    project.evaluationDependsOn(':app')
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

```


- 
**Enable AndroidX in your gradle.properties file **

To enable AndroidX at the root level, open gradle.properties file and paste below snippet

```
android.useAndroidX=true
android.enableJetifier=true

```


Below is how my gradle.properties file looks like in case you want to compare with yours

```
org.gradle.jvmargs=-Xmx1536M
android.useAndroidX=true
android.enableJetifier=true

```


# Conclusion
Wow! that's the end of the article if you get to this point, you would have definitely fix AndroidX error in your flutter application and your application is working well. If you have an issue or encounter any error, feel free to drop it in the comment box I will respond to it asap.