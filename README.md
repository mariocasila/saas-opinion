# Opinion about Scalability and Robust


I know these days we always talk about building scalable and robust platforms. So, how can we achieve a scalable and robust backend system? Here are my thoughts based on my experience developing a successful online SaaS platform.

1) Scalable

   What does scalable mean? Let's say your platform becomes very popular, attracting many users. For example, you might have 10,000 concurrent users.
   Will your server be able to handle that? Definitely not. In this case, we need to scale the server horizontally. However, there is a problem: when we have multiple servers, we face session inconsistency for WebSocket connections and unnecessary duplicated process execution.
   Let's discuss unnecessary duplicated process execution. Suppose you have a cron job function in your codebase that performs operations involving database access. If you have two servers running and scaled up, then, traditionally, 2X database accesses may occur, which is inefficient.
   Then how to resolve this issue? We need to implement microservices to handle such jobs in a shared manner, possibly using a queueing system or dedicated service.
   In other words, from the beginning of development, we need to consider scalability in our codebase. Let's assume your system is going to pull real-time data from third parties.

   We shouldn't use await to fetch data; instead, we should process data in a callback function because waiting for data retrieval can be too expensive. Additionally, we should avoid processing data directly into the database, as doing so can lead to database freezing if multiple concurrent responses occur.

   In this case, it would be better to use a RabbitMQ producer/consumer model (or pub/sub) to process those responses periodically without putting too much burden on the system. This approach is also an effective way to improve scalability.
  
2) Robust

   All companies, even start up companies always propose robust, robust, robust.
   But can robust implement easily? I think NO.
   Let me list 2 simple and significant examples. 
   The company who developed real estate SaaS platform ( which I joined ) invested 3 million dollars ( heard from CEO ) in a few years. but it didn't succeed. during development for 1 year, I always thought why this company had not succeeded yet though every developer worked so hard and add many new features day by day.
   I didn't join this company from the first time, but when I joined and reviewed the codebase, I was a little bit surprised. there was no test case in codebase, even unit test.
   if we didn't implement test code, at the first time, development speed seemed fast. but as the time went by and platform began to complex and specification changed, so many issues happened.
   Though developers consider many of the cases while developing new features, they can't consider all, espcially some parts he was not involved in.
   It results in refactoring of codebase repeatedly.
   How nice it will be if there are unit tests? before raising PR, on local, developers can run unit test, if failed, they can find what the issue is and fix.
   

   Moreover, running tests don't pass by, CI/CD pipeline has to reject merging PR to main branch.
   Another thing I want to mention is QA.
   QA needs to know about all acceptance criteria. 
   we can say, coding is the very detailed specification. The person who knows the best about the specification for a specific part is the programmer who developed that functionality.
   But unfortunately QA doesn't know all, even don't know what to test sometimes, especially in remote company. 
   In my previous company, 2 QAs always test new features and do regression test. but they didn't find some important issues which was found by CEO.
   Why did this happen? 
   Of course they will be many factors, but one of them is we missed grooming call for each functionality.
   before getting into development of new feature, everyone related to this functionality know about why we develop this feature, what goal we acheive, what will be the edge case and etc.
   We must derive as much as possible.
   And everyone has to think how I can implement this feature.
   I am a software engineer, so I have to think what techs I have to use and what structure will be best to acheive scalability and robust.
   if you are a QA, you have to think what cases I have to test, what will be the edge case from the users' perspective.
   If we keep these 2 things above at least, there will be many improvement of platform.

   In conclusion, Unit test & grooming call are significant though development speed is a bit slow.

   Finally these are the things I focus on for scalability and robust.

   To create an optimized and scalable backend service, I focus on the following strategies:

    - Create a cacheable system.
    - Optimize database queries.
    - Use async/await for non-blocking code execution.
    - Enable compression to reduce load times.
    - Implement rate limiting to manage API usage.
    - Create microservices using technologies like Kafka, RabbitMQ.
    - For database optimization, I prioritize query processing speed and regularly examine performance using tools such as EXPLAIN ANALYZE during development.

If you agree with my opinion, please give me stars.
Thanks for reading and give me your feedback about my opinion.
