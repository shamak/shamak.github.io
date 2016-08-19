---
layout: post
title:  "Analysing the Big Money Strategy in Dominion"
date:   2015-09-10 00:40:54
---

[Dominion](https://en.wikipedia.org/wiki/Dominion_(card_game)) is deck building game which I recently started playing. Quoting from Wikipedia - 

*Each player uses a separate deck of cards; players draw their hands from their own decks, not others'. Players use their cards to perform actions and buy cards from a common pool of card stacks, including Action, Treasure, and Victory cards. The player with the most victory points wins.*

Each game is different as you can play with a unique set of card stacks. These stacks come with the game and there are various expansions to the game where you get more card stacks. The game involves a lot of strategy (as with any card game, usually) and is a lot of fun! I definitely recommend trying it out. 

There's a basic strategy in Dominion called [Big Money](http://dominionstrategy.com/big-money/). I highly recommend you click on the link to understand what it's about. The link also provides a very apt description of different strategies you can play comparing them to rolling a die. As a beginner, I've lost to the Big Money strategy so many times. It annoyed me and I wanted to write a program to simulate the player using that strategy to see the average number of points it would actually achieve in an ideal game situation (no interaction with other cards/players).

Here's a [link](https://github.com/shamak/dominion_strategy_analysis) to the code I wrote to simulate the strategy. The results show that on average it would only give you 19 points over 15 turns, which is pretty good if the game gets over before 15 turns with about 3-4 players. The code does very simplistic things, buys gold whenever possible, buys provinces whenever possible. It does not take into account how long the game has been running so as to buy more victory cards. It might be cool to develop an AI for the game to quickly analyse the card stacks and determine what the best strategy would be. 