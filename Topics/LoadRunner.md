# LoadRunner Interview Questions

# Source: https://www.softwaretestinghelp.com/loadrunner-interview-questions-and-best-answers/


A few basic pointers before we begin:

1. LoadRunner interview questions can be categorized into 3 main types – Scripting, Execution, and Analysis. It is important for beginners to focus more on the scripting part.

2. Http/HTML is mostly used protocol, for a start try to perfect this protocol.

3. Be sure to know the exact version of LoadRunner that you worked on. In case of work experience with a previous version, try to keep yourself updated with the features that are part of the newer/current versions.

4. Performance Testing interviews are more practical than they used to be. Scenario oriented questions are common rather than straightforward ones. Some companies, even make scripting tests a part of the interview process. So, be prepared for the same.

5. Even in scripting, it is preferred that you be able to customize code, instead of just record and replay.

6. Expect questions on – think time, transactions, comments, recording options, runtime settings, etc. – these are to test your knowledge of scripting best practices.


The following are some of the performance testing interview questions that will need some experience to answer. Try to keep these questions in mind while working on your performance test projects, so the interview preparation activity becomes a continuous process.

What are the different scripting issues you faced so far?

What are the performance bottlenecks that you found in projects you were working? What are the recommendations made to overcome those issues?

Have you applied Little's law in your project? If so, how?

What is your approach for analysis?

What do you monitor while execution?

How to extract server data for test execution and how to analyze that?

How to identify performance bottlenecks?

Key question areas are:

Challenges that you face during scripting

Correlation function

Error handling

Different recording modes for Web HTTP/HTML protocol.

Scenario creation

Challenges during execution

## Analysis

Below we provided few common LoadRunner interview questions and answers to them. However, please note that the best results can be achieved by providing answers based on your exposure, expertise and interpretation of the concepts. Learning just the answers to questions is not always optimum. Practice, Learn and Expert – this should be your approach for performance testing interview preparation.

LoadRunner Interview Questions and Best Answers

1. What is the difference between Performance testing and Performance engineering?

Ans => In Performance testing, testing cycle includes requirement gathering, scripting, execution, result sharing and report generation. Performance Engineering is a step ahead of Performance testing where after execution; results are analyzed with the aim to find the performance bottlenecks and the solution is provided to resolve the identified issues.

2. Explain Performance Testing Life Cycle.

Ans => Step 1: System Analysis (Identification of critical transaction)

Virtual User Generator

Step 2: Creating Virtual User Scripts (Recording)

Step 3: Defining Users Behavior (Runtime setting)
LoadRunner Controller

Step 4: Creating Load Test Scenarios

Step 5: Running the Load Test Scenarios and Monitoring the Performance
LoadRunner Analysis

Step 6: Analyzing the Results

Refer Performance Testing Tutorial #2 for more details.

3. What is Performance testing?

Ans => Performance testing is done to evaluate application`s performance under load and stress conditions. It is generally measured in terms of response time of user’s action on an application.

4. What is Load testing?

Ans => Load testing is to determine if an application can work well with the heavy usage resulting from a large number of users using it simultaneously. The load is increased to simulates the peak load that the servers are going to take during maximum usage periods.

5. What are the different components of LoadRunner?

Ans => The major components of LoadRunner are:
VUGen- Records Vuser scripts that emulate the actions of real users.
Controller – Administrative center for creating, maintaining and executing load test scenarios. Assigns scenarios to Vusers and load generators, starts and stops loading tests.
Load Generator – An agent through which we can generate load
Analysis – Provides graphs and reports that summarize the system performance

6. What is the Rendezvous point?

Ans => Rendezvous point helps in emulating heavy user load (request) on the server. This instructs Vusers to act simultaneously. When the vuser reaches the Rendezvous point, it waits for all Vusers with Rendezvous point. Once designated numbers of Vusers reaches it, the Vusers are released. Function lr_rendezvous is used to create the Rendezvous point. This can be inserted by:

Rendezvous button on the floating Recording toolbar while recording.

After recording Rendezvous point is inserted through Insert> Rendezvous.

7. What are the different sections of the script? In what sequence do these sections run?

Ans => LoadRunner script has three sections vuser_init, Action and vuser_end.
vuser_init has requests/actions to login to the application/server.
Action has actual code to test the functionality of the application. This can be played many times in iterations.

Vuser_end has requests/actions to login out the application/server.
The sequence in which these sections get executed is vuser_init is at the very beginning and vuser_end at the very end. The action is executed in between the two.

8. How do you identify which protocol to use for any application?

Ans => Previously Performance tester had to depend much on the development team to know about the protocol that application is using to interact with the server. Sometimes, it also used to be speculative.
However, LoadRunner provides a great help in form of Protocol Advisor from version 9.5 onwards. Protocol advisor detects the protocols that application uses and suggest us the possible protocols in which script can be created to simulate the real user.

9. What is a correlation? Explain the difference between automatic correlation and manual correlation?

Ans => Correlation is used to handle the dynamic values in a script. The dynamic value could change for each user action (value changes when action is replayed by the same user) or for different users (value changes when action is replayed with a different user). In both, the cases correlation takes care of these values and prevents them from failing during execution.

Manual Correlation involves identifying the dynamic value, finding the first occurrence of dynamic value, identifying the unique boundaries of capturing the dynamic value, writing correlation function web_reg_save_param before the request having the first occurrence of dynamic value in its response.

Automated correlation works on predefined correlation rules. The script is played back and scanned for autocorrelation on failing. Vugen identifies the place wherever the correlation rules work and correlate the value on approval.

Refer this tutorial for more details.

10. How to identify what to correlate and what to parameterize?

Ans => Any value in the script that changes on each iteration or with the different user while replaying needs correlation. Any user input while recording should be parametrized.

11. What is parameterization & why is parameterization necessary in the script?
Ans => Replacing hard-coded values within the script with a parameter is called Parameterization. This helps a single virtual user (vuser) to use different data on each run. This simulates real-life usage of an application as it avoids server from caching results.

Refer this tutorial for more details.

12. How you identify Performance test use cases of any application?

Ans => Test cases/Uses cases for Performance test are almost same as any manual/functional testing test cases where each and every step performed by the user is written. The only difference is that all manual test cases can’t be Performance testing use cases as there are few criteria for the selection as:

I. The user activity should be related to the critical and most important functionality of the application.
II. The user activity should be having a good amount of database activity such as search, delete or insert.
III. The user activity should be having good user volume. The functionality having less user activity is generally omitted from Performance testing point of view. e.g admin account activity.

Any of the manual test cases that fulfil the above criteria can be used as performance testing use case/test case. If manual test cases are not written step by step, Performance team should create dedicated documents for them.
