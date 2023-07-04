# Subcommands
Subcommands
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

    @Command(parent = "hello", aliases = {"hello2"}, description = "Hey!")
    public void myCommand(CommandContext ctx) {
        ctx.getCaller().sendMessage(Component.text("Hey2!"));
    }
}
```
