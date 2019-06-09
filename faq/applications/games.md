# Could games be built on top of SSB?

SSB would be quite suitable for turn based games.

Generally, games are competitive, and so ensuring fairness requires consistency, i.e. turns. 
In some games, player move in a given order (i.e. in a card game, players move one at a time).
In other games, players make moves simultaneously (i.e. in rock paper scissors).
(This is distinct from collaborative tasks such as wiki editing which are cooperative and are generally fine with eventual consistency.)

This would be similar to editable documents, except that there would be well defined order that "edits" must occur in.

## Perfect information games: chess / checkers / go

Often in strategy games, all players know all information (except the plan of their opponent).
This could be easily implemented by posting messages that indicated the move taken from the previous game state.

## Rock Paper Scissors

In Rock Paper Scissors players reveal a secret simultaneously (their move).
This could be implemented securely by using a [commitment protocol](https://en.wikipedia.org/wiki/Commitment_scheme).

## Poker

Poker could be implemented securely (though, with more than 2 players you would have to trust other players not to collude, as you would in real life).
Shortly after inventing RSA encryption, Shamir, Rivest, Adleman developed a system for secure online poker called [mental poker](https://en.wikipedia.org/wiki/Mental_poker).

I am not currently aware of any online poker site that uses their system, however.
Online poker depends on a trusted server - imagine playing poker around a table, but the dealer holds the cards face up, and shuffles behind a screen.
And yes, there have been [scandals](http://freakonomics.com/2007/10/17/the-absolute-poker-cheating-scandal-blown-wide-open/) where poker sites have had backdoors and have had house players that knew what cards the other players have!
