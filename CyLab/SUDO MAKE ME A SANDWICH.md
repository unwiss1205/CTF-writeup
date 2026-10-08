# SUDO MAKE ME A SANDWICH
## Description
Can you read the flag? I think you can!

### instance
ssh -p 22280 ctf-player@chatelaine.cylabacademy.net using password 98cb1be0

## solve
とりあえずsshで入ります。
入れたら一旦ls
```
ls -a
.  ..  .bash_logout  .bashrc  .cache  .profile  flag.txt
```
flag.txtがあるのでできないとは思いつつcatしてみるができず。
ここでヒント見ました。
### hint
```
What is sudo?
```
sudoは管理者権限を使うときに使うので管理者権限で使える権限があるんだろうなと思ったので
```
sudo -l
```
すると、
```
Matching Defaults entries for ctf-player on challenge:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User ctf-player may run the following commands on challenge:
    (ALL) NOPASSWD: /bin/emacs
```
下が管理者権限で実行できるものなので実行します。
```
sudo /bin/emacs flag.txt
```
```
File Edit Options Buffers Tools Text Help                                                                                                                                                                                                  
academy{ju57_5ud0_17_101e25fb}
```
ということでflag取得