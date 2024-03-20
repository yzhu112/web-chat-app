# web-chat-app
A chat app designed for private conversations with end-to-end encryption.

## Table of contents
  - [Architecture](#architecture)
    - [Diagram](#diagram)
    - [Client (React.js)](#client-reactjs)
    - [Server](#server)
      - [API Endpoints](#api-endpoints)
      - [DB Schema](#db-schema)
  - [Features](#features)
  - [Timeline](#timeline)
  - [Notes](#notes)
    - [NoSQL vs SQL](#nosql-vs-sql)
  - [References](#references)
    - [Some stuff to learn about](#some-stuff-to-learn-about)


## Architecture
### Diagram
(subject to change and revision)

![Chat App Architecture](https://github.com/yzhu112/web-chat-app/assets/76628827/fa6c1ad9-f9a2-4741-86f1-51f5303e2675)

### Client (React.js)
* Main page (authentication)
* Friends list page (after successfully logging in)
    - Friends list
    - Chat window

### Server
#### API Endpoints

* Endpoints
  - Authentication endpoint for login
  - Authentication endpoint for signup
  - Find user by ID
  - Add the user with a given ID as a friend
  - Acknowledge a friend invitation received
  - Get friends list
  - Post to the queue of messages of a friend

  | Endpoint                    | Method | Description                                  |
  | :-------------------------- | :----- | :------------------------------------------- |
  | /api/users/{id}             | GET    | Get user by ID                               |
  | /api/users/create           | POST   | Create a new user                            |
  | /api/users/{id}/update      | PUT    | Update user by ID                            |
  | /api/users/{id}/delete      | DELETE | Delete user by ID                            |
  | /api/auth/signup            | POST   | Register a new user                          |
  | /api/auth/login             | POST   | Log in an existing user                      |
  | /api/auth/logout            | POST   | Log out the current user                     |
  | /api/auth/reset-password    | POST   | Reset user password                          |
  | /api/friend-req/send        | POST   | Send a friend request                        |
  | /api/friend-req/{id}/accept | PUT    | Accept a friend request by friend request ID |
  | /api/users/{id}/friends     | GET    | Get list of friends for a user by ID         |
  | /api/chats/{id}             | GET    | Get chats by user ID                         |
  | /api/messages/{id}          | GET    | Get messages by chat ID                      |
  | /api/chats/{id}/send        | POST   | Get list of friends for a user by ID         |
  | /api/users/{id}/status      | PUT    | Update the status of a user by ID            |
  | /api/users/{id}/status      | GET    | Get the current status of a user by ID       |

  (How do api calls work with websockets?)

#### DB Schema
<details>
<summary>User Collection</summary>

| Field              | Type         | Notes                                   |
| :----------------- | :----------- | :-------------------------------------- |
| _id                | ObjectId     | (primary key)                           |
| username           | String       | user's username                         |
| email              | String       | user's email                            |
| password           | String       | user's password stored as a hash        |
| registration_date  | Date/ISODate | user's registration date as a timestamp |

</details>

<details>
<summary>Chat Collection</summary>

| Field              | Type              | Notes                                    |
| :----------------- | :---------------- | :--------------------------------------- |
| _id                | ObjectId          | (primary key)                            |
| chat_name          | String            | name of group chat or null for 1:1 chats |
| created_by_user_id | ObjectId          | an _id from the User collection          |
| created_at         | Date/ISODate      | chat creation timestamp                  |
| members            | Array of ObjectId | array of _id s from the User collection  |

</details>

<details>
<summary>Message Collection</summary>

| Field              | Type         | Notes                                    |
| :----------------- | :----------- | :--------------------------------------- |
| _id                | ObjectId     | (primary key)                            |
| chat_id            | ObjectId     | an _id from the Chat collection          |
| sender_id          | ObjectId     | an _id from the User collection          |
| receiver_id        | ObjectId     | an _id from the User collection          |
| msg_content        | String       | content of the msg (utf-8)               |  
| timestamp          | Date/ISODate | message timestamp                        |

</details>


## Features
1. End-to-end encryption
2. Authentication (bcrypt, JWT)
3. Friends look up and connect
4. Real-time communication (Socket.io)
5. New and past message storage (MongoDB? Is NoSQL really a better choice than RDBMS?)
6. Custom data retention period (lifetime/a year/a month)
7. Data export and backup for messages and contacts
8. 1:1 chats and group chats with a max size of <?>
9. Message and media search in chat history
10. User presence status: online or offline 
11. Optional: Game disguise with a toggleable stealth mode to hide the chat interface

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