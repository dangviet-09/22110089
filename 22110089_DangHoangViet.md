# Untitled

```markdown
# Lab #1,22110089, Dang Hoang Viet, INSE331280E_02FIE
# Task 1: Software buffer overflow attack
**Question 1**: 
##1. Compile asm program and C program to executable code. 
###1.1 Compile the Assembly Shellcode
We need to compile the shellcode into an object file and then create an executable binary.
[View Image](https://imgur.com/a/phdjEHx)
```

![image.png](image.png)

```markdown
###1.2 Compile the Vulnerable C Program
The C program needs to be compiled with the -m32 flag to make it compatible with the 32-bit shellcode.
[View Image](https://imgur.com/XfXkCkw)
```

![image.png](image%201.png)

```markdown
##2. Create the Shellcode Payload
In this step, we will extract the shellcode from the assembly file and convert it into a format that can be injected into the vulnerable C program.
###2.1. Extract Shellcode in Hex Format
We can extract the shellcode using the following command:
This will give us the hex representation of the shellcode, which can be injected into the vulnerable program.
[View Image](https://https://imgur.com/ZOSfENL)
```

![image.png](image%202.png)

```markdown
###2.2. Craft the Exploit
The vulnerable C program uses strcpy() to copy user input directly into a fixed-size buffer, making it susceptible to a buffer overflow attack. We will provide input that overwrites the return address on the stack with the address of the buffer, where our shellcode will reside.
We can use Python to generate the payload for the exploit:
"A" * 16: Fills the buffer completely.
"B" * 4: Overwrites the saved return pointer.
"\x90" * 100: Adds a NOP sled to increase the chances of hitting the shellcode.
"<shellcode>": The extracted shellcode in hex format.

```

![image.png](image%203.png)

```markdown
###2.3. Find the return address
We need to determine the address of the buffer to overwrite the return pointer. This can be done by running the program under gdb and checking the stack layout.

```

![image.png](image%204.png)

![image.png](image%205.png)

![image.png](image%206.png)

```markdown
##3. Conduct the attack
Now that we have the exploit payload, we will run the vulnerable program with this payload to trigger the shellcode and add a new entry to /etc/hosts.

```

![image.png](image%207.png)

```markdown
##4. Verify the attack
After running the exploit, we can verify whether the new entry was successfully added to the /etc/hosts file.

```

![image.png](image%208.png)