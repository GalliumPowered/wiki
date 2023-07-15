---
label: Configurations
---

# Plugin configurations
Plugin configurations can be defined like:

```java
package org.galliumpowered.example;

import com.google.inject.Inject;
import org.galliumpowered.annotation.PluginLifecycleListener;
import org.galliumpowered.plugin.PluginLifecycleState;
import org.galliumpowered.plugin.PluginContainer;
import org.galliumpowered.config.Configuration;
import org.galliumpowered.config.PluginConfiguration;
import org.apache.logging.log4j.Logger;

public class MyPlugin {

    @Inject
    private Logger log;

    @Inject
    private PluginContainer container;

    private Configuration config;

    @PluginLifecycleListener(PluginLifecycleState.ENABLED)
    public void onPluginEnable() {
        // Create a new configuration.
        // Using Gallium implementation, this will be stored in "config/<plugin id>"
        config = new PluginConfiguration(container);

        // Set default configuration values
        config.setValue("my-thing", "Something");

        // Get a value
        log.info("my-thing: {}", config.getValue("my-thing"));
    }
}
```