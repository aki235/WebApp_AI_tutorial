# templatesの作成

先ほど作成したページは、Hello, ukouken!と表示するだけでしたが、これを改良してみましょう。<br>
食材を入力するテキストボックス、作成ボタン、レシピを表示するボックスを書いていきます。(※ただし、まだ外観のみで、ボタンをクリックしても何も起きない状態です)<br>

ai_recipe内にtemplatesというディレクトリを作成してください。templatesディレクトリの中に、さらにai_recipeというディレクトリを作成してください。<br>
その中に、index.htmlというファイルを作り、以下のHTMLコードを書きこんでください。<br><br>
ファイル構成は、<br>
ai_recipe/templates/ai_recipe/index.html<br>
のようになります。

```
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>AIレシピメーカー</title>
</head>
<body>
    <h1>AIレシピメーカー</h1>
    <form action="{% url 'index' %}" method="POST">
        {% csrf_token %}
        <h2>食材:</h2>
        <textarea id="ingredients" name="ingredients" required rows="4" cols="50"></textarea>
        <br>
        <button type="submit">作成！</button>
    </form>

    <h2>レシピ</h2>
        <textarea readonly rows="10" cols="50">{{ recipe }}</textarea>
</body>
</html>
```
<br>

ai_recipe/views.pyのindexビューを以下のように書き換えてください。
```
def index(request):
    recipe = ""
    ingredients = ""
    return render(request, 'ai_recipe/index.html', {'recipe': recipe, 'ingredients': ingredients if request.method == "POST" else ''})
```

再びターミナルで`$ python manage.py runserver`を実行してみましょう。テキストボックス二つと、ボタン一つが見えていたら成功です！