---
label: Events
order: 2
---

Example listener class:
```java
package org.galliumpowered.example.listeners;

import org.galliumpowered.annotations.EventListener;
import org.galliumpowered.event.system.ServerStartEvent;
import org.apache.logging.log4j.Logger;

public class TestListener {
    private Logger log = Gallium.getPluginManager().getPluginById("myplugin").getLogger();

    @EventListener
    public void serverStartEvent(ServerStartEvent event) {
        log.info("Hello, world");
    }
}
```

Main class:
```java
package org.galliumpowered.example;

import com.google.inject.Inject;
import org.galliumpowered.annotation.PluginLifecycleListener;
import org.galliumpowered.plugin.PluginLifecycleState;
import org.galliumpowered.example.listeners.TestListener;
import org.apache.logging.log4j.Logger;

public class MyPlugin {

    @PluginLifecycleListener(PluginLifecycleState.ENABLED)
    public void onPluginEnable() {
        // Registering the listener
        Gallium.getEventManager().registerEvent(new TestListener());
    }
}
```


