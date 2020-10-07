---
layout: post
title: You're up and running!
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

``` java
import com.jagrosh.jdautilities.command.CommandClientBuilder;
import net.dv8tion.jda.api.JDABuilder;
import net.dv8tion.jda.api.entities.Activity;
import net.dv8tion.jda.api.entities.Message;
import net.dv8tion.jda.api.entities.MessageChannel;
import net.dv8tion.jda.api.events.message.MessageReceivedEvent;
import net.dv8tion.jda.api.exceptions.RateLimitedException;
import net.dv8tion.jda.api.hooks.ListenerAdapter;
import net.dv8tion.jda.api.requests.GatewayIntent;
import javax.security.auth.login.LoginException;
import commands.*;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

public class xezelBot extends ListenerAdapter {
    public static void main(String[] args) throws LoginException, IOException, IllegalArgumentException, RateLimitedException {
        //first argument is token
        String token = args[0];
        //second argument is ownerID
        String ownerID = args[1];
        //Initializes command client builder
        CommandClientBuilder commandClientBuilder = new CommandClientBuilder();
        //Sets game to "Type ;help"
        commandClientBuilder.useDefaultGame();
        //Sets owner of the bot
        commandClientBuilder.setOwnerId(ownerID);
        //Sets prefix of bot to ;
        commandClientBuilder.setPrefix(";");
        //Adds commands
        commandClientBuilder.addCommands(
                new owoifyTextCommand()
        );
        //Initializes the bot
        JDABuilder.createLight(token, GatewayIntent.GUILD_MESSAGES, GatewayIntent.DIRECT_MESSAGES)
                .addEventListeners(new xezelBot(), commandClientBuilder.build())
                .setActivity(Activity.playing("OwO Whats this!?"))
                .build();
    }
    //Test command to make sure bot runs
    @Override
    public void onMessageReceived(MessageReceivedEvent event) {
        Message msg = event.getMessage();
        if (msg.getContentRaw().contains("uwu")) {
            MessageChannel channel = event.getChannel();
            channel.sendMessage("**OwO**").queue();
        }
        else if (msg.getMentionedUsers().toString().contains("295234517839380481") || msg.getMentionedUsers().toString().contains("755737263585099776")) {
            MessageChannel channel = event.getChannel();
            xezelRandom(channel);
        }
    }
    public void xezelRandom(MessageChannel channel) {
        List phrases = Arrays.asList(
                "I hate women", "hamburger", "moment", "yeah man yeah dude yeah bro", "burger", "bruh", "sex",
                ":woman_bald:", "ok buddy", "hamburger cheeseburger bigmac whopper"
        );
        int choices = (phrases.size() - 1);
        int choice = (int) (Math.random() * (choices + 1));
        String message = phrases.get(choice).toString();
        channel.sendMessage(message).queue();
    }
}
```

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.