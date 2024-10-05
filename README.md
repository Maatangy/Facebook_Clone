# Facebook Clone

![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![Apache Maven](https://img.shields.io/badge/Apache%20Maven-C71A36?style=for-the-badge&logo=Apache%20Maven&logoColor=white)
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
![ElasticSearch](https://img.shields.io/badge/-ElasticSearch-005571?style=for-the-badge&logo=elasticsearch)
![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-000?style=for-the-badge&logo=apachekafka)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)

This is a full-stack Facebook clone built with React and Spring Boot microservices.

[Watch Demo on YouTube](https://www.youtube.com/watch?v=SppYteB37PU&t=2s&ab_channel=ritikchauhan)

---

## Features 😎

- **Offline-first PWA**: Responsive web app built with React.
- **User Registration**: Users can create accounts with unique usernames and passwords.
- **Profile Management**: Users can create profiles with avatars, cover photos, and personal information.
- **Post Updates**: Users can post updates with text and photos on their profiles.
- **News Feed**: Users can see updates from their friends in the news feed.
- **Friend Requests**: Users can send and withdraw friend requests, as well as accept or decline requests.
- **Notifications**: Real-time notifications via WebSockets for friend requests, messages, and updates.
- **Search Functionality**: Users can search for others and posts across Facebook.

---

## Technologies Used ⚒️

### FrontEnd

- Built with [React](https://react.dev/) (v18.2.0)
- Styles using [SCSS](https://sass-lang.com/)
- Responsive layouts for Desktop, Tablet, and Mobile views
- Offline-first PWA support with light and dark themes

### APIs

- REST APIs are used for microservice communication via the Gateway
- Real-time notifications sent through WebSockets using the [STOMP protocol](https://stomp.github.io/)

### Security

- **JWT authentication**: Required to communicate with backend services.
- All REST API calls require a valid JWT token in the `Authentication` header (except for login and register).
- WebSocket connections also require a valid JWT token in the `Authentication` request param.
- All backend microservices are secured behind a Gateway.

### BackEnd

- Backend built with [Spring Boot](https://spring.io/projects/spring-boot) (v3.1.1) and [JDK](https://www.oracle.com/java) (v17)
- [Apache Maven](https://maven.apache.org/) for dependency management

### Gateway & Consul

- [Consul](https://www.consul.io/) is used for service registry and discovery.
- Handles load balancing and inter-microservice communication.
- Also acts as a key-value store for microservices.

### Database

- [MongoDB](https://www.mongodb.com/) with [Spring Data MongoDB](https://spring.io/projects/spring-data-mongodb) (v4.1.1)
- [GridFS](https://www.mongodb.com/docs/manual/core/gridfs/) is used for storing user avatars, post images, etc.
- [ElasticSearch](https://www.elastic.co/) for fast search of users and posts.

### Caching

- [Guava Caching](https://github.com/google/guava) for faster retrieval of user profiles and posts.
- Also used for creating user feeds efficiently.

### Message Broker

- [Apache Kafka](https://kafka.apache.org/) for event-driven communication between microservices.
- Three Kafka topics: `userTopic`, `postTopic`, and `friendTopic` handle user-related, post-related, and friend request-related events, respectively.
- Messages are consumed by the `Facebook-NotificationMS` microservice.

---

## Architecture 🏗️

![Architecture](./.github/assets/FaceBook_Architecture.png)

The application is divided into 5 key microservices:

### Facebook_Gateway

- Connects the frontend to the backend and ensures security by verifying JWT tokens for all requests (except login and register).
- Extracts user ID from valid tokens and forwards the request to the corresponding microservice.

### Facebook_UserMS

- Responsible for managing user data.
- Utilizes MongoDB for storing user info, profile pics (via GridFS), and friends lists.
- Publishes messages to `userTopic` on Kafka.

### Facebook_PostMS

- Handles the creation, storage, and retrieval of posts.
- Stores post data in MongoDB and GridFS for images.
- Uses Guava caching for efficient feed creation.
- Publishes messages to `postTopic` on Kafka.

### Facebook_FriendMS

- Manages friend requests and connections between users.
- Stores friend request data in MongoDB.
- Consumes and publishes messages to Kafka topics.

### Facebook_NotificationMS

- Handles real-time notifications for events such as new friend requests, messages, and post updates.
- Consumes Kafka messages from all relevant topics.

---

## Screen Shots 📸

| Registration Page                                   | SignIn Page                                      |
| -------------------------------------------------- | ------------------------------------------------ |
| ![Registration Page](/.github/assets/Register_Page.png) | ![SignIn Page](/.github/assets/SignIn_Page.png)  |

| Desktop UI                                         | Desktop UI (Dark Mode)                           |
| -------------------------------------------------- | ------------------------------------------------ |
| ![Desktop UI](/.github/assets/Desktop_UI.png)      | ![Desktop UI Dark](/.github/assets/Desktop_UI_Dark.png) |

| Notifications                                      | Search                                           |
| -------------------------------------------------- | ------------------------------------------------ |
| ![Notifications](/.github/assets/Notifications.png) | ![Search](/.github/assets/Search.png)            |

| Mobile UI                                          | Mobile UI (Dark Mode)                            |
| -------------------------------------------------- | ------------------------------------------------ |
| ![Mobile UI](/.github/assets/Mobile_UI.png)        | ![Mobile UI Dark](/.github/assets/Mobile_UI_Dark.png) |

| Edit Profile Page                                  | Tablet UI                                        |
| -------------------------------------------------- | ------------------------------------------------ |
| ![Edit Profile Page](/.github/assets/Edit_Profile_Page.png) | ![Tablet UI](/.github/assets/Tablet_UI.png)      |

---

## License

This project is licensed under the MIT License.

---




