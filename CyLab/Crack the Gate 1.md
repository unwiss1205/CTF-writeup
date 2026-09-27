# Crack the Gate 1
## Description
We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: ctf-player@cylabacademy.org. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?

日本語訳(google翻訳より)
```
現在、ある調査を進めています。捜査対象の一人である「ctf-player」という人物が、アクセス制限のかかったWebポータル内に機密データを隠していると見られています。彼がログインに使用するメールアドレス（ctf-player@cylabacademy.org）は特定できましたが、残念ながらパスワードは不明で、一般的な推測手法も通用しませんでした。しかし、何かが引っかかります……まるで開発者が「秘密の入り口」を残しておいたかのようなのです。その方法を突き止められますか？
```

### Instance
The website is running here. Can you try to log in?

## solve
Web問でした。開発者ツールでコードを見ると,
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #eaeaed;
            font-family: Arial, sans-serif;
        }

        #loginForm {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
        }

        #loginForm label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }

        #loginForm input {
            width: calc(100% - 10px);
            padding: 8px;
            margin-bottom: 16px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        #loginForm button {
            width: 100%;
            padding: 10px;
            background-color: #007BFF;
            border: none;
            color: white;
            border-radius: 4px;
            font-size: 16px;
        }

        #loginForm button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
 <!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->
<!-- Remove before pushing to production! -->   

    <form id="loginForm">
        <h2 style="font-size: 24px; margin-bottom: 24px;">
            Login
        </h2>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br>
        <button type="submit">Login</button>
    </form>

    <script>
        document.getElementById('loginForm').addEventListener('submit', function(event) {
            event.preventDefault();

            const formData = {
                email: document.getElementById('email').value,
                password: document.getElementById('password').value
            };

            fetch('/login', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(formData)
            })
            .then(response => response.json())
            .then(data => {
                console.log(data);
                if (data.success) {
    prompt('Login successful!\nFlag:', data.flag);
} else {
    alert('Invalid credentials');
}

            })
            .catch(error => console.error('Error:', error));
        });
    </script>

</body>
</html>
```
というコードがあり,この中に
```html
<!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->
```
という怪しい文章がありました。ROT13で復号すると,
```
Jack - temporary bypass: use header "X-Dev-Access: yes
```
となりました。このheaderを使えば良さそうなので,burpsiteでctf-player@cylabacademy.orgと適当なpasswordを使ってログインした後,
name:X-Dev=Acsess value:yes 
のヘッダーを追加すると,Flagがゲットできました!