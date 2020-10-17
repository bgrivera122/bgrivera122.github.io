# The Dockerfile
## A Brief Message

I apolagize for not working on the blog posts. I have always been someone who was
nervous when it cames to things that I get errors with, and the weekly nature of
these blog posts made me feel as if I was too far gone when I fell behind.

However, I would feel worse if I did not try, so I'm happy to have learned howto
post. I was scared by the errors, but seeing the dummy posts work got me excited.
I'll be looking to have a theme be properly working for the next blog posts onwards.

## About That Dockerfile...

The approach I took with the Dockerfile was a simple one; It reminded me of scripting
from previous classes and was surprised at how the RUN commands worked with little
issue.

(first picture up to line 11)

Up until line 11, it was straightforward.

(icture of line 11)

COPY'ing the files that were generated from the previous RUN commands was an obvious
solution that I didn't arrive to until way later. The biggest clue in for using COPY
was the description on the LAB 2 turn-in mentioning to include "other related files"
needed to run the lab.

WORKDIR worked just like "cd." I can imagine it would be painful to keep track of
which directories I need to be in when working on these Dockerfiles, so I hope I
enter a better workflow in the future on realistic projects.

(picture of up till 23)

I thought I had finished after installing composer, but trying to run the dockerfile
without this line resulted in container immediately shutting down. With this, it will
remain open.

Thank you! 