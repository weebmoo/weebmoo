<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة كتابة المقالات مع النشر التلقائي</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            direction: rtl;
        }
        .container {
            background-color: white;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            max-width: 600px;
            width: 100%;
        }
        h2 {
            text-align: center;
        }
        textarea {
            width: 100%;
            height: 100px;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            border: 1px solid #ddd;
            font-size: 16px;
        }
        select {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            border: 1px solid #ddd;
            font-size: 16px;
        }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        button:hover {
            background-color: #0056b3;
        }
        .output {
            margin-top: 20px;
            padding: 10px;
            background-color: #f1f1f1;
            border-radius: 5px;
            min-height: 100px;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>أداة كتابة المقالات مع النشر التلقائي</h2>

    <textarea id="inputText" placeholder="أدخل موضوع المقال..."></textarea>

    <button onclick="generateAndPublishArticles()">كتابة 10 مقالات ونشرها</button>
    <div class="output" id="outputText"></div>
</div>

<script>
    async function generateAndPublishArticles() {
        const input = document.getElementById('inputText').value;
        const articleTitles = [];
        const outputElement = document.getElementById('outputText');
        outputElement.innerHTML = "جاري كتابة ونشر 10 مقالات...";

        // كتابة 10 مقالات مختلفة بناءً على الموضوع
        for (let i = 1; i <= 10; i++) {
            const title = `${input} - المقال رقم ${i}`;
            const content = generateArticleContent(title);
            articleTitles.push(title);

            // نشر المقال في المدونة
            const response = await publishArticleToWordPress(title, content);

            if (response.ok) {
                outputElement.innerHTML += `<br>تم نشر المقال: ${title}`;
            } else {
                outputElement.innerHTML += `<br>فشل نشر المقال: ${title}`;
            }
        }
    }

    // دالة لإنشاء محتوى المقال
    function generateArticleContent(title) {
        return `${title} هو مقال يتحدث عن ${title}. هذا المحتوى تم إنشاؤه تلقائيًا باستخدام أداة الكتابة والنشر التلقائي.`;
    }

    // دالة لنشر المقال في مدونة WordPress باستخدام REST API
    async function publishArticleToWordPress(title, content) {
        const apiUrl = 'https://your-wordpress-site.com/wp-json/wp/v2/posts';
        const apiKey = 'your-api-key';  // هنا تدخل مفتاح الـ API الخاص بك

        const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': `Bearer ${apiKey}`
            },
            body: JSON.stringify({
                title: title,
                content: content,
                status: 'publish'  // نشر المقال مباشرة
            })
        });

        return response;
    }
</script>

</body>
</html>
