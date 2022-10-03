# Ruihan

I know this page is public so I did not what to put any sensative or overly personal information.

Styling text : 

Hi, my *name* <sub>is</sub> ~~not~~ ***Ruihan***

Quoting text:

> I am a programmer and a person, I think

Quoting code:

some code I helped write a while back

```js
exports.run = async function (client, message) {

  // User must be in channel
  if (!message.member.voice.channel) {
    message.channel.send(`You must be in the voice channel from which you want to move users.`);
    return;
  }
  let start_vc = message.member.voice.channel;

  // Command must contain target channel ID
  let tokens = message.content.split(" ");
  if (tokens.length <= 1) {
    message.channel.send(`Must specify target channel (via Copy ID).`);
    return;
  }
  let target_vc_id = tokens[1];

  // Target channel ID must be a voice channel
  let target_vc = message.guild.channels.cache.get(target_vc_id);
  if (!target_vc) {
    message.channel.send(`Couldn't find target channel.`);
    return;
  }
  if (target_vc.type != "GUILD_VOICE") {
    message.channel.send(`Target channel ID must be for a must be a voice channel.`);
    return;
  }

  // Target channel must be available to the mover
  let dev = message.guild.roles.cache.get("637279237841354754");
  let mod = message.guild.roles.cache.get("408106863117336577");
  let admin = message.guild.roles.cache.get("408106459910504458");
  if (!target_vc.permissionsFor(message.member).has("CONNECT") && !message.member.roles.cache.has(dev.id) && !message.member.roles.cache.has(mod.id) && !message.member.roles.cache.has(admin.id)) {
    message.channel.send(`You must be able to enter the target channel.`);
    return;
  }


  let members = [...start_vc.members.values()];
  let movedlist = new Array();
  let moverperms = target_vc.permissionsFor(message.member).toArray();

  for (let i = 0; i < members.length; i++) {
    movedlist.push(members[i].displayName);
    if (!target_vc.permissionsFor(members[i]).has("CONNECT")) {
      target_vc.permissionOverwrites.edit(members[i], {'CONNECT': true}).then(async () => {
        await members[i].voice.setChannel(target_vc).catch(() => null);
      }).then(() => {
        setTimeout(() => {
          target_vc.permissionOverwrites.delete(members[i].id);
        }, 1000)
      }).catch((err) => console.log(err));
    } else {
      await members[i].voice.setChannel(target_vc).catch(() => null);
    }
  }

  // Log move.
  message.channel.send(`**${message.member.displayName}** has moved the users in **${start_vc.name}** to **${target_vc.name}**.\n\nMoved: ${movedlist.join(", ")}`);
};

exports.conf = {
  enabled: true,
  guildOnly: false,
  aliases: ["mm"],
  permLevel: permLevel.INACTIVEMENTOR
};

exports.help = {
  name: "massmove",
  description: "Move all from current voice channel into another",
  usage: "massmove <target channel ID>"
};
```

External Links:

You can find an example of a project I worked on [here](https://gitlab.com/qhp/wdr-discord-bot/). Oh wait, it's private

Section links :

[Clicking on this takes you to the top of the page](#ruihan)

Relative links:

[Don't look](README.md)

Pictures :

![image1](https://i.postimg.cc/T2SgBP2d/1.png) 
Ruihan is very lazy and makes poor Jason do all the work

![image2](https://i.postimg.cc/XJ2jtXwn/selfie.jpg) 
Where am I? (yes the guy in the picture is actually me)

Ordered and Unordered Lists :

Thing I like to do
- cooking and eating Chinese food
- swimming
- programming

some CSE classes I took in order

1. CSE 11
2. CSE 12
3. CSE 30

Task lists :

TODO LIST
- [x] CSE Homework :computer:
- [ ] Math Homework :heavy_multiplication_x:
- [ ] Spanish Homework :speaking_head: