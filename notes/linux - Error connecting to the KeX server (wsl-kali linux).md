# linux - Error connecting to the KeX server (wsl-kali linux)
Save From : [linux - How to fix the error Error connecting to the KeX server? - Stack Overflow](https://stackoverflow.com/questions/70577819/how-to-fix-the-error-error-connecting-to-the-kex-server) 

## Content
[How to fix the error Error connecting to the KeX server? \[closed\]](/questions/70577819/how-to-fix-the-error-error-connecting-to-the-kex-server)

Asked 1 year ago


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

好使！ `10061 ERROR`
