# encoding: UTF-8
require 'cinch'
require 'httparty'
require 'timeout'
require 'pstore'
require_relative 'rubyfunge'
require_relative 'brainfuck'
require_relative 'word_game'
include Cinch
BOTS = %w(fungot DoofBot HackEgo YayBot idris-bot EgoBot lambdabot Doofbot)
BANS = %w(Disgurntledman)
messages = {}
tells = PStore.new('tells.pstore')
dootbot = Bot.new do
  configure do |c|
    c.server = 'orwell.freenode.net'
    c.nick = 'DootBot'
    c.plugins.plugins = [ Cinch::Plugins::WordGame ]
  end

  on :join do |m|
    if m.user.nick == 'DootBot'
      messages[m.channel] = []
      m.reply('DOOT DOOT!')
    elsif m.channel == '#tppleague'
      m.reply("HELLO #{m.user.nick.upcase}!")
    end
  end
