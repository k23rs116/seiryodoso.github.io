<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>掲示板</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .post {
            border: 1px solid #ccc;
            padding: 10px;
            margin-bottom: 10px;
        }
        /* スマホ用のスタイル */
        @media (max-width: 600px) {
            body {
                margin: 10px;
            }
            .post {
                padding: 5px;
            }
        }
    </style>
</head>
<body>
    <h1>掲示板</h1>
    <form id="postForm">
        <textarea id="postContent" rows="4" cols="50" placeholder="ここに投稿を入力してください"></textarea><br>
        <button type="submit">投稿</button>
    </form>
    <div id="posts"></div>

    <script>
        // ローカルストレージから投稿を読み込む
        function loadPosts() {
            const posts = JSON.parse(localStorage.getItem('posts')) || [];
            posts.forEach(content => {
                const post = document.createElement('div');
                post.className = 'post';
                post.textContent = content;
                document.getElementById('posts').appendChild(post);
            });
        }

        // 投稿を保存する
        function savePost(content) {
            const posts = JSON.parse(localStorage.getItem('posts')) || [];
            posts.push(content);
            localStorage.setItem('posts', JSON.stringify(posts));
        }

        document.getElementById('postForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const content = document.getElementById('postContent').value;
            if (content.trim() !== "") {
                const post = document.createElement('div');
                post.className = 'post';
                post.textContent = content;
                document.getElementById('posts').appendChild(post);
                savePost(content);
                document.getElementById('postContent').value = '';
            }
        });

        // ページ読み込み時に投稿を表示
        window.onload = loadPosts;
    </script>
</body>
</html>
