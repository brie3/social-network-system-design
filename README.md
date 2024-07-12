# Trip Adviser - System Design

Example of the homework for [course by System Design](https://balun.courses/courses/system_design). 

Trip Adviser is a social network for travelers. Where people can publish travel posts with photos, a short description and a link to a specific travel location. Rating and comments on posts of other travelers. Follow other travelers to monitor their activity. Search for popular places to travel and view posts from these places in the form of TOP places by country and city. Communication with other travelers in private messages. Viewing the feeds of other travelers.

![trip-adviser-collage](./assets/trip_adviser.png)

### Functional requirements
Based on the provided business requirements, here are the functional requirements for the future social network
- **User Interaction**: The platform should offer features for easy user interaction, including messaging, commenting, liking, sharing, and following other users or businesses.
    - subscribe/unsubscribe to user channel
    - direct private messages between users
        - create, update, delete message
        - share message 
    - view user feed
        - list user feed
        - get feed by id
    - leave/remove a comment under the user's post/photo
    - list user's posts/photos
    - rate/unrate the user's post/photo
    - sort places by filter 
        - popularity 
        - number of posts 
        - number of reviews 
        - by price 
        - by location 
        - best offers 
    - creating, editing, deleting geo tags
- **Content Management**: The system should allow users to create, publish, and manage various types of content such as posts, images, videos, and articles.
    - uploading, storing, receiving photos
- **Analytics**: The platform should provide analytics tools for businesses to track user engagement, measure advertising effectiveness, and gain insights into user behavior.
    - store and provide analytics on offer reviews, ratings 
- **Notification System**: The platform should have a notification system to keep users informed about relevant activities such as new messages, comments, mentions, or updates from followed users or businesses. 
    - notify follower on new posts/photos. Mark the last message read

### Non-functional requirements
Based on the provided business requirements, here are the non-functional requirements for the future social network

- **Scalability**: The system must be able to handle linear user growth of up to 10,000,000 unique users per day over the course of a year, with room for further growth.
    - horizontally scalable architecture
    - scalable data storage
    - cloud infrastructure
- **Reliability**: The system must ensure high availability and reliability to handle the large user base and business requirements. This includes minimizing downtime, robust error handling, and fault tolerance mechanisms. 
    - automated monitoring and alerting
    - replication
    - availability 99,95% (average yearly downtime: 4 hours, 23 minutes)
- **Performance**: The system must be optimized for performance to ensure smooth user experience even during peak usage hours. This includes efficient database queries, caching mechanisms, and load balancing.
    - in-memory storage cluster
- **Mobile Compatibility**: The platform must be responsive and easily accessible from mobile devices, ensuring seamless user experience across various screen sizes and resolutions.
    - IPhone
    - Android
- **Browser Compatibility**: The system should be compatible with major web browsers to ensure accessibility for users using different browsers.
    - Chrome
    - Safari
    - Edge
    - Firefox
    - Opera
- **Security**: The platform must implement robust security measures to protect user data and prevent unauthorized access. This includes encryption of sensitive information, secure authentication mechanisms, and regular security audits.
    - SSL/TLS
    - JWT 
    - OAuth
    - MFA
- **Localization**: Since the target audience is in CIS countries, the platform should support localization features such as language preferences, regional content, and currency support. Accordingly, it is required to implement support for the following languages ​​and currencies:
    - Azerbaijan
    - Armenia
    - Belarus
    - Kazakhstan
    - Kyrgyzstan
    - Moldova
    - Russian Federation
    - Tajikistan
    - Turkmenistan
    - Uzbekistan
- **Notification System**: The platform should have a notification system to keep users informed about relevant activities such as new messages, comments, mentions, or updates from followed users or businesses. 
    - message brokers
    - full-duplex communications

## Basic calculations
Let's start with the following assumptions:

RPS:
1. DAU = 10 000 000
1. Each user create/update/delete 1 private message per week
    ```
    Maximum RPS = 10 000 000 / 86 400 / 7 ~= 17
    ```
1. Each user create/update/delete 1 post per week
    ```
    Maximum RPS = 10 000 000 / 86 400 / 7 ~= 17
    ```
1. Each user leave/remove a 1 comment under the user's post per week
    ```
    Maximum RPS = 10 000 000 / 86 400 / 7 ~= 17
    ```
1. Each user rate/unrate 1 times the user's post per day
    ```
    Maximum RPS = 10 000 000 / 86 400 ~= 115
    ```
1. On average, each post is accessed 20 times a day
    ```
    Created posts for 1 year = 10 000 000 * 365 / 7 ~= 1e9
    Maximum RPS = 1e9 * 20 / 86400 ~= 250k
    ```
1. On average, each post contains 5 photos
    ```
    Maximum RPS = 250k * 5 = 1250k
    ```
1. Each user create/update/delete 1 geo tag per week
    ```
    Maximum RPS = 10 000 000 / 86 400 / 7 ~= 17
    ```
1. On average, each post contains 1 geo tag
    ```
    Created posts for 1 year = 10 000 000 * 365 / 7 ~= 1e9
    Maximum RPS = 1e9 * 20 / 86400 ~= 250k
    ```
