# linux - Error connecting to the KeX server (wsl-kali linux)
Save From : [linux - How to fix the error Error connecting to the KeX server? - Stack Overflow](https://stackoverflow.com/questions/70577819/how-to-fix-the-error-error-connecting-to-the-kex-server) 

## Content
[How to fix the error Error connecting to the KeX server? \[closed\]](/questions/70577819/how-to-fix-the-error-error-connecting-to-the-kex-server)
=================================================================================================================================================

Asked 1 year ago

Modified [1 month ago](?lastactivity "2022-12-31 11:55:10Z")

Viewed 11k times

This question shows research effort; it is useful and clear

1

This question does not show any research effort; it is unclear or not useful

Save this question.

[](/posts/70577819/timeline)

Show activity on this post.

**Closed.** This question is [not about programming or software development](/help/closed-questions). It is not currently accepting answers.

* * *

This question does not appear to be about [a specific programming problem, a software algorithm, or software tools primarily used by programmers](/help/on-topic). If you believe the question would be on-topic on [another Stack Exchange site](https://stackexchange.com/sites), you can leave a comment to explain where the question may be able to be answered.

Closed last month.

[Improve this question](/posts/70577819/edit)

When I run the kex, it gives this error

```
Error connecting to the KeX server.
Please try "kex start" to start the service.
If the server fails to start, please try "kex kill" or restart your WSL2 session and try again.
    

```

*   [linux](/questions/tagged/linux "show questions tagged 'linux'")
*   [vnc](/questions/tagged/vnc "show questions tagged 'vnc'")

Answer 
-----------

Following Instructions worked for me, remount `/tmp/.X11-unix` with `rw` option:

```
sudo mount -o remount,rw /tmp/.X11-unix

```

[https://github.com/microsoft/WSL/issues/9303#issuecomment-1345615675](https://github.com/microsoft/WSL/issues/9303#issuecomment-1345615675)

## Note
好使！