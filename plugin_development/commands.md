---
label: Commands
order: 20
---

# Commands
Commands are those things starting with a `/` ingame.

## Command class
Your command method should have a `@Command` annotation in it.

The method should take CommandContext as a parameter.

```java
package org.galliumpowered.example;

import net.kyori.adventure.text.Component;
import org.galliumpowered.annotation.Command;
import org.galliumpowered.command.CommandContext;

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
import org.galliumpowered.annotation.PluginLifecycleListener;
import org.galliumpowered.command.PluginCommandManager;
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
