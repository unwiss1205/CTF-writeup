# MultiCode
## Description
We intercepted a suspiciously encoded message, but it’s clearly hiding a flag. No encryption, just multiple layers of obfuscation. Can you peel back the
layers and reveal the truth? Download the message.

日本語訳(Google翻訳より)
```
不審なエンコードが施されたメッセージを傍受しました。明らかにフラグが隠されています。暗号化はされておらず、単に幾重もの難読化が施されているだけです。その層を剥ぎ取り、
真実を暴き出せますか？メッセージをダウンロードしてください。
```

## solve
message.txt内の文字列
```
NmU3MDZlNzE3MjdhNmMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM2NzIzNDM5NmUzODM3MzkyNTM3NDQ=
```
どうやらいろいろと復号しないといけないらしいのでやっていきます。

とりあえず末尾に「=」がついているのでBase64です。
復号後
```
6e706e71727a6c2537426172666772715f72617030717661745f367234396e383739253744
```
見た目16進数なので解読
```
npnqrzl%7Barfgrq_rap0qvat_6r49n879%7D
```
文字列内に%がついているのでURLエンコードがされてるのがわかりました。ので、デコードします。
```
npnqrzl{arfgrq_rap0qvat_6r49n879}
```
「{}」がついているので文頭だけROT13確認するとacademyが出てきたのでROT13を使います。
```
academy{nested_enc0ding_6e49a879}
```
ということでflag獲得です。
