# Old Sessions
## Description
Proper session timeout controls are critical for securing user accounts. If a user logs in on a public or shared computer but doesn’t explicitly log out (instead simply closing the browser tab), and session expiration dates are misconfigured, the session may remain active indefinitely.

This then allows an attacker using the same browser later to access the user’s account without needing credentials, exploiting the fact that sessions never expire and remain authenticated.

日本語訳(google翻訳より)
```
ユーザーアカウントを保護する上で、適切なセッションタイムアウト制御は極めて重要です。公共の場所や共用のコンピュータでログインしたユーザーが、明示的にログアウトせず
（単にブラウザのタブを閉じるなどして）その場を離れ、かつセッションの有効期限設定が不適切である場合、セッションが永続的に有効なまま残ってしまう可能性があります。

その結果、セッションが期限切れにならず認証状態が維持されていることを悪用し、後から同じブラウザを使用した攻撃者が、認証情報なしでそのユーザーのアカウントにアクセスでき
るようになってしまいます。
```
### instance
Your friend tells you to check out a new social media platform he built a few years ago. Although its still under development, he said the site is almost complete. He also mentioned that he hates constantly logging into sites, and so has made his page that 'once you login, you never have to log-out again'!

Browse here, and find the flag!
## solve
Web問です。まずログインしたいのでRegisterから登録してログインします。
そうするとcommentというところに4つコメントがあり、その一つに
```
mary_jones_8992
2024-2-20 14:50
Hey I found a strange page at /sessions
```
と書いてあるので、URLに/sessionsをつけてみると
```
1) session:RZ0m6SGlK2LoDbgqTRlzcXajGrW94k-No1W2CzN7qck, {'_permanent': True, 'key': 'admin'}

2) session:lJYhxIkQ2ezaR_VeTRCDsa3leGpvUjfuD2NbPgU_PHI, {'_permanent': True, 'key': 'maru'}
```
というのが出てきました。2個目は自身がログインしたときのものなので、1つ目が必要です。
見た目cookieっぽいので開発者メニューからcookiesに飛ぶとログイン時にcookieがあるので値を一つ目に変更してロードしてあげるとflag取得できました。