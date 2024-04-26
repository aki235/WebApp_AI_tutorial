# models の作成

## models.pyの編集

このアプリケーションでは、今までに作ったレシピの履歴を保存して一覧表示できるようにします。<br>
そのためには、models を使ってデータベースと連携を行う必要があります。<br>

ai_recipe/models.py を開いて、以下のコードを書きこんでください。<br>

```
class FoodRecipe(models.Model):
    ingredients = models.TextField()
    recipe = models.TextField()

    def __str__(self):
        return self.recipe
```

modelsを書き換えた後は、データベース(ここでは、db.sqlite3というファイル)に変更を反映させる必要があります。<br>
manage.py のある階層に移動し、以下を実行してください。<br>
`$ python manage.py makemigrations`<br>
`$ python manage.py migrate`

## 管理ユーザーの作成
adminサイトにログインするため、管理ユーザーを作成してみましょう。<br>
ターミナルで以下を実行してください。<br>
`$ python manage.py createsuperuser`

好きなユーザー名とメールアドレスを入力し、パスワードを設定してください。(実際にメールが送られてくることはないので、空でもかまいません)<br>

ai_recipe/admin.pyに以下を追記してください。<br>
```
from .models import FoodRecipe

admin.site.register(FoodRecipe)
```

## 管理画面の表示
まずサーバーを起動してみましょう。<br>
`$ python manage.py runserver`

次にブラウザを起動して、localhost:8000/adminにアクセスします。<br>
UsernameとPasswordの入力が求められるので、先ほど作成したユーザー名とパスワードを入力し、ログインしてください。<br>
Food Recipesという名前でmodelが表示されているのを確認してください。