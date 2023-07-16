---
label: Plugins
order: 1000
---

# Plugins
## Setting up
+++ Gradle (Groovy)
```groovy
repositories {
    mavenCentral()
    maven { url 'https://repo.zenoc.net/repository/' }
}

dependencies {
    implementation 'org.galliumpowered:gallium:1.1.0-beta.4'
    implementation 'org.apache.logging.log4j:log4j-core:2.19.0'
    implementation 'org.apache.logging.log4j:log4j-api:2.19.0'
    implementation 'org.apache.logging.log4j:log4j-slf4j2-impl:2.19.0'
    implementation 'org.slf4j:slf4j-api:2.0.1'
    implementation 'com.google.guava:guava:32.0.1-jre'
    implementation 'com.google.inject:guice:7.0.0'
    implementation 'net.kyori:adventure-api:4.2.0'
} 
```
+++ Gradle (Kotlin)
```kts
repositories {
    mavenCentral()
    maven("https://repo.zenoc.net/repository")
}

dependencies {
    implementation("org.galliumpowered:gallium:1.1.0-beta.4")
    implementation("org.apache.logging.log4j:log4j-core:2.19.0")
    implementation("org.apache.logging.log4j:log4j-api:2.19.0")
    implementation("org.apache.logging.log4j:log4j-slf4j2-impl:2.19.0")
    implementation("org.slf4j:slf4j-api:2.0.1")
    implementation("com.google.guava:guava:32.0.1-jre")
    implementation("com.google.inject:guice:7.0.0")
    implementation("net.kyori:adventure-api:4.2.0")
}
```
+++

## Defining a plugin
!!!warning
Do not use both an annotation and JSON to define a plugin. Pick one and only use that.
!!!
### JSON
JSON can be used to define a plugin. It should be a `plugin.json` file in your resources. Consider the following template:
```json
{
    "mainClass": "org.gallium.example.MyPlugin",
    "name": "My Plugin",
    "id": "myplugin",
    "description": "My first Gallium plugin",
    "authors": ["You"],
    "version": "1.1"
}
```
### Annotation
Plugins can also be defined through an annotated main class. Consider the following template:
```java
@Plugin(name = "My Plugin",
        id = "myplugin",
        description = "My first Gallium plugin",
        authors = { "You" },
        version = "1.0")
```
If you are using this method, ensure that your `Main-Class` attribute is properly set.

## Main class
Once you've chosen your preferred definition method, we can move onto the main class.

Here, we are injecting a logger to be used and saying `Hey!` once the plugin is enabled.
```java
package org.galliumpowered.example;

import com.google.inject.Inject;
import org.galliumpowered.annotation.PluginLifecycleListener;
import org.galliumpowered.plugin.PluginLifecycleState;
import org.apache.logging.log4j.Logger;

public class MyPlugin {
    @Inject
    private Logger log;

    @PluginLifecycleListener(PluginLifecycleState.ENABLED)
    public void onPluginEnable() {
        log.info("Hey!");	
    }
}
```
