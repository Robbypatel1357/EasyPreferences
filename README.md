EasyPreferences
===============

A small library containing a wrapper/helper for the shared preferences of Android.

With this library you can initialize the shared preference inside the onCreate of the Application class of your app.

```Java
public class PrefsApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        // Initialize the Prefs class
        new Prefs.Builder()
                .setContext(this)
                .setMode(ContextWrapper.MODE_PRIVATE)
                .setPrefsName(getPackageName())
                .setUseDefaultSharedPreference(true)
                .build();
    }
}
```

# Usage

After initialization, you can use simple one-line methods to save values to the shared preferences anywhere in your app, such as:

- `Prefs.putString(key, string)`
- `Prefs.putLong(key, long)`
- `Prefs.putBoolean(key, boolean)` 

Retrieving data from the Shared Preferences can be as simple as:

    String data = Prefs.getString(key, default value)

If the shared preferences contains the key, the string will be obtained, otherwise the method returns the default string provided. No need for those pesky `contains()` or `data != null` checks!

For some examples, see the sample App.

## Bonus feature: ordered sets

The default implementation of `getStringSet` on Android **does not preserve the order of the strings in the set**. For this purpose, EasyPreferences adds the methods:

    void Prefs.putOrderedStringSet(String key, Set<String> value);

and

    Set<String> Prefs.getOrderedStringSet(String key, Set<String> defaultValue);

which internally use Java's LinkedHashSet to retain a predictable iteration order. These methods have the added benefit of adding the missing functionality of storing sets to pre-Honeycomb devices.


# Download
Download the latest [AAR][1] or grab via Maven:
```XML
<dependency>
  <groupId>com.pixplicity.easyprefs</groupId>
  <artifactId>library</artifactId>
  <version>1.8.1</version>
  <type>aar</type>
</dependency>
```

or Gradle:
```Groovy
repositories {
    maven { url "http://dl.bintray.com/pixplicity/maven" }
}
dependencies {
    compile 'com.pixplicity.easyprefs:library:1.8.1@aar'
}
```

# License

```
Copyright 2014 Pixplicity (http://pixplicity.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```


[1]: https://bintray.com/artifact/download/pixplicity/maven/com/pixplicity/easyprefs/library/1.8.1/library-1.8.1.aar