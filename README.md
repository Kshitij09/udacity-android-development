# udacity-android-development
Solutions to Udacity's Android course exercises

## Course - Developing Android Apps with Kotlin

### Lesson 3 - Navigation (Trivia App)

### Lesson 4 - Activity & Fragment Lifecycle (Dessert Pusher App)

### Lesson 5 - App Architecture - UI Layer (Guess-it App)

**Changes:** 

* At the time of completing these assignments, LiveData's `observe` method no-longer accept Fragment (`this`) as the `lifecyclerOwner` and we need to use `viewLifecycleOwner` property of Fragment instead.
* `binding.setLifecycleOwner(this)` &rarr; `binding.lifecycleOwner = viewLifecycleOwner ` (In Fragments)
* `ViewModelProviders.of(this)` &rarr; `ViewModelProvider(this)`

### Lesson 8 - Connect to the internet (Mars Real Estate App)

Build REST API client using retrofit2, coroutines and glide (for image loading) and a RecyclerView with DataBinding perks.

**Changes:**

* Using the latest retrofit version, targeting java sdk "1.8"

  ```gradle
  android {
  	...
      compileOptions {
          sourceCompatibility JavaVersion.VERSION_1_8
          targetCompatibility JavaVersion.VERSION_1_8
      }
   	kotlinOptions { jvmTarget = "1.8" }
  }
  ```
  
  Also, an optional change that might fix some multidex issues: in dependencies
  
  `implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$version_kotlin"` *to*
  
  `implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk8:$version_kotlin"`
  
* Fixed `java.io.IOException: Cleartext HTTP traffic to storage.googleapis.com not permitted`

  * create `network_security_config.xml` with following content

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <network-security-config>
        <base-config cleartextTrafficPermitted="false" />
        <domain-config cleartextTrafficPermitted="true">
            <domain includeSubdomains="true">mars.jpl.nasa.gov</domain>
        </domain-config>
    </network-security-config>
    ```

  * Specify the same in `AndroidManifest.xml`

    ```xml
    <application
    	...           
    	android:networkSecurityConfig="@xml/network_security_config"
    ```

### Lesson 9 - Behind the scenes

**Changes:**

* Updated all the dependencies to the latest version
  * Change `version_gradle=4.0.0` in `build.gradle` (Project-level)  to fix this [issue](https://github.com/udacity/andfun-kotlin-dev-bytes/issues/9)
  * `Payload(Result.SUCCESS)` &rarr; `Result.success()`