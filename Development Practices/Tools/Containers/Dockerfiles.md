# Best Practices
 - have a `USER` directive whenever possible. Running as root is unwise unless it is absolutely necessary.
 - To minimize the number of layers created at build time try to consolidate multiple commands either by using shell scripts or by consolidating multiple commands into one `RUN` directive by using `&&` and `\`
 - **DO NOT** embed secrets inside of your dockerfile at build time. Providing them as environment variables is also not encouraged. If possible use the built in secrets mechanisms to provide and keys or credentials.
 - It is preferable to provide environment variables via a `.env` file rather than passing them on the command line.
 