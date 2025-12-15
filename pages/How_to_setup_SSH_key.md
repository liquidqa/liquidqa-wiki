# Generate a key pair

### 1) Generate key
In your local repo Terminal:
```
$ ssh-keygen -t rsa
```
Example Output:
```
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/YOURNAME/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/YOURNAME/.ssh/id_rsa
Your public key has been saved in /c/Users/YOURNAME/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:FFn8JF8ov427QTF2+5xw7hRHcUU0BB9xnR5EK+CPv7k YOURNAME@DESKTOP-VNMR1KP
The key's randomart image is:
+---[RSA 3072]----+
|        .+.. o=@@|
|        ..= + ooO|
|        .  O+oooo|
|       .   .*+.+ |
|        S  ..*.o.|
|           .+ =o+|
|            .o +o|
|            ..=  |
|            .E.. |
+----[SHA256]-----+
```

### 2) Check the key 
```
$ cat ~/.ssh/id_rsa.pub
```
Example Output:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDN11K7q9abg+VfThBlPoGoHzBjLGEgUmhbW8sVCK53H0vMvpSK6Jf1E0BFunxSoW5vR18pcbXZR51vqEVBwvc8ma+xr7Kb9FOO6sbIISPI1LzbvJrQfV7d3fA8SfIXRhil6HMCFY2WYhe7+j2gnLvgf+Kc8WLGLWXT1gJBAHl3iAKQM2eDgLwN1kiTFuTLeceoS7yBul2Ay/7WeHwILvjXYfngv2/Z48+Le6+64giEqx17hd0N/1hMpDWMvabShvu7KFRtO+FuUNlRTtpMuKP4jWvQ3b9el0uk2OUO+RVuOde2Hgv6rcx76EPWOMJ7ZICmRn21u2oajU+saB5x6lRKWaAvSJiRduQ7TRhAgKfnX/XpGO5/8vILaXve1ldmYCw2zMatLPg0W1igbxraHar+BQyaKRiJfxv0EuiN/eorBhl1OBZU68W3Eoq3VyMyggrjgWALGv5eVFf44JDoCNEUz58mfdJI3Nt8zp12FwWEhIaN5JMxwlW7pzOOJrp8oXk= Stoio@DESKTOP-VNMR1KP
```
### 3) Copy the key (including the ssh-rsa) and add it to GitHub - Settings - SSH Keys -> New SSH Key
