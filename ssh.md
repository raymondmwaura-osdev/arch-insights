# ssh

**Installation**:

```sh
# Arch Linux
pacman -S openssh
```

---

## Key Generation

Use `ssh-keygen`:

```sh
ssh-keygen -C "comment"
```

+ Have a useful comment to help identify what/who uses the key.
+ Also have a passphrase for the key. The passphrase is used only once when using `ssh-add` to add the key to the agent (`ssh-agent`). You won't need to provide the passphrase everytime the key is used for authentication. The passphrase encrypts your private key file ensuring that even if someone steals the private key, they won't be able to use it without the passphrase.

### Key Types

The type of key to generate is specified by the `-t` flag in the `ssh-keygen` command.

+ **ed25519** (recommended): Very quick to generate and use. Provides excellent security with small key size (around 68 characters).
+ **rsa**: Takes longer to generate and use. Has larger public keys (4096-bit) with around 700+ characters.
+ **ecdsa**: Faster than RSA.
+ **dsa** (deprecated)

---

## Key Management

+ `ssh-agent` holds private keys and uses them for automatic authentication when logging in to other machines.
+ `ssh-add` is used to add private keys to `ssh-agent`, because the agent doesn't have any private keys initially. This needs to be done every time the agent is started like after restarting the machine.

---
