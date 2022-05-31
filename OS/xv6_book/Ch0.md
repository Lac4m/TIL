# Chapter 0

## Operating System Interfaces

xv6 takes traditional form of a <b>kernel</b>, a special program that provides services to running programs (process).

Process has memory containing instructions, data, and a stack. Instructions implement the program's computations. Data are the variables on which the computation acts. The stack organizes the program's procedure calls.

When process needs to invoke kernel service, it invokes a procedure call in the OS interface called system calls. The system call enters the kernel, the kernel performs the service and returns. Thus a process alternates between executing in user space and kernel space.

<img src="https://clownote.github.io/2021/02/27/xv6/Xv6-operating-system-organization/Xv6-operating-system-organization/kernel.png" width="400px">

<br>

| System call               | Description                              |
|---------------------------|------------------------------------------|
| fork()                    | create process                           |
| exit()                    | terminate current process                |
| wait()                    | wait for child process to exit           |
| kill(pid)                 | terminate process pid                    |
| getpid()                  | return current process's id              |
| sleep(n)                  | sleep for n seconds                      |
| exec(filename, flags)     | open a file; flag indicate read/write    |
| sbrk(n)                   | grow process's memory by n bytes         |
| open(filename, flags)     | open a file; flag indicate read/write    |
| read(fd, buf, n)          | read n bytes from an open file into buf  |
| write(fd, buf, n)         | write n bytes to an open file            |
| close(fd)                 | release open file fd                     | 
| dup(fd)                   | duplicate fd                             |
| pipe(p)                   | create a pipe and return fd's in p       |
| chdir(dirname)            | change the current directory             |
| mkdir(dirname)            | create a new directory                   |
| mknod(name, major, minor) | create a device file                     |
| fstat(fd)                 | return info about an open file           |
| link(f1, f2)              | create another name (f2) for the file f1 |
| unlink(filename)          | remove a file                            |

The shell is an ordinary program that reads commands from the user and executes them, and is the primary UI to traditional Unix-like systems.

## Processes and Memory

An xv6 process consists of user-space memory and per-process state private to the kernel.

A process may create a new process using <b>fork</b> syscall. Fork creates a new process called child process, with exactly the same memory contents as the calling process (parent process). Fork returns in both parent and child. In parent, fork returns child pid, in child returns zero.

```C
int pid;

pid = fork();
if(pid > 0){
    printf("parent: child=%d\n", pid);
    pid = wait();
    printf("child %d is done\n", pid);
} else if(pid == 0){
    printf("child: exiting\n");
    exit();
} else {
    printf("fork error\n");
}
```

The exit system call causes the calling process to stop executing and to release resources such as memory and open files. The wait system call returns the pid of an exited child of the current process; if none of the caller’s children has exited, wait() waits for one to do so.

output:

```C
parent: child=1234
child: exiting
parent: child 1234 is done
```

The exec system call replaces the calling process’s memory with a new memory
image loaded from a file stored in the file system. The file must have a particular format, which specifies which part of the file holds instructions, which part is data, at which instruction to start, etc. 

When exec succeeds, it does not return to the calling program; instead,
the instructions loaded from the file start executing at the entry point declared in the ELF header.

Exec takes two arguments: the name of the file containing the executable
and an array of string arguments.

char *argv[3];
argv[0] = "echo";
argv[1] = "hello";
argv[2] = 0;
exec("/bin/echo", argv);
printf("exec error\n");