## SSH

For remote work use public key authentication. Therefore we have to initially permit root access with password.

```bash
sudo nano /etc/ssh/sshd_config
```

Add `PermitRootLogin yes` and reboot.

Copy public key to the Raspberry Pi
```bash
cat ~/.ssh/id_rsa.pub | ssh root@alpha "mkdir .ssh && cat - >> ~/.ssh/authorized_keys"
```

Test ssh login

```bash
ssh root@alpha
```

Change `sshd_config`
```
PermitRootLogin prohibit-password
PubkeyAuthentication yes
```