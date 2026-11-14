📝 MY_WORK: Student Information, Development Log, Reflection & Answers

This is the only file your instructor reads to grade Parts 3 and 4 (documentation and video). Everything you write here must be in your own words.


🛑 STOP: Read This Before You Do Anything Else

1️⃣ Read the whole

README.md

first

The README.md in this repository contains the full instructions for this assignment, including the class descriptions, feature specifications, question prompts, and video requirements.

2️⃣ Understand the full code before answering any question

I reviewed SchedulerSimulationSync.java, including SharedStats, ReadyQueue, CpuWorker, RaceWindow.pause(), ReentrantLock, and Semaphore.

3️⃣ Use only the code of this repository

All implementation work was done in SchedulerSimulationSync.java from this repository.

4️⃣ Commit many times, not once

The implementation was organized into separate commits for the student ID and the three synchronization features.


👤 Student Information

Field
	

Your Answer

Full Name
	

Shahad Alassmi

Student ID
	

445052149

University Email
	

445052149@std.psau.edu.sa

GitHub Username
	

shahadalassmi

Repository Link
	

https://github.com/shahadalassmi/OS-Assignment3-Shahad-Alassmi


🎥 Video Link

Video Link: [Paste your public video link here after uploading]

The video must be publicly accessible. It must be 2–3 minutes long and named 445052149_Assignment3_Demo.mp4.


🗺️ Work Roadmap (follow in this order)

Step
	

What to do
	

Status

0
	

Read README, inspect the code, and run the original starter
	

Completed

1
	

Fork, rename, make the repository public, and set the student ID
	

Completed

2
	

Feature 1: Ready queue lock
	

Completed

3
	

Feature 2: Statistics locks
	

Completed

4
	

Feature 3: Counting semaphore
	

Completed

5
	

Development Log
	

Completed

6
	

Reflection
	

Completed

7
	

Technical Answers
	

Completed

8
	

Record and upload the video
	

Pending

9
	

Final check and submit the repository link
	

Pending


🔁 Commit Rules (MANDATORY)

#
	

Commit
	

Date

1
	

Set personal student ID
	

November 10, 2026

2
	

Feature 1: Protect ReadyQueue with ReentrantLock
	

November 11, 2026

3
	

Feature 2: Protect Shared Statistics with ReentrantLock
	

November 13, 2026

4
	

Feature 3: Replace busy waiting with counting semaphore
	

November 13, 2026

The commits are available in the public repository history.


Part A: Development Log (0.5 mark)

Your Development Log

Entry 1 - November 10, 2026

What I did: Forked and personalized the repository.

Details:

    Forked the original starter repository.
    Renamed my repository to OS-Assignment3-Shahad-Alassmi.
    Set my student ID to 445052149 in SchedulerSimulationSync.java.
    Ran the original starter program and observed synchronization problems.
    Saved the original output for comparison.

Challenges: Understanding why multiple CPU threads could access the shared ready queue at the same time.

Solution: Reviewed the original code and examined how the CPU workers accessed the shared queue and statistics.

Time spent: Approximately 1 hour.


Entry 2 - November 11, 2026

What I did: Implemented Feature 1: Ready Queue Lock.

Details:

    Declared a ReentrantLock in the ReadyQueue class.
    Protected the add() method.
    Protected the poll() method.
    Protected the processOf() method.
    Protected the snapshot() method.
    Used try/finally to ensure the lock is released.

Challenges: Making sure that all accesses to the shared list and map were protected.

Solution: Used the same lock around the critical sections in the four queue methods and released it in the finally block.

Time spent: Approximately 1 hour.


Entry 3 - November 13, 2026

What I did: Implemented Feature 2: Statistics Locks.

Details:

    Declared a ReentrantLock named statsLock in SharedStats.
    Protected updates to contextSwitchCount.
    Protected updates to completedProcessCount.
    Protected updates to totalServiceTime.
    Protected the getter methods because reading shared values also requires synchronization.

Challenges: Understanding why read operations also need protection and deciding how many locks to use.

Solution: Used one lock for the three statistics to keep the implementation simple and ensure that all updates and reads are protected consistently.

Time spent: Approximately 1 hour.


Entry 4 - November 13, 2026

What I did: Implemented Feature 3: Counting Semaphore.

Details:

    Added a counting Semaphore named availableProcesses to ReadyQueue.
    Initialized it with zero permits.
    Used release() when a process is added to the ready queue.
    Added waitForProcess() using acquire().
    Updated the CPU workers to wait for available processes instead of continuously polling an empty queue.
    Added a shutdown signal to wake blocked CPU workers when all processes have completed.

Challenges: Understanding how the semaphore counts available processes and how blocked CPU workers should terminate.

Solution: Used semaphore permits to coordinate the CPU workers with the ready queue. When the last process finishes, the shutdown logic releases permits to wake the waiting CPUs.

Time spent: Approximately 1 hour.


Entry 5 - November 14, 2026

What I did: Tested the completed synchronization implementation and reviewed the assignment.

Details:

    Ran the final program five times.
    Checked the built-in verification output after each run.
    Confirmed that all shared values were consistent in all five runs.
    Reviewed the implementation of the three synchronization features.
    Reviewed the GitHub commit history.

Challenges: Making sure that the statistics remained consistent and that CPU workers terminated correctly after all processes finished.

Solution: Checked the verification output across five consecutive runs and reviewed the semaphore shutdown logic.

Time spent: Approximately 1 hour.


Development Log Summary

Total time spent on assignment: Approximately 5 hours.

Most challenging part:

The most challenging part was understanding how multiple CPU threads access shared data at the same time. I had to understand why protecting only some operations was not enough and why all accesses to the shared queue needed synchronization.

Most interesting learning:

I learned how ReentrantLock provides mutual exclusion and how a counting semaphore coordinates CPU workers without busy waiting.

What I would do differently next time:

I would test each feature immediately after implementing it and save screenshots of the output. I would also review the shutdown behavior carefully before considering the implementation complete.


Part B: Reflection (0.5 mark)

Question 1: What did you learn about synchronization?

Your Answer:

I learned that synchronization is important when multiple threads access shared data at the same time. A race condition can happen when two threads read and update the same variable without proper protection. In this assignment, I used ReentrantLock to protect the ready queue and the shared statistics. I also learned that a lock should be released inside a finally block so another thread can continue even if an exception occurs. The counting semaphore helped me understand how threads can wait until a resource becomes available instead of continuously checking it. I now understand better why mutual exclusion is necessary in concurrent programs.

Question 2: What was the most challenging part of this assignment?

Your Answer:

The most challenging part was understanding how the CPU workers interact with the shared ready queue. Several CPU threads can try to access the queue at almost the same time, which can cause race conditions if the operations are not protected. I also found it challenging to understand the difference between protecting shared statistics and protecting the ready queue. Another difficult part was understanding how the semaphore should be initialized and how CPU workers should terminate when all processes finish. I needed to review the code carefully to understand how the different methods work together. This assignment required me to think about the order of operations between threads rather than only the program output.

Question 3: How did you overcome the challenges you faced?

Your Answer:

I overcame the challenges by working on the assignment one feature at a time. First, I reviewed the original code to understand the ready queue, CPU workers, and shared statistics. Then I implemented the ready queue lock and checked the methods that access the shared list and map. After that, I protected the statistics and worked on replacing busy waiting with a counting semaphore. I used VS Code and the terminal to compile and run the program and inspect the results. Running the final program five times helped me check that the shared values remained consistent.

Question 4: Where can synchronization concepts be applied in real-world applications?

Your Answer:

Synchronization is useful in many real-world applications where multiple users or processes access shared resources. For example, in a banking application, two transactions should not update the same account balance at the same time without protection. In an online ticket booking system, synchronization can prevent two users from booking the same seat. A print queue can also use synchronization to organize requests from multiple computers. In databases, locks help protect shared records while transactions are being processed. These examples are similar to my assignment because multiple threads access shared data and need coordination to avoid inconsistent results.

Optional: What would you like to learn more about?

I would like to learn more about deadlocks, thread scheduling, and the different types of semaphores. I am also interested in understanding how synchronization is implemented in real operating systems.

Optional: How confident do you feel about synchronization concepts now?

Intermediate. I understand the basic purpose of locks, critical sections, and counting semaphores, but I still need more practice with complex concurrency problems and deadlock prevention.

Optional: Feedback on the assignment

The assignment was useful because it connected synchronization concepts from the lectures to a practical Java program. Working with multiple CPU threads helped me understand why synchronization is necessary.


Part C: Technical Answers (0.5 mark)

Question 1: Race Condition in Your Own Output

Your Answer:

In the original starter program, multiple CPU threads could access the shared ready queue without proper mutual exclusion. The RaceWindow.pause() method made it easier to observe the race condition by creating a delay between reading and updating shared data. For example, CPU-1 and CPU-2 could both read the same value of contextSwitchCount before either thread writes its update, causing a lost update. The same bug can happen on a real machine because thread scheduling can interrupt operations even without the artificial pause, which makes race conditions difficult to detect.

Verification block of the original starter:

The original starter run showed synchronization problems, including a NullPointerException and a failed verification result.

Verification block of my final version:

The final implementation was tested five consecutive times. All four verification checks passed in each run, and the program displayed:

ALL shared values are consistent.

Explanation of the timeline:

CPU-1 reads the current value of a shared counter. Before CPU-1 writes the updated value, CPU-2 reads the same old value. CPU-1 writes the incremented value, and then CPU-2 writes the same incremented value. As a result, one update is lost because both threads used the same original value.

Question 2: Critical Sections and Lock Granularity

Your Answer:

I used a ReentrantLock in the ReadyQueue class to protect the shared list and map. The methods add(), poll(), processOf(), and snapshot() use the lock to provide mutual exclusion. In SharedStats, I used one ReentrantLock named statsLock to protect the three shared statistics and their getter methods. Using one lock makes the implementation simpler and ensures that all accesses to these statistics are protected consistently, although independent updates must wait for one another. I used a separate lock for the ready queue because it protects a different shared resource, which avoids unnecessary blocking between queue operations and statistics operations.

Critical sections:

Critical section (variable / method)
	

Lock used
	

Why it needs protection

ReadyQueue.add()
	

lock
	

Protects insertion into the shared list and map

ReadyQueue.poll()
	

lock
	

Protects checking and removing the first queue item

ReadyQueue.processOf()
	

lock
	

Protects access to the shared map

ReadyQueue.snapshot()
	

lock
	

Protects reading the queue and its associated map

incrementContextSwitch()
	

statsLock
	

Prevents lost updates to the context switch counter

incrementCompletedProcess()
	

statsLock
	

Prevents lost updates to the completed process counter

addServiceTime()
	

statsLock
	

Protects updates to the total service time

Statistics getter methods
	

statsLock
	

Protects reading shared values during updates

The default ReentrantLock is not fair, so a waiting thread is not guaranteed to acquire the lock in the exact order it requested it. Therefore, bounded waiting is not guaranteed by the default lock configuration.

Question 3: Busy Waiting vs Semaphore

Your Answer:

In the original starter, CPU workers repeatedly checked the ready queue when it was empty, which is an example of busy waiting. This wastes CPU time because a worker keeps checking even when no process is available. In my implementation, the counting semaphore represents the number of processes available in the ready queue. It starts at zero because the queue is initially empty, and each successful add() operation releases a permit, so after the initial additions it has numProcesses permits. CPU workers call acquire() to wait for an available process, and the last CPU releases totalCPUs permits to wake blocked CPU workers so they can terminate.

Busy-waiting polls in the original starter: [Use the exact number from your saved original run.]

Semaphore initial value: 0

Semaphore value after the initial process additions: numProcesses

Shutdown explanation: The last CPU calls release(totalCPUs) to wake CPU workers that may be blocked in acquire(). Without this shutdown signal, those workers could remain blocked forever after all processes have finished.

Question 4: Classical Problems and Deadlock

Your Answer:

The synchronization structure in this assignment is similar to the Producer-Consumer problem. The main thread initially acts as a producer because it adds processes to the ready queue, while the CPU workers act as consumers because they remove processes and execute them. The CPU workers can also act as producers when they add unfinished processes back to the ready queue. If the queue had a fixed capacity of K, the bounded-buffer solution would use an empty semaphore initialized to K, a full semaphore initialized to 0, and a mutex semaphore initialized to 1. A deadlock could occur if a thread held the queue mutex while waiting for a free slot, while another thread needed the same mutex to remove an item and create space. To prevent this, the mutex should not be held while waiting for a semaphore permit, which breaks the circular-wait condition in that scenario.

Classical problem and roles:

Producer-Consumer problem. The main thread initially produces queue entries, and CPU workers consume them. CPU workers may also produce entries when they re-enqueue unfinished processes.

Semaphores for a bounded queue:

Semaphore
	

Initial value
	

Purpose

empty
	

K
	

Counts available empty slots

full
	

0
	

Counts available items

mutex
	

1
	

Protects the shared buffer

Deadlock scenario and prevention:

A producer could hold the mutex while waiting for an empty slot. If a consumer needs the same mutex to remove an item and create an empty slot, neither thread can proceed. Avoid holding the mutex while waiting for the semaphore to prevent this circular wait.

Summary

Key concepts I understood through these questions:

    Race conditions and lost updates.
    Critical sections and mutual exclusion using ReentrantLock.
    Counting semaphores and the Producer-Consumer problem.

Concepts I need to study more:

    Deadlock prevention and the four necessary conditions.
    Fairness, bounded waiting, and advanced thread coordination.


✅ Final Checklist (complete before submitting)

Repository

    ☑ Repository is PUBLIC.
    ☑ Repository is renamed to OS-Assignment3-Shahad-Alassmi.
    ☑ GitHub account uses the university email.

Code

    ☑ Student ID is set in SchedulerSimulationSync.java.
    ☑ Feature 1: Ready queue lock implemented.
    ☑ Feature 2: Statistics locks implemented.
    ☑ Feature 3: Counting semaphore implemented.
    ☑ Final program passed five consecutive runs according to the verification output.
    ☑ All shared values were consistent in the five runs.
    ☑ Every lock is released in a finally block.
    ☐ Confirm that RaceWindow, Config, the verification block, and the watchdog are unchanged.
    ☐ Confirm that all feature comments are clear.

Commits

    ☑ At least 4 meaningful commits.
    ☑ One commit per feature.
    ☑ Commits are spread over different dates.
    ☑ Changes are pushed to GitHub.

This file (

MY_WORK.md

)

    ☑ Full name and student ID filled in.
    ☑ Development Log has five entries.
    ☑ Reflection has four answers.
    ☑ Technical Answers have four answers.
    ☐ Confirm the original starter’s exact Busy-waiting polls value.
    ☐ Review all answers and make sure you can explain them.
    ☐ No remaining placeholders.
    ☑ Original section headers retained.

Video

    ☐ Video is 2–3 minutes long.
    ☐ Video is named 445052149_Assignment3_Demo.mp4.
    ☐ Shows name, ID, repository, all three features, IDE execution, one synchronization concept, and commit history.
    ☐ Link is public and pasted in the Video Link section above.

Blackboard

    ☐ Submit only the link to the public GitHub repository.




