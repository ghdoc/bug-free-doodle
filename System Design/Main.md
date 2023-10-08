**System Design**

- [https://github.com/donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer)
- [https://github.com/checkcheckzz/system-design-interview](https://github.com/checkcheckzz/system-design-interview)
- Grokking the System Design Interview

- System Design Interviews: A step by step guide

- Step 1: Requirements clarifications

- Clarify scope, ambiguities
- In a 30-45 minute interview, we should clarify what parts of the system we will be focusing on.
- Eg: Design Twitter like service

- User Features

- Will users of our service be able to post tweets and follow other people?
- Will users be able to search tweets?
- Do we need to display hot trending topics?
- Will there be any push notification for new (or important) tweets?

- UI/UX

- Should we also design to create and display the user’s timeline?

- Content

- Will tweets contain photos and videos?

- System

- Are we focusing on the backend only, or are we developing the front-end too?

- Step 2: Back-of-the-envelope estimation

- Estimating the scale of problem will help design the system.
- Estimating this helps later when we focus on scaling, partitioning, load balancing and caching
- What **scale** is expected from the system (e.g., number of new tweets, number of tweet views, number of timeline generations per sec., etc.)?
- How much **storage** will we need? We will have different storage requirements if users can have photos and videos in their tweets.
- What **network** bandwidth usage are we expecting? This will be crucial in deciding how we will manage traffic and balance load between servers.

- Step 3: System interface definition (API contracts)

-  This will establish the exact contract expected from the system and ensure if we haven’t gotten any requirements wrong
- postTweet(user_id, tweet_data, tweet_location, user_location, timestamp, …)
- generateTimeline(user_id, current_time, user_location, …)
- markTweetFavorite(user_id, tweet_id, timestamp, …)

- Step 4: Defining data model

- This will clarify how data will flow between different system components.
- This will also guide data partitioning and management
- Identify various entities of the system, how they will interact with each other, and different aspects of data management like storage, transportation, encryption, etc.
- Here are some entities for our Twitter-like service:

- User: UserID, Name, Email, DoB, CreationData, LastLogin, etc.
- Tweet: TweetID, Content, TweetLocation, NumberOfLikes, TimeStamp, etc.
- UserFollow: UserID1, UserID2
- FavoriteTweets: UserID, TweetID, TimeStamp
- Database: Will NoSQL like [Cassandra](https://en.wikipedia.org/wiki/Apache_Cassandra) best fit our needs, or should we use a MySQL-like solution? What kind of block storage should we use to store photos and videos?

- Step 5: High level design

- Draw a block diagram with 5-6 boxes representing the core components of our system. We should identify enough components that are needed to solve the actual problem from end-to-end.

- For Twitter, at a high level, we need:

- Multiple Application Servers  
    Read Write requests
- Load Balancers in front of App Servers  
    to distribute traffic
- If no. of read requests are more than write, then we can decide to have separate servers to handle these scenarios.
- For the backend, we need an efficient database that can store all tweets and support a huge number of reads.
- We also need a distributed file storage system for storing photos and videos.

- Step 6: Detailed design

- Based on feedback, dig deeper into two or three major components;
- Present different approaches, pros and cons and explain why we will prefer one approach over the other.
- Since we will be storing a massive amount of data, how should we partition our data to distribute it to multiple databases? Should we try to store all the data of a user on the same database? What issue could it cause?
- How will we handle hot users who tweet a lot or follow lots of people?
- Since users’ timeline will contain the most recent (and relevant) tweets, should we try to store our data so that it is optimized for scanning the latest tweets?
- How much and at which layer should we introduce cache to speed things up?
- What components need better load balancing?

- Step 7: Identifying and resolving bottlenecks

- Try to discuss as many bottlenecks as possible and different approaches to mitigate them.
- Is there any single point of failure in our system? What are we doing to mitigate it?
- Do we have enough replicas of the data so that we can still serve our users if we lose a few servers?
- Similarly, do we have enough copies of different services running such that a few failures will not cause a total system shutdown?
- How are we monitoring the performance of our service? Do we get alerts whenever critical components fail or their performance degrades?