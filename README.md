Download Link: https://assignmentchef.com/product/solved-cs304-assignment-1
<br>
<span class="kksr-muted">Rate this product</span>

In this assignment, you will run a few simple commands on the Linux shell to understand the basics of operating systems. In each of the exercises below, you will be expected to run a com- mand, observe some output and report it. Please note down the answers to all questions in a report. In addition to the final answer, you must also state the commands or tools you used to arrive at your answer. The following helper files are provided to you: cpu.c,cpu-print.c,disk.c,disk1.c,foo.pdf,make-copies.sh,memory1.c, and memory2.c. Before you begin

<ul>

 <li>FamiliarizeyourselfwiththecommontoolsonLinuxliketopandpsthatareusedtomonitor processes running in the system. Understand the most useful and common command line options to use with these commands.</li>

 <li>Understand the/proc filesystem in Linux. The /procfile system is a mechanism provided by Linux for the kernel to report information about the system and processes to users. The/proc file system is nicely documented in the /proc man page. You can access this document by running the command man proc on a Linux system. Understand the system- wide /proc files such as meminfo and cpuinfo, and per-process files such as status, stat, limits, and maps.Questions1. Byansweringthisquestion,youwillunderstandthehardwareconfigurationofyourworking machine using the/procfilesystem.

  <ol>

   <li>(a)  Run command more /proc/cpuinfo and explain the following terms: processor and cores.[Hint: Use lscpu to verify your definitions.]</li>

   <li>(b)  How many cores does your machine have?</li>

   <li>(c)  How many processors does your machine have?</li>

   <li>(d)  What is the frequency of each processor?</li>

   <li>(e)  How much physical memory does your system have ?</li>

   <li>(f)  How much of this memory is free ?</li>

   <li>(g)  What is total number of number of forks since the boot in the system ?</li>

   <li>(h)  How many context switches has the system performed since bootup ?</li>

  </ol>2. In this question, you will understand how to monitor the status of a running process using the top command. Compile the program cpu.c given to you and execute it in the bash or</li>

</ul>




any other shell of your choice as follows.

$ gcc cpu.c -o cpu$ ./cpuThis program runs in an infinite loop without terminating. Now open another terminal, run the top command and answer the following questions about the cpu process.

<ol>

 <li>(a)  What is the PID of the process running the cpu command?</li>

 <li>(b)  How much CPU and memory does this process consume?</li>

 <li>(c)  What is the current state of the process? For example, is it running or in a blocked state or a zombie state?</li>

</ol>

3. In this question, you will understand how the Linux shell (e.g., the bash shell) runs user commands by spawning new child processes to execute the various commands. Compile the program cpu-print.c given to you and execute it in the bash or any other shell of your choice as follows.

<pre>   $ gcc cpu-print.c -o cpu-print   $ ./cpu-print</pre>

<ol>

 <li>(a)  This program runs in an infinite loop printing output to the screen.Now, open another terminal and use the ps command with suitable options to find out the pid of the process spawned by the shell to run the cpu-print executable. You may want to explore the ps command thoroughly to understand the various output fields it shows.</li>

 <li>(b)  Find the PID of the parent of the cpu-print process, i.e., the shell process. Next, find the PIDs of all the ancestors, going back at least 5 generations (or until you reach the init process).</li>

 <li>(c)  To understand how the shell performs output redirection. Run the following com- mand../cpu-print &gt; /tmp/tmp.txt &amp;Look at the proc file system information of the newly spawned process. Pay particu- lar attention to where its file descriptors 0, 1, and 2 (standard input, output, and error) are pointing to. Using this information, can you describe how I/O redirection is being implemented by the shell?</li>

 <li>(d)  To understand how the shell implements pipes. Run the following command.<pre>       ./cpu-print | grep hello &amp;</pre>Once again, identify the newly spawned processes, and find out where their standard input/output/error file descriptors are pointing to. Use this information to explain how pipes are implemented by the shell.</li>

 <li>(e)  When you type in a command into the shell, the shell does one of two things. For some commands, executables that perform that functionality already come built into the Linux kernel.For such commands, the shell simply invokes the executable like it runs the executables of your own programs. For other commands where the exe- cutable does not exist, the shell implements the command itself within its code. Con-</li>

</ol>




sider the following commands that you can type in the bash shell: cd,ls,history,ps. Which of these commands already exist as built-in executables in the Linux kernel that are then simply executed by the bash shell, and which are implemented by the bash code itself?

<ol start="4">

 <li>Consider the two programs memory1.c and memory2.c given to you. Compile and run them one after the other. Both programs allocate a large array in memory. One of them accesses the array and the other doesn’t. Both programs pause before exiting to let you inspect their memory usage. You can inspect the memory used by a process with the ps command. In particular, the output will tell you what the total size of the “virtual” memory of the process is, and how much of this is actually physically resident in memory. You will learn later that the virtual memory of the process is the memory the process thinks it has, while the OS only allocates a subset of this memory physically in RAM.Compare the virtual and physical memory usage of both programs, and explain your ob- servations.You can also inspect the code to understand your observations.</li>

 <li>In this question, you will compile and run the programs disk.c and disk1.c given to you. These programs read a large number of files from disk, and you must first create these files as follows. Create a folder disk-files and place the file foo.pdf in that folder. Then use the script make-copies.sh to make 5000 copies of the same file in that folder, with different filenames. The disk programs will read these files. Now, run the disk programs one after the other.For each program, measure the utilization of the disk while the program is running. Report and explain your observations. You will find a tool like iostat useful for measuring disk utilization. Also read through the code of the programs to help explain your observations.Note that for this exercise to work correctly, you must be reading from a directory on the local disk.If your disk-files directory is not on a local disk (but, say, mounted via NFS), then you must alter the location of the files in the code provided to you to enable reading from a local disk. Also, modern operating systems store recently read files in a cache in memory (called disk buffer cache)for faster access to the same files in the future. In order to ensure that you are making observations while actually reading from disk, you must clear your disk buffer cache between multiple runs of disk.c. If you do not clear the disk buffer cache between successive runs of disk.c, you will be reading the files not from disk but from memory. Look up online for commands on how to clear your disk buffer cache, and note that you will need superuser permissions to execute these commands.</li>

</ol>