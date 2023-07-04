---
label: Commands
order: 2
---

# Commands
Commands are those things starting with a `/` ingame.

## Command class
Your command class should have a `@Command` annotation in it.
```java
package org.galliumpowered.example;

import net.kyori.adventure.text.Component;
import org.galliumpowered.api.annotations.Command;
import org.galliumpowered.commandsys.CommandContext;

public class MyCommand {
    @Command(aliases = {"hello"}, description = "Hey!")
    public void myCommand(CommandContext ctx) {
        ctx.getCaller().sendMessage(Component.text("Hey!"));
    }
}
```
## Main class
You need to register your command!
```java
package org.galliumpowered.example;

import com.google.inject.Inject;
import org.galliumpowered.api.annotations.PluginLifecycleListener;
import org.galliumpowered.commandsys.PluginCommandManager;
import org.galliumpowered.plugin.PluginLifecycleState;
import org.apache.logging.log4j.Logger;

public class MyPlugin {
    @Inject
    private Logger log;

    @Inject
    private PluginCommandManager commandManager;

    @PluginLifecycleListener(PluginLifecycleState.ENABLED)
    public void onPluginEnable() {
        log.info("Hey!");
        commandManager.registerCommand(new MyCommand());
    }
}
```
