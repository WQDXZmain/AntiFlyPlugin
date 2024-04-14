# AntiFlyPlugin
I was interested in creating a plugin for the Minecraft server that restricts players from using the cheat functions for flight, but I don't understand this area at all, so I asked to write code from Chat GPT. If it's not difficult, please help me compile the following code into a jar file, or write this small plugin for me manually. Thanks!

import org.bukkit.Bukkit;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerMoveEvent;
import org.bukkit.plugin.java.JavaPlugin;

public class AntiFlightPlugin extends JavaPlugin implements Listener {

    @Override
    public void onEnable() {
        getLogger().info("AntiFlightPlugin has been enabled!");
        Bukkit.getServer().getPluginManager().registerEvents(this, this);
    }

    @Override
    public void onDisable() {
        getLogger().info("AntiFlightPlugin has been disabled!");
    }

    @EventHandler
    public void onPlayerMove(PlayerMoveEvent event) {
        Player player = event.getPlayer();
        if (player.isFlying() && !player.hasPermission("antiflight.bypass")) {
            player.setFlying(false); // Отключаем полет
            player.setAllowFlight(false); // Запрещаем полет
            player.kickPlayer("Использование запрещенных функций обнаружено!"); // Кикаем игрока
        }
    }
}
