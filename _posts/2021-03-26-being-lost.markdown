---
hero_image: https://northslopechillers.com/wp-content/uploads/2019/07/Cool-Server-Room.jpg
---

## Diagrams and How They Can Go Wrong

When attempting to set up the SSH Bastion for Project 0, there was an issue: I was totally lost and the diagram that was initially put forth didn't reflect where an SSH bastion would belong relative to the subnet it belonged to.

Originally, the SSH Bastion wasn't attached to a subnet at all, and wasn't considered an EC2 instance. We would have to "log in" to the SSH Basion, then be forwarded into a private subnet. That didn't make sense.

## Mistakes Were Made

Confusedly trudging ahead, after setting up the SSH Bastion, a second EC2 instance was launched. SSH'ing into this instance from the SSH bastion was difficult because of how a user's private key wouldn't reach to the instance server's public key. The public key was SCP'd into the instance, but then it required using SSH-agent to attempt to access this.

All this because I didn't look into the options built into AWS and managing policies better. I have a lot to learn.