# Top 10 Frequent Words — Naive vs Multiprocessing vs Multithreading

A C project. It finds the top 10 most frequent words in a large text dataset (enwik8) and compares the performance of three approaches: single-process, multiprocessing, and multithreading.

## How It Was Made

Written in C. All three approaches split the work of reading and counting words from the input file, then sort the results by frequency using `qsort`. The multiprocessing version uses `fork()`, shared memory (`shmget`/`shmat`), and a named semaphore for synchronization. The multithreading version uses `pthread_create`/`pthread_join` with a named semaphore to protect shared frequency updates. In both parallel versions, the input file is split into equal chunks distributed across workers, and the results are merged at the end.

## Files

- `main1.c` — naive single-process approach
- `main2.c` — multiprocessing approach using `fork()` and shared memory
- `main3.c` — multithreading approach using `pthreads`

## Features

- Reads and counts word frequencies from a large text file
- Prints the top 10 most frequent words with their counts
- Reports execution time for each approach
- Parallel versions support a configurable number of workers (tested with 2, 4, 6, 8)
- Semaphore-based synchronization to prevent race conditions on shared data
- Temporary chunk files are cleaned up automatically after execution
