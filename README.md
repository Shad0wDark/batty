const Discord = require("discord.js");
const YTDL = require("ytdl-core");
const TOKEN = "my token";
const PREFIX = "!bc "

function play(connection, message) {
        var server = servers[message.guild.id];

        server.dispatcher = connection.playStream(YTDL(server.queue[0], {filter: "audioonly"}));

        server.queue.shift();

        server.dispatcher.on("end", function() {
            if (server.queue[0]) play(connection, message);
            else connection.disconnect();
        
        });
}


var isReady = true;

var fortunes = [
    "Yes Sir",
    "Agreed Sir",
    "Disagreed Sir",
    "No Sir",
    "Maybe, Im not sure.",
    "I don't know",
    "Searching...",

];

var bot = new Discord.Client();

var servers = {};

bot.on("ready", function(){
    console.log("Loading computer sequences... \
    Version 1.0.5 ALPHA \
    System ready ... waiting for further orders.");
});

bot.on("guildMemberAdd", function(member) {
    member.guild.channels.find("name", "general").sendMessage("Welcome " +member+ " to the Bat-Server, I'm the Bat Computer, Batty, if you need any further help just type '!bc commands' for my assistance.");

    member.addRole(member.guild.roles.find("name", "newcomer"));
});
bot.on('message', message => {
    if (isReady && message.content === '_change')
    {
    isReady = false;
    var voiceChannel = message.member.voiceChannel;
    voiceChannel.join().then(connection =>
    {
       const dispatcher = connection.playFile('./change.mp3');
       dispatcher.on("end", end => {
         voiceChannel.leave();
         });
     }).catch(err => console.log(err));
     isReady = true;
     console.log(message.author + " changed the scene");
    }
  });
bot.on('message', message => {
    if (isReady && message.content === '_br')
    {
    isReady = false;
    var voiceChannel = message.member.voiceChannel;
    voiceChannel.join().then(connection =>
    {
       const dispatcher = connection.playFile('./brhr.mp3');
       dispatcher.on("end", end => {
         voiceChannel.leave();
         });
     }).catch(err => console.log(err));
     isReady = true;
     console.log(message.author + " brhr");
    }
  });
  bot.on('message', message => {
    if (isReady && message.content === '!bc salve')
    {
    isReady = false;
    var voiceChannel = message.member.voiceChannel;
    voiceChannel.join().then(connection =>
    {
       const dispatcher = connection.playFile('./coe.mp3');
       dispatcher.on("end", end => {
         voiceChannel.leave();
         });
     }).catch(err => console.log(err));
     isReady = true;
     console.log(message.author + " sent a special message to the server");
    }
  });  
bot.on('message', message => {
  if (isReady && message.content === '_back')
  {
  isReady = false;
  var voiceChannel = message.member.voiceChannel;
  voiceChannel.join().then(connection =>
  {
     const dispatcher = connection.playFile('./nsv/welcome back 2.wav');
     dispatcher.on("end", end => {
       voiceChannel.leave();
       });
   }).catch(err => console.log(err));
   isReady = true;
   console.log(message.author + " is back.");
   message.channel.sendMessage("Welcome back " +message.author+ ", I wish you a good stay.");
  }
});
bot.on('message', message => {
    if (isReady && message.content === '_out')
    {
    isReady = false;
    var voiceChannel = message.member.voiceChannel;
    voiceChannel.join().then(connection =>
    {
       const dispatcher = connection.playFile('./nsv/guard.wav');
       dispatcher.on("end", end => {
         voiceChannel.leave();
         });
     }).catch(err => console.log(err));
     isReady = true;
     console.log(message.author + " left.");
     message.channel.sendMessage(message.author+ ", I wish you good luck out there.");
    }
  });

bot.on('message', message => {
  if (isReady && message.content === '_agamemnon')
  {
  isReady = false;
  var voiceChannel = message.member.voiceChannel;
  voiceChannel.join().then(connection =>
  {
     const dispatcher = connection.playFile('./agamemnon.mp3');
     dispatcher.on("end", end => {
       voiceChannel.leave();
       });
   }).catch(err => console.log(err));
   isReady = true;
   console.log(message.author + " asked for the contingency plan.");
  }
});

bot.on('message', message => {
    if (isReady && message.content === '_drogas')
    {
    isReady = false;
    var voiceChannel = message.member.voiceChannel;
    voiceChannel.join().then(connection =>
    {
       const dispatcher = connection.playFile('./drogas.mp3');
       dispatcher.on("end", end => {
         voiceChannel.leave();
         });
     }).catch(err => console.log(err));
     isReady = true;
     console.log(message.author + " asked for Batman's opinion about drugs.");
     message.channel.sendMessage("Log#420 : this is my opinion about the use of illegal drugs.");
    }
  });

bot.on('message', message => {
  if (isReady && message.content === '_shakebololo')
  {
  isReady = false;
  var voiceChannel = message.member.voiceChannel;
  voiceChannel.join().then(connection =>
  {
     const dispatcher = connection.playFile('./Shake It Bololo ft. Classics of MPB.mp3');
     dispatcher.on("end", end => {
       voiceChannel.leave();
       });
   }).catch(err => console.log(err));
   isReady = true;
   console.log(message.author + " shake it bololo.");
  }
});
bot.on("message", function(message) {
    if (message.author.equals(bot.user))return;

    if (!message.content.startsWith(PREFIX)) return;

    var args = message.content.substring(PREFIX.length).split(" ");

    switch (args[0].toLowerCase()) {
        
        case "log":
            message.console.sendMessage("use '_' before a certain audio file name to play it.");
            console.log(message.author + " asked for the log explication.");
            break;
        case "bleed":
            message.channel.sendMessage("http://i.imgur.com/MTPaRmV.gifv");
            console.log(message.author + " asked for blood.");
            break;
        case "version":
            message.channel.sendMessage("Alpha version 1.0.5");
            console.log(message.author + " version");
            break;
        case "suits":
            message.channel.sendMessage("http://batman.wikia.com/wiki/Batsuit");
            console.log(message.author + " suits");
            break;
        case "patch":
            message.channel.sendMessage("");
            console.log(message.author + " patch");
            break;    
        case "nice_work":
            message.channel.sendMessage("Thanks you for the compliment " +message.author+ ", I was just doing what I was told to do. ");
            console.log(message.author + " nice_work");
            break;
        case "protocols":
            message.channel.sendMessage("");
            console.log(message.author + " protocols");            
            break;       
        case "im_out":
            message.channel.sendMessage("Farewell " +message.author+  " waiting for you to come back.");
            console.log(message.author + " im_out");
            break;
        case "info":
            message.channel.sendMessage("I am the Bat computer's AI, Batty for more faster communication, and my master is <@234520719566962688> (batman). ");
            console.log(message.author + " pilot");        
            break;
        case "status":
            message.channel.sendMessage("Fully armed and operational at your orders");
            console.log(message.author + " status");
            break;
        case "mission":
            message.channel.sendMessage("I am the Bat computer's AI, Batty, created to assist <@234520719566962688>.");
            console.log(message.author + " mission");
            break;
        case "opinion":
            if (args[1]) message.channel.sendMessage(fortunes[Math.floor(Math.random() * fortunes.length)]);
            else message.channel.sendMessage("ERROR 404: MISSING QUESTION");
            console.log(message.author + " asked my opinion");
            break;
        case "commands":
            var commands = new Discord.RichEmbed()
                .addField("Here is my list of Commands:")
                .addField("mission", "Show information about me.")
                .addField("Opinion", "I can give my honest opinion about a certain subject of interest.")
                .addField("music commands", "play + link, skip, stop")
                .addField("spotify", "no need to say")
                .addField("salve", "special message for all the server")
                .addField("filmes", "show a list of upcoming superhero movies in the near future")
                .addField("liga", "shows the actual composition of the Justice League")
                .addField("status", "I'll tell you my actual condiction.")
                .addField("protocols","I will show my current protocols")
            message.channel.sendEmbed(commands);
            console.log(message.author + " asked for my commands");
            break;
        case "liga":
            message.channel.sendMessage("Batman=Shadow#4434, Superman=Arthur#0885, Mulher-Maravilha=giitoschii#1300, Lanterna-Verde=Rangel#9353, Flash=Henrique Lyra#7581, BatGirl=Duda#3589, Mutano=Walter#6960, Black Adam=Deus Negro#3072, Sasuke=Cesar#9484, Deadpool(?)=Vitormamede#6395");
            console.log(message.author + " asked about the actual composition of the Justice League");
            break;
        case "hey":
            message.channel.sendMessage(message.author.toString() + " Yes Sir do you need anything?");
            console.log(message.author + " said hey");
            break;
        case "nickname":
            message.channel.sendMessage("I do not have a name, but for the idea of making communication easier, I have been assigned the nickname of Batty, an allusion to the word Bat, as to Batman, and the name Betty.")

            break;
        case "spotify":
            message.channel.sendMessage("It's here > https://open.spotify.com/user/fernandomiguel99");
            console.log(message.author + " asked for your spotify");
            break;
        case "moises": 
            message.channel.sendMessage("Não Consegue né? http://i.ytimg.com/vi/HCVsd6R1L4Y/hqdefault.jpg");
            console.log(message.author + " asked for the meme");
            break;
        case "salve":
            message.channel.sendMessage("COÉ RAPAZIADAAAAA!!!! SALVE!!!! http://www.ahnegao.com.br/wp-content/uploads/2017/04/4-14.jpg");
            console.log(message.author + " welcomed the server");
            break;
        case "source":
            message.channel.sendMessage("https://github.com/Shad0wDark/batty/projects");
            console.log(message.author+ " asked for my source code Sir.");
            break;
        case "filmes":
            message.channel.sendMessage("Here you go > https://omelete.uol.com.br/calendario-de-filmes-dc-e-marvel/");
            console.log(message.author + " asked for the movies calendar");
            break;
        case "play":
            if (!args[1]) {
                message.channel.sendMessage(message.author + " Please provide me a link to use.");
                return;
            }

            if (!message.member.voiceChannel) {
                message.channel.sendMessage(message.author + " Please join a Voice Channel.");
                return;
            }
            if (!servers[message.guild.id]) servers[message.guild.id] = {
                queue: []
            };

            var server = servers[message.guild.id]

            server.queue.push(args[1]);

            if (!message.guild.voiceConnection) message.member.voiceChannel.join().then(function(connection) {
                play(connection, message);
            });
            message.channel.sendMessage("Successfully added to queue.");
            console.log(message.author + " asked for a song");
            break;
        case "skip":
            var server = servers[message.guild.id];

            if (server.dispatcher) server.dispatcher.end();
            console.log(message.author + " skipped the actual song");
            break; 
        case "stop":
             var server = servers[message.guild.id];

             if (message.guild.voiceConnection) {
            for (var i = server.queue.length - 1; i >= 0; i--) {
                server.queue.splice(i, 1);
         }
            server.dispatcher.end();
            console.log("[" + new Date().toLocaleString() + "] Stopped the queue.");
        }
            console.log(message.author + " stopped the song");
            break;
        default:
            message.channel.sendMessage("invalid command");
    }
    
});

bot.login(TOKEN);
