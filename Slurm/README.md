# Slurm
Slurm is a "workload manager" commonly used by Linux compute clusters.
It acts as a middleman between users and the compute power of the cluster.
As a user, you "tell" Slurm what you want to do and how many resources it will take.
Slurm then manages all the requests and gives access to the resources when they're available.

This document will give a high-level overview of the most common tasks you may want to do in Slurm.

## Terminology and Definitions
Here is some terminology used by Slurm and the definitions for these terms.
Note: there are a number of terms that are defined differently for Slurm than they are elsewhere.
For example, the way Slurm defines "CPU" is different from the standard definition of "CPU".
Keep this in mind, as it can be a source of confusion.

Here are some commonly used terms and their definitions in the context of Slurm.
These terms are organized so a new user can read them top-down to get an idea of how Slurm works, not in alphabetical order.
To reiterate: these terms may be defined differently in other contexts.

* __Resource__
  * A resource in Slurm is anything that is being tracked and shared by the users of the cluster.
  * This includes physical resources, such as nodes, CPUs, GPUs, and RAM.
  * Time is also considered to be a resource.
* __Node__
  * A single computer within the cluster.
  * Each node contains some number of CPUs and GPUs, plus some amount of RAM.
  * A cluster is made up of several nodes, each of which may have different amounts of these.
    * Typically, the administrators will buy multiple of the same computer, meaning there will be several nodes each with the same amount of resources. Usually, these systems are given similar names with different numbers, such as "node001" and "node002".
    * Sometimes, there are special systems that have different kinds of resources (e.g., more RAM). Usually, the name will indicate if a node is special, such as "mnode001" or "gnode001".
* __CPU__
  * A single processing unit available to perform computations.
  * In standard terms, this refers to a single logical CPU core.
  * For example:
    * Consider a computer which has 8 hyperthreaded performance cores and 4 non-hyperthreaded efficiency cores.
    * The performance cores each have 2 logical cores, while the efficiency cores only have 1.
    * This gives us $(8 \times 2) + (4 \times 1) = 20$ logical cores.
    * Slurm would report this system as having 20 CPUs.
  * When allocating resources, you can also think of this as the total number of processes and threads running (Slurm doesn't distinguish between the two, or even use those terms).
    * For example, suppose you have a job that starts 2 processes, and each process uses 4 threads. This means there are 8 threads running at once, so you need to request 8 CPUs.
    * Example 2:suppose you have a job that starts 2 processes, and each process creates a single child process. This is a total of 4 processes. If each process then uses 5 threads, there are 20 threads running at once, so you need to request 20 CPUs.
* __GPU__
  * A single graphics processing unit available to perform computations.
  * Unlike the "CPU" term, this does _not_ divide out each processor within the GPU.
  * Often, this will refer to an entire graphics processor as a whole.
    * For example, "1 GPU" may refer to an entier NVIDIA A100 GPU.
  * Sometimes, using NVIDIA's "multi-instance GPU" (MIG) technology, the administrators of a cluster may divide a single graphics processor into several "virtual" graphics processors. Slurm would refer to each of these as individual GPUs.
    * As of August 2024, this is not used on Riviera, but is worth noting as it may be used on other clusters.
    * For example, suppose the administrator divided a single NVIDIA A100 GPU into 2 virutual GPUs, each with half of the processing power and memory. Slurm would report this as being 2 GPUs.
* __RAM (Memory)__
  * RAM, or "random access memory", or just "memory", is the typical definition.
* __Job__
  * When you ask Slurm for resources to do some piece of work, Slurm refers to this as a "job". Each time you ask for resources, that is a separate job.
  * Each job has a unique ID number to identify it with.
  * A job is typically started using the `sbatch` command.
  * The resources you requeseted will be reserved for the entire time the job is running, even if you don't need all of them the whole time.
* __Job Step__
  * A job can be broken up into several different pieces of work, called "job steps" (or just "steps").
  * A job step is typically started using the `srun` command inside an `sbatch` script.
  * All job steps are defined by a program (or terminal command) that you want run.
  * Optionally, you can indicate the step only requires some of the resources requested by the job it's in.
    * This can be helpful if you want multiple steps to run at the same time, as the total number of resources you're using at once cannot exceed what you requested for the job.
  * You can write the steps so they can run one at a time, in parallel, or some combination thereof.
* __Task__
  * A job step can be further broken up into several "tasks".
  * When a job step starts, all of the tasks are started simultaneously and run in parallel.
  * When they start, each task will run the program (or command) you specified in the job step.
  * For example, if you have a job step that runs `python myscript.py` and has 4 tasks, then the `myscript.py` script will be run 4 times (all in parallel).
    * Furthermore, if the job step is given 8 CPUs, then each instance of the script can use 2 threads or processes.
* __Rank__
  * When a job step has multiple tasks, each task is given a "rank" number starting from 0 and counting up.
    * For example, if my job step has 4 tasks, then the tasks will be given a rank of 0, 1, 2, or 3.
  * When a program uses this, it often wants to do something slightly different for different tasks.
    * For example, if you have a large dataset to process, you may have each task process a distinct subset of the data. You would then use the taks's rank to determine which subset to process.
  * Sometimes, one of the tasks will be considered a "leader" (a.k.a. "main" or "master"). The standard convention is that this is the task with rank 0, as there will always be a rank 0.
  * If your job step uses multiple nodes, and each node is running multiple tasks, then the tasks on each node are given a second "local rank", which is the same idea but only counts the tasks on the same node.
    * For example, you may have 8 tasks split evenly across 2 nodes. These 8 tasks would have a "rank" between 0 to 7 inclusive, and each would be unique for your job step. However, the tasks would have a "local rank" between 0 and 3 inclusive, which would be unique per node, but not globally.
* __Partition (Job Queue)__
  * A "partition", also called a "job queue", is a way for Slurm to organize the jobs that users submitted and decide which ones to do next.
  * Typically, a partition only has access to a specific set of resources available.
    * For example, many clusters have separate partitions for jobs that require GPUs versus jobs that only need CPUs. The GPU partition can only use nodes which have GPUs available, while the CPU partition might be set up to only use the nodes which do not have GPUs attached.
  * Additionally, a partition may impose limits on how many resources you can request at once.
    * For example, there may be a partition which limits your jobs to be 1 hour or less, or there may be a partition which limits your jobs to a maximum of 4 CPUs.
  * Unlike mathematics, partitions are not disjoint. That is, a specific resource may be part of several partitions.
    * For example, there may be different partitions for the same compute resources, but with different time limits (e.g., 1 hour vs. 1 day).
  * When Slurm is deciding what job to run next, certain partitions may be prioritized over others.
* __Account__
  * As of August 2024, Riviera does not use accounts.
  * Sometimes, the administrators want to track the resources being used by a group of people, or for a specific project.
  * In this case, they would set up an "account" for this, and you would specify that account when submitting your job.
    * Note: this is _not_ a user account. Instead, it works more like a bookkeeping account.
