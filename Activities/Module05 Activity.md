---
layout: page
title: Web Socket Activity
nav_exclude: true
---

## Test Adequacy Activity
This project will give you practice in working with web sockets which enable you to use emitter pattern. 

Start by downloading the [starter code]({{ site.baseurl }}{% link Activities/module-05-websocket-activity.zip %}).

### Instructions
The current protocol, in `webSocketsSimple/shared.ts', has the server start the conversation with each client by sending it a `ping`

Modify this system in the following ways:
1. The server should keep track of the number of clients that are connected.
2. When a new client joins, the client should send the server a `hello` message with its name.
3. When the server sees the new client, it should print to the console the name of the new client and the total number of connected clients. It should then send an initial ping to the new client, as it does now.
4. When a client is disconnected, the server should print to the console the name of the client that is leaving and the updated number of connected clients.

Check your solution by running `npx ts-node demo-server.ts` in one shell window, and `npx ts-node demo-clientAB.ts` in a separate window.  Try starting the server first, and then the clients; then try starting the clients first and then the server. Observe the differences in behavior, if any. This check is for your purposes only, you need not submit it unless your instructor requires it in the Canvas assignment.

When you are done, submit your work as required by your instructor (check the Canvas asssignment for details, if assigned). This may vary from section to section.