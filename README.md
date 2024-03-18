# web-chat-app
A chat app designed for private conversations with end-to-end encryption.

## Architecture
1. Client (React.js)
    * Main page (authentication)
    * Friends list page (after successfully logging in)
        - Friends list
        - Chat window
2. Server
    * Endpoints
        - Authentication endpoint for login
        - Authentication endpoint for signup
        - Find user by ID
        - Add the user with a given ID as a friend
        - Acknowledge a friend invitation received
        - Get friends list
        - Post to the queue of messages of a friend
    * DB Schema: (TODO)

## Features
1. End-to-end encryption
2. Authentication (bcrypt, JWT)
3. Friends look up and connect
4. Real-time communication (Socket.io)
5. New and past message storage (MongoDB? Is NoSQL really a better choice than RDBMS?)

## Timeline
TBD

## References
1. [Design A Chat System](https://bytebytego.com/courses/system-design-interview/design-a-chat-system)
2. [How to build your own real-time chat app](https://www.freecodecamp.org/news/building-a-chat-application-with-mean-stack-637254d1136d/)
3. [How JWT (JSON Web Token) authentication works?](https://dev.to/kcdchennai/how-jwt-json-web-token-authentication-works-21e7)
4. [How to Secure Your MERN Stack App with JWT-Based User Authentication and Authorization](https://www.freecodecamp.org/news/how-to-secure-your-mern-stack-application/)

### Some stuff to learn about
* [Socket.io Introduction - How to Build a Chat App](https://www.youtube.com/watch?v=SGQM7PU9hzI)
* [Learn Socket.io In 30 Minutes](https://www.youtube.com/watch?v=ZKEqqIO7n-k)
