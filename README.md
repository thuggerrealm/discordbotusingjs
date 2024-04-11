# discordbotusingjs
const Discord = require('discord.js');
const client = new Discord.Client();
const { prefix, token } = require('./config.json');

client.once('ready', () => {
    console.log('Bot is ready!');
});

client.on('message', message => {
    if (!message.content.startsWith(prefix) || message.author.bot) return;

    const args = message.content.slice(prefix.length).trim().split(/ +/);
    const command = args.shift().toLowerCase();

    if (command === 'ping') {
        message.channel.send('Pong!');
    } else if (command === 'hello') {
        message.channel.send(`Hello ${message.author}!`);
    } else if (command === 'join') {
        if (!message.member.voice.channel) {
            message.reply('You need to be in a voice channel to use this command.');
            return;
        }
        message.member.voice.channel.join()
            .then(connection => {
                message.channel.send('Successfully joined the voice channel!');
            })
            .catch(console.error);
    }
});

client.login(token);
