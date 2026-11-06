# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 
```
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main()
{
    int fd1, fd2, n;
    char buffer[100];

    fd1 = open("source.txt", O_RDONLY);

    if (fd1 < 0)
    {
        printf("Error opening source file\n");
        return 1;
    }

    fd2 = open("destination.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);

    while ((n = read(fd1, buffer, sizeof(buffer))) > 0)
    {
        write(fd2, buffer, n);
    }

    printf("File copied successfully\n");

    close(fd1);
    close(fd2);

    return 0;
}
```

## 2.To Write a C program that illustrates files locking
```
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main()
{
    int fd;
    struct flock lock;

    fd = open("lockfile.txt", O_RDWR | O_CREAT, 0644);

    lock.l_type = F_WRLCK;
    lock.l_whence = SEEK_SET;
    lock.l_start = 0;
    lock.l_len = 0;
    lock.l_pid = getpid();

    if (fcntl(fd, F_SETLKW, &lock) == -1)
    {
        printf("Locking failed\n");
        return 1;
    }

    printf("File locked successfully\n");

    sleep(5);

    lock.l_type = F_UNLCK;

    fcntl(fd, F_SETLK, &lock);

    printf("File unlocked successfully\n");

    close(fd);

    return 0;
}

```
## OUTPUT

1.
 <img width="696" height="306" alt="image" src="https://github.com/user-attachments/assets/1733dc2d-b17c-4748-8f6f-31e577c253bb" />


2.
<img width="708" height="170" alt="image" src="https://github.com/user-attachments/assets/0aeba15e-61b8-4818-825e-192c5fa9ed21" />



# RESULT:
The programs are executed successfully.
