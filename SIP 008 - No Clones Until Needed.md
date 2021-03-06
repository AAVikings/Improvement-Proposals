# SIP 008 - No Clones Until Needed

_This is a recommendation by Luis Molina to be implemented as a core team effort._

The Clones Concept is going to become a fundamental part of the evolution of Financial Beings. We expect people to fork and clone other people's Financial Being in the future. But we are not there yet, and today dealing with this concept introduces an artificial entry barrier. Besides that the Clones Module is designed for tech savvy users, allowing them to view raw logs and requiring them to have and underlaying understanding of the system that it is not even documented.

### Today is an Entry Barrier

Today this represents an entry barrier and it is difficult to digest why a new user is required to manually create several clones with parameters he does not understand in a system that is precisely about automation.  

### Proposal

Lets start the clones that the users would need automatically with some default parameters so as to avoid users to learn about them and to completely remove this entry barrier. The Clones Module could still be there, in case needed and for the time users start digging and trying to diverge from the most probable common usage and would like to run their clones in a different way.

These are the clones that would need to run automatically immediately after signup:

```
Trading Simulation with Market Files starting 1 year prior to the date of signup.
Trading Simulation with Daily Files starting 30 day prior to the date of signup @ 10 Min timePeriod.
Trading Executor @ Poloniex @ BTC / USDT.
Trading Executor @ Coss @ BTC / USDT.
```

The trading clones should:

1. Run every 10 minutes.
2. Do not stop if something is missing, like the exchange keys, just continue running until that is set it up properly.

The simulation should keep running.

The Strategizer should have a "Recalculate Simulations" button, that removes both Trading Simulations clones and creates fresh ones, again starting from the same dates the original clones started (so that users can easily compare and see the difference in performance of the changes in their strategies).

With this "Last Mile" improvement, we can target a wider market of exchange users that are not tech savvy enough to operate the Clones Modules and that is they would do, most likelly they would use a similar set of initial values.  
