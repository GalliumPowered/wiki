---
label: Subcommands
order: 19
---

# Subcommands
A parent command is required to have a subcommand. You can use `parent` to define it. `parent` should be an alias of the parent.
```java
package org.galliumpowered.example;

import net.kyori.adventure.text.Component;
import org.galliumpowered.annotation.Command;
import org.galliumpowered.command.CommandContext;

public class MyCommand {
    // Parent command
    @Command(aliases = {"hello"}, description = "Hey!")
    public void myCommand(CommandContext ctx) {
        ctx.getCaller().sendMessage(Component.text("Hey!"));
    }

    // Subcommand
    @Command(parent = "hello", aliases = {"hello2"}, description = "Hey!")
    public void myCommand(CommandContext ctx) {
        ctx.getCaller().sendMessage(Component.text("Hey2!"));
    }
}
```
