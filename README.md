# Flamekeeper

Flamekeeper is a free Windows app for running an **Enshrouded dedicated server**. You can change the server settings,
start and stop the server, make backups, update it through SteamCMD, add mods, post server news in a Discord channel,
and manage the server from another PC.

**[Download Flamekeeper-setup.exe](https://github.com/fren-huehuehue/Flamekeeper-releases/releases/latest/download/Flamekeeper-setup.exe)**
(newest version, Windows 10 and 11)

Flamekeeper is not made by or affiliated with Keen Games. Enshrouded is a trademark of Keen Games GmbH.

---

## Contents

- [Install](#install)
- [First start](#first-start)
- [Server tab](#server-tab)
- [Server settings: General, Gameplay, Access](#server-settings-general-gameplay-access)
- [Settings](#settings)
- [Discord channel](#discord-channel)
- [Mods](#mods)
- [Backups](#backups)
- [Remote: manage the server from another PC](#remote-manage-the-server-from-another-pc)
- [Letting players in from the internet](#letting-players-in-from-the-internet)
- [Updates](#updates)
- [Questions](#questions)

## Install

1. Download `Flamekeeper-setup.exe` (link above) and run it. It installs for your Windows user only, so you don't need
   admin rights. Flamekeeper then opens by itself.
2. Windows may show "Windows protected your PC", because the installer is not signed by a known publisher. Click
   **More info**, then **Run anyway**.

To remove Flamekeeper, go to Windows Settings > Apps > Flamekeeper > Uninstall. Your server, savegame and backups stay.

## First start

- **Server already installed** (Steam's "Enshrouded Dedicated Server" tool, or SteamCMD): Flamekeeper usually finds
  it. If it doesn't, go to the menu (☰) > **Settings** > Server folder > **Choose** and pick the folder that holds `enshrouded_server.exe`.
- **No server yet**: click **Install server** on the Server tab and pick where it should go. Flamekeeper downloads SteamCMD and the
  server (Steam app 2278520, no Steam account needed).
- **No `enshrouded_server.json` yet**: the server makes one on its first start. You can also create a default file
  with new passwords from the settings tabs.

## Server tab

- **Start / Stop / Restart.** Stop sends Ctrl+C, so the server saves before it closes. If it hasn't stopped after 30
  seconds, Flamekeeper asks whether to force it. With Discord set up, Stop first asks how long the server stays down
  (players see "back around 14:30") and whether to stop now or in some minutes, with warnings in Discord.
- **Later** plans a restart in some minutes. Discord gets a message right away and warnings 30, 15, 5 and 1 minute
  before it. **Cancel** under the buttons drops a planned restart or stop.
- **Update via SteamCMD** installs the newest server version. The server has to be stopped for this; Flamekeeper
  offers to stop it.
- **Players online** shows who is in the game. Flamekeeper reads this from the server log. Enshrouded has no kick
  command, so **Ban** puts a player on the ban list; the ban works after a restart.
- **Server Message** posts a message in your Discord channel, for example "the server restarts in 5 minutes". The
  game itself can't show messages to players. This box appears once Discord is set up (see
  [Discord channel](#discord-channel)). Switch on **@here** to ping everyone online in the channel; other pings are
  set in Settings > Discord. With the bot you can also make the message a **Poll** (✅ / ❌ under it; who clicked what
  shows under **Recent**) or **Pin it**. **Recent** lists your last messages; the bin deletes one from Discord.
- **Activity** lists what Flamekeeper did. **Server log** shows the server's own log. If the server quits on its own,
  Activity shows the important log lines and common causes.

## Server settings: General, Gameplay, Access

These tabs edit `enshrouded_server.json`. Click **Save** in the bottom bar when you're done, or **Undo** to go back.
The server reads the file when it starts, so restart it to apply your changes.

- **General**: server name, player slots, tags, IP and query port, text and voice chat, savegame and log folders.
- **Gameplay**: pick a preset (Default, Relaxed, Hard, Survival), or change values yourself. That sets the preset to
  Custom; the server only uses your own values with Custom.
- **Access**: user groups and their passwords. Players don't pick a group: the password they connect with puts them in
  one. Give every group its own password. Each group has rights: kick and ban, open chests, edit the world, edit and
  extend bases. **Banned players** lists banned Steam IDs.

Before you save, Flamekeeper warns you about values the server refuses (it would quit right away) and about groups
with an empty or shared password.

## Settings

Menu (☰) > **Settings** holds the settings of the PC that runs the server (also when you manage it from another PC):

- **Server**: the server folder (where `enshrouded_server.exe` is; **Open**, **Savegame** and **Json** open those
  folders and files). **Hide server console** runs the server without its black window. **Keep this PC awake** stops
  Windows from going to sleep while the server runs.
- **Updates**: the SteamCMD folder (Flamekeeper downloads SteamCMD there when it's missing). **Verify files on update**
  checks every file when you update (takes longer). **Flamekeeper test builds** (off by default) also updates
  Flamekeeper to new versions before they are released, for trying them out first.
- **Backups**: the backup folder, how many automatic backups to keep, how often to make them, and whether to make one
  after every stop.
- **Discord**: webhook or bot, see [Discord channel](#discord-channel).

## Discord channel

Enshrouded can't send messages to players. Instead, Flamekeeper can post server events in a Discord channel:

- start, stop and restart (a restart shows as one message), force stop, and a server that doesn't respond
- crashes, with the important log lines
- changed settings, grouped like the tabs (Player, Enemies, World, ...), with old and new values. Passwords are never
  shown, only that they changed.
- server updates (old and new build number), restored backups, failed backups
- mods switched on, off, added or removed
- players joining and leaving (switch it off under Settings > Discord)

**Webhook or bot** (Settings > Discord > Send through). You can switch at any time; Flamekeeper first lists what stops
working and what comes, and keeps both setups so switching back is one click.

- **Webhook**: simple, one URL. Flamekeeper can only post (and delete its own Server Messages).
- **Bot**: everything a webhook does, plus a pinned **status message** that keeps itself up to date (online or offline,
  who plays, when it is back), `!settings` and the other commands typed in Discord, polls with ✅ / ❌, pings picked
  from your Discord roles, and pinning messages.

To set up a webhook in Discord, open the channel's settings > **Integrations** > **Webhooks** > **New Webhook** >
**Copy Webhook URL**. In Flamekeeper, go to the menu (☰) > **Settings** > **Discord**, paste it under Webhook and click
**Test and save**. A test message shows up in the channel. To turn Discord off, clear the field and click **Turn off**.

**Server Messages ping** (in Settings > Discord, once Discord is on) sets who a Server Message pings; `@here` can also be switched on the Server tab. With the bot you pick `@here`, `@everyone` or roles. With a webhook, Discord can't ping by name, so use `@here` (everyone
online in the channel), `@everyone`, or IDs. Switch on Developer Mode in Discord (Settings > Advanced). Then right-click
a member > **Copy User ID**, or right-click a role > **Copy Role ID** and put `&` in front of it. A role such as
"Enshrouded" pings a whole group. Leave the field empty to ping nobody.

**Playtime jokes** (Settings > Discord, off by default): when someone has been online for 2, 4, 6, 8 or 12 hours in
one go, Flamekeeper teases them in the channel, and it gets wilder with every milestone. Under **Your own jokes**, pick
a milestone and add your own lines, one per line, with `{name}` for the player. Your jokes take turns with the
built-in ones, and each line comes up once before any repeats.

**Leave jokes** (Settings > Discord, off by default): when someone leaves, Flamekeeper sends them off with an insult
instead of a plain "left", with how long they played underneath. Built for a server of friends who troll each other;
the lines swear. Add your own under **Your own jokes > Leave**, with `{name}` for the player and `{time}` for how long
they played.

**Commands**: type one of these in the Server Message box and Flamekeeper posts the answer in the channel:

- `!settings`: who is online, the server name, slots, tags, chat and the gameplay values (never passwords)
- `!players`: who is online and for how long
- `!mods`: the mods that are switched on, and which ones players need too
- `!power`: what each group (Admin, Friend, ...) may do in the game

**Bot**: so players can type those commands in Discord themselves, and for the status message, polls and role pings. At [discord.com/developers/applications](https://discord.com/developers/applications): **New Application**,
then **Bot** > **Reset Token** > **Copy**, and switch on **Message Content Intent** on the same page. Then **OAuth2** >
**URL Generator**: tick the scopes `bot` and `applications.commands` and the permissions View Channels, Send Messages,
Embed Links, Add Reactions, Read Message History and Pin Messages, open the URL at the bottom and add the bot to your
Discord server. In Flamekeeper, choose **Bot** under Settings > Discord, paste the token under **Bot token** and the
channel under **Channel ID** (Developer Mode on, right-click the channel > **Copy Channel ID**; leave it empty to use
the webhook's channel), and click **Test and save**. A test message shows up in the channel. The bot answers `!settings`, `!players`,
`!mods` and `!power`, and also `/settings`, `/players`, `/mods` and `/power` (those work even without Message
Content Intent).

Flamekeeper on the server's PC sends these messages and runs the bot, so it has to be running there.

## Mods

Mods use the community mod loader [EML](https://github.com/Brabb3l/kfc-parser) (Enshrouded Mod Loader).

1. Mods tab > **Install EML**.
2. Drop a mod's `.zip` on the tab, or add it with the button. Flamekeeper unpacks it into the server's `mods` folder.
   If you add a newer version of a mod, it replaces the old one.
3. Switch mods on and off with their switch. Mods load when the server starts, so restart it afterwards.

Before each change, Flamekeeper makes a backup.

**Players need it**: click the **person icon** next to a mod when players must install it on their own PC too (a mod
that changes what they see). The icon turns yellow; hover it to see what it means, click it again to undo. `!mods` and
the Discord message when such a mod is switched on tell players they need it. Mods that only change the server's data (like the tweaks below) leave it grey.

**Turn off mods** removes EML and has SteamCMD check the game files, so you get a normal server back.

**Tweaks** (on the Mods tab) are server-side changes that Flamekeeper adds as its own small mods (`mods\flamekeeper-*`),
so EML must be installed, but players do not need to install anything:

- **Bigger stacks** (slider 1x to 10x): every stackable item holds that much more per slot. Gear does not stack and
  stays at one. What the game does with stacks that already grew bigger after going back to Normal is not known yet, so
  keep the backup Flamekeeper makes before the change.
- **Faster crafting** (slider 1x to 5x): smelter, kiln, loom and other timed recipes finish that much faster, on top of
  the factory speed setting.
- **More chest slots** (Normal or Double the size): chests you build from now on get twice the slots. Chests already
  placed keep their size until you take them down and build them again.
- **Faster fishing** (slider 1x to 2x): the fish's bar fills that much faster when you steer against it, fish bite that
  much sooner and you get that much more time to click. Fish with several rounds may get fewer. Works on top of Fishing
  on the World tab.
- **Better catches** (slider 1x to 2x): legendary fish come up that much more often, lower rarities a bit less (at 2x:
  epic 1.75x, rare 1.5x, uncommon 1.25x). Shoes and junk come up that many times less, and junk you do catch holds
  better items the same way.

Sliders move in steps of 0.05 and apply when you let go. **Normal** (1x) takes a tweak's mod out again. Tweaks apply when the server starts.

## Backups

- A backup is a zip of the savegame, plus `enshrouded_server.json`.
- **Back up now** makes one by hand. Automatic backups run every few hours while the server runs, and after every stop
  (set this under menu > Settings > Backups). Old automatic backups are removed once there are more than the number you keep; manual
  backups are never removed.
- **Restore**: pick a backup and click Restore. Flamekeeper stops the server, backs up the current state, puts the
  backup back, and starts the server again. Tick **Also enshrouded_server.json** to restore the settings too.

## Remote: manage the server from another PC

Install Flamekeeper on both PCs.

1. **On the server's PC**: Remote tab > switch on **Remote access**, then click **Firewall rules (admin)** once.
2. **On the other PC**: Remote tab > **Add a PC**, then enter the server PC's name or IP address. The server's PC can
   let you in two ways:
   - **Pair a device** shows a code (XXXX-XXXX); type it in on the other PC, or
   - the other PC sends an access request, and you click **Approve** on the server's PC.
3. Switch between servers with the button at the top right ("This PC").

Only PCs on your own network or on [Tailscale](https://tailscale.com) (for friends elsewhere) can connect, and only
devices you let in. The connection is encrypted, and each PC checks the other's fingerprint.

From PowerShell on the server's PC you can do the same with the `fk` command: `fk requests`, `fk approve <nr>`,
`fk devices`, `fk remove <name>`.

## Letting players in from the internet

- Players on your own network connect to `<server PC IP>:15637`. The Server tab shows the address.
- For players elsewhere, forward **UDP port 15637** (the query port on the General tab) in your router to the server's
  PC, and allow it in Windows Firewall (**Firewall rules (admin)** on the Remote tab does this).
- Players find the server by its name in Enshrouded's server list, or connect to your public IP address.

## Updates

Flamekeeper checks for a newer version by itself and shows a banner when there is one. Click **Update now**: the
Enshrouded server keeps running while Flamekeeper updates. You can also check by hand in the menu (☰) >
**Check for updates**. If you manage another PC, you can update the Flamekeeper there too.

## Questions

**The server quits right after it starts.** See Activity on the Server tab: it shows the server's important log lines
and common causes (a value the server refuses, another server still running, a port in use). Switch off **Hide server
console** (menu > Settings) to see the server's own messages.

**My gameplay changes do nothing.** The preset on the Gameplay tab has to be **Custom**.

**Can I message players in the game?** No, the game doesn't allow it. Use **Server Message** with a Discord channel.

**Where are Flamekeeper's own settings?** In `%APPDATA%\Flamekeeper`. Backups go to `Documents\Flamekeeper\Backups`
unless you choose another folder.
