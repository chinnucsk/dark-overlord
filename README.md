How can we demo distributed Erlang if not by having a dark overlord control an army of minions...

## Overview

Only the dark overlord needs to have this code compiled and loaded into an Erlang VM.
The minions only needs to connect to the master node.
The necessary minion code will then be loaded into the remote nodes by the master node.

### Compiling

```bash
$ ./rebar compile
```

## The Dark Overlord: Starting the master node

```bash
$ erl -sname hypnosponge@overlord -setcookie TheHypnoSpongeKnowsBest
```

## The Minions: Connect to the Dark Overlord

```bash
$ erl -sname minion -connect_all false -setcookie TheHypnoSpongeKnowsBest -s net_adm ping_list hypnosponge@overlord
```

```erlang
(minion@iris)1> nodes().
[hypnosponge@overlord]
(minion@iris)2> net_adm:ping('hypnosponge@overlord').
pong
```

## The Dark Overlord: Controlling your army of minions

Once your minions have connected, you can send some direct commands:

```erlang
(hypnosponge@overlord)1> darklord:sing().
```

Or you can start up the hypnosponge and compell your minions to do your bidding out "their own free will" (muhahaha!!!):
```erlang
(hypnosponge@overlord)2> sponge:start().
(hypnosponge@overlord)3> sponge:sing().
```
