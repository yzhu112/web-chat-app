# web-chat-app
A chat app designed for private conversations with end-to-end encryption.

## Table of contents
  - [Architecture](#architecture)
  - [Features](#features)
  - [Timeline](#timeline)
  - [Notes](#notes)
    - [NoSQL vs SQL](#nosql-vs-sql)
  - [References](#references)
    - [Some stuff to learn about](#some-stuff-to-learn-about)

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
    * DB Schema:
        * User Collection

        | Field              | Type         | Notes                                   |
        | ------------------ | ------------ | --------------------------------------- |
        | _id                | ObjectId     | (primary key)                           |
        | username           | String       | user's username                         |
        | email              | String       | user's email                            |
        | password           | String       | user's password stored as a hash        |
        | registration_date  | Date/ISODate | user's registration date as a timestamp |

        * Chat Collection

        | Field              | Type              | Notes                                    |
        | ------------------ | ----------------- | ---------------------------------------- |
        | _id                | ObjectId          | (primary key)                            |
        | chat_name          | String            | name of group chat or null for 1:1 chats |
        | created_by_user_id | ObjectId          | an _id from the User collection          |
        | created_at         | Date/ISODate      | chat creation timestamp                  |
        | members            | Array of ObjectId | array of _id s from the User collection  |

        * Message Collection
        
        | Field              | Type         | Notes                                    |
        | ------------------ | ------------ | ---------------------------------------- |
        | _id                | ObjectId     | (primary key)                            |
        | chat_id            | ObjectId     | an _id from the Chat collection          |
        | sender_id          | ObjectId     | an _id from the User collection          |
        | receiver_id        | ObjectId     | an _id from the User collection          |
        | msg_content        | String       | content of the msg (utf-8)               |  
        | timestamp          | Date/ISODate | message timestamp                        |

## Features
1. End-to-end encryption
2. Authentication (bcrypt, JWT)
3. Friends look up and connect
4. Real-time communication (Socket.io)
5. New and past message storage (MongoDB? Is NoSQL really a better choice than RDBMS? *)
6. Data retention period (forever?)
7. Export/backup data (msgs and contacts)
8. Supports 1:1 chats and group chats with a max size of <?>
9. Search for messages and media in chat history
10. Just for fun/low priority/completely optional: 
    * Disguise the chat app as a simple game (sudoku, tictactoe, flappy bird, etc.) -> turn on/off stealth mode

## Timeline
TBD

## Notes
### NoSQL vs SQL
* Pros of NoSQL
    * Flexible schema: don't need to define a schema upfront; each document in a collection can have a different structure
    * Highly available: there will be minimal downtime and data loss if a server fails because data is replicated across nodes in a NoSQL system 
* Cons of NoSQL
    * Limited query capabilities
    * Data inconsistency and poor performance in some cases
* Pros of SQL
    * Good for simple aggregations over large datasets
    * Widely understood and supported
* Cons of SQL
    * performance can be poor on large datasets
    * debugging SQL can be difficult
    * SQL syntax can be verbose

## References
1. [Design A Chat System](https://bytebytego.com/courses/system-design-interview/design-a-chat-system)
2. [How to build your own real-time chat app](https://www.freecodecamp.org/news/building-a-chat-application-with-mean-stack-637254d1136d/)
3. [How JWT (JSON Web Token) authentication works?](https://dev.to/kcdchennai/how-jwt-json-web-token-authentication-works-21e7)
4. [How to Secure Your MERN Stack App with JWT-Based User Authentication and Authorization](https://www.freecodecamp.org/news/how-to-secure-your-mern-stack-application/)
5. [SQL vs. NoSQL: The Differences Explained + When to Use Each](https://www.coursera.org/articles/nosql-vs-sql)

### Some stuff to learn about
* [Socket.io Introduction - How to Build a Chat App](https://www.youtube.com/watch?v=SGQM7PU9hzI)
* [Learn Socket.io In 30 Minutes](https://www.youtube.com/watch?v=ZKEqqIO7n-k)
* [Connecting to Mongodb in Nodejs](https://learn.mongodb.com/learn/course/connecting-to-mongodb-in-nodejs)
* [Mongodb CRUD Operations in Nodejs](https://learn.mongodb.com/learn/course/mongodb-crud-operations-in-nodejs)