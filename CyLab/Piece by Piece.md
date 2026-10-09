# Piece by Piece
## Description
After logging in, you will find multiple file parts in your home directory. These parts need to be combined and extracted to reveal the flag. 

日本語訳(google翻訳より)
```
ログイン後、ホームディレクトリに複数のファイル分割パーツがあります。
フラグを入手するには、これらを結合して展開する必要があります。
```
### instance
SSH to chatelaine.cylabacademy.net:35958 and login as ctf-player with password 4f5344cd.

## solve
sshでやれって言われているので、
```
ssh ctf-player@chatelaine.cylabacademy.net -p 35958
```
を使ってパスワード付きで入ります。
とりあえずlsするとpart_aaからaeまでのファイルとinstructions.txtがありました。
とりあえずinstructions.txtの中身を見ます。
```
ctf-player@academy-chall$ cat instructions.txt
Hint:

- The flag is split into multiple parts as a zipped file.
- Use Linux commands to combine the parts into one file.
- The zip file is password protected. Use this "supersecret" password to extract the zip file.
- After unzipping, check the extracted text file for the flag.

```
こんな感じでHintが出てきました。
日本語訳(google翻訳より)
```
- フラグは複数のパートに分割され、zipファイルとしてまとめられています。
- Linuxコマンドを使用して、それらのパートを1つのファイルに結合してください。
- zipファイルはパスワードで保護されています。「supersecret」というパスワードを使用して解凍してください。
- 解凍後、展開されたテキストファイルでフラグを確認してください。
```
というわけでファイルまとめて解凍しないといけないらしいので、
```
ctf-player@academy-chall$ cat part_aa part_ab part_ac part_ad part_ae > flag
ctf-player@academy-chall$ unzip -p flag
[flag] flag.txt password:
academy{z1p_and_spl1t_f1l3s_4r3_fun_2cd7190f}ctf-player@academy-chall$ Connection to chatelaine.cylabacademy.net closed by remote host.
Connection to chatelaine.cylabacademy.net closed.
```
ということでflagゲットです。