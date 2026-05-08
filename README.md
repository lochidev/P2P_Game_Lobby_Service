# TCP, P2P Game Lobby Service

This program acts as a meeting point (a "Lobby") for hosts on the internet. For example, if Host A needs to find a random Host B to start an online game, Host A connects to this Lobby and waits until the Lobby assigns an available peer.

1. Registration -  When a host connects, the server captures its connection details. Since it is handling multiple hosts, std::thread is used to spawn a new thread for each connection. To prevent race conditions when keeping track of hosts, thread-safe access has been implemented.

2. Discovery - The Lobby maintains an active registry of waiting peers. STL containers (like std::vector or std::map) were used to keep track of all the connected hosts. The focus was placed on using RAII principles and Smart Pointers (std::unique_ptr) to ensure that if a host disconnects or a thread terminates, there are no memory leaks.

3. Coordination - Once two hosts are matched, the Lobby sends the IP/Port info to both peers. This uses TCP sockets to ensure the handshake data is delivered reliably. After the "introduction," the Lobby drops the connection so the peers can talk directly.

This might be a good indication of my knowledge on C++ STL and multi-threading. I learned alot working on this project

Amazing resource I used to learn multi-threading -> [Chili's multi-threading series](https://www.youtube.com/watch?v=f-1rZdMEzE8&list=PLqCJpWy5Fohe9b4gS5_HHyYcGNXVrtKUa "Chili's multi-threading series") 
