# udacity-android-development
Solutions to Udacity - Developing Android Apps with Kotlin

1. Lesson 3 - Navigation (Trivia App)

2. Lesson 4 - Activity & Fragment Lifecycle (Dessert Pusher App)

3. Lesson 5 - App Architecture - UI Layer (Guess-it App)

   **Changes:** 

   * At the time of completing these assignments, LiveData's `observe` method no-longer accept Fragment (`this`) as the `lifecyclerOwner` and we need to use `viewLifecycleOwner` property of Fragment instead.
   * `binding.setLifecycleOwner(this)` &rarr; `binding.lifecycleOwner = viewLifecycleOwner ` (In Fragments)
   * `ViewModelProviders.of(this)` &rarr; `ViewModelProvider(this)`

4. Lesson 8 - Connect to the internet (Mars Real Estate App)

   Build REST API client using retrofit2, coroutines and glide (for image loading) and a RecyclerView with DataBinding perks.

   **Changes:**

   * Using the latest retrofit version, targeting java sdk "1.8"

     ```gradle
     compileOptions {
     	sourceCompatibility JavaVersion.VERSION_1_8
     	targetCompatibility JavaVersion.VERSION_1_8
     }
     kotlinOptions { jvmTarget = "1.8" }
     ```

   * Fixed `java.io.IOException: Cleartext HTTP traffic to storage.googleapis.com not permitted`

     1. create `network_security_config.xml` with following content

        ```xml
        <?xml version="1.0" encoding="utf-8"?>
        <network-security-config>
            <base-config cleartextTrafficPermitted="false" />
            <domain-config cleartextTrafficPermitted="true">
                <domain includeSubdomains="true">mars.jpl.nasa.gov</domain>
            </domain-config>
        </network-security-config>
        ```

     2. Specify the same in `AndroidManifest.xml`

        ```xml
        <application
        	...           
        	android:networkSecurityConfig="@xml/network_security_config"
        ```