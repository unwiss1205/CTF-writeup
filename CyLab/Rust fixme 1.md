# Rust gixme 1
## Description
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
Download the Rust code here.

日本語訳(Google翻訳より)
```
Rustをご存知ですか？このRustファイルの構文エラーを修正して、フラグを表示させてください！
Rustコードはこちらからダウンロードできます。
```
## solve
与えられたコードは以下のものです。
``` rust
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS") // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        ret; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        ":?", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```
問題文の通りコード内に修正箇所が書かれているので直していきます。
### First
```rust
let key = String::from("CSUCKS") // How do we end statements in Rust?
```
↓   この行の終了部分に「;」がないので書き込みます。
```rust
let key = String::from("CSUCKS"); // How do we end statements in Rust?
```
### Second
```rust
ret; // How do we return in rust?
```
↓   rustで値を返すのはreturnなので訂正します。
```rust
return; // How do we return in rust?
```

### Last
```rust
 println!(
        ":?", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
```
rustのprintln!では変数を使うとき「{}」を使うので「:?」になっている部分を書き換えます。
```rust
 println!(
        "{}", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
```
後は配布ファイル内で
```
cargo run
```
などのコマンドでファイルを実行してflagが取得できました。
## solver
```rust
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS"); // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        "{}", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```
## postscript
初めてGitHubを使って初めてwriteupを書いたので分かりにくいかもしれません。
試行錯誤しつつやっていこうと思います。
