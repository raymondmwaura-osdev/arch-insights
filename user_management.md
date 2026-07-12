# User Management

## Create A User

```
useradd --create-home -G wheel raymond
```

+ `--create-home`: Create a home directory for the user.
+ `-G wheel`: Add the user to the `wheel` group. That group is commonly used for `sudo` access.
+ `raymond`: The username.

## Set User's Password

`passwd raymond`, then enter the user's password twice.

## Allow User to Use Sudo

Securely edit the sudoers file.

```
EDITOR=nvim visudo
```

Uncomment this line:

```
%wheel ALL=(ALL:ALL) NOPASSWD: ALL
```

This will allow all users in the `wheel` group to use sudo to run any command, without a password.

---
