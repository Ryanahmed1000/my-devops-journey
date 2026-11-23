# Troubleshooting: Docker permission denied

## Key Concepts

- Commands, flags and placeholders

## Commands

- `docker run hello-world` - command that shows docker instillation is working correctly.
- ` ls -l /var/run/docker.sock` - shows who  owns this specific file
- `groups` - shows which groups a users is in.
- `$USER` - placeholder gives back who the account belongs to.
- `-G` - flag refers to creating a new list of supplementary groups.
- `-a` - flag to append, adds a user to the end of whats already existing. 
- `-aG` - A flag, two combined adds a group to the end of the users existing groups
- `-G docker` - A flag -G on its own with docker would replace the users exsisting groups with docker. Especially bad, if the user is a part of sudo group. Sudo being admin.
- `usermod --help` - provides a list of commands
- `man usermod` - full manual of commands

## Examples

- sudo usermod -aG docker $USER
`sudo` runs it as admin, `usermod` changes a user, `-aG docker` adds docker to the list of extra groups, `$USER` fills in with the username automatically.  


## What I Learned

When i would enter `docker run hello-world` in Ubuntu, i would get an error message "permission denied while trying to connect to the docker API at unix:///var/run/docker.sock". I then used `ls -l /var/run/docker.sock` to find out who owns this file and what groups can use it. 

I recieved the response `srw-rw---- 1 root docker 0 Nov 22 19:24 /var/run/docker.sock`. `srw-rw----` - represents premissions - first `rw-`is the owner (root). 
second `rw-` is the group (docker).
final --- is everyone else, who get nothing.

This gave back that docker is the group required for access. I then used `groups` to find out which groups my user is a part of and docker was not present. This explained why my permission was denied.

I then searched on google the speciifc command required to add a user to a group. I found `sudo usermod -aG docker $USER`. 

I then used `usermod --help` to figure out what `-a` and `-G` do on their own and the importance of using them together. 

After using the complete command, I was able to add my user to the neccessary group and after relauching it, I was succefully able to use the command hello world and establish a connection to the file. 

 ## Review questions

 - What would have happened if I used `-G` on its own and replaced my sudo gorup?
 - How would i correct that?
 - What is a practical solution to avoid such an easy mistake in the future?