# Viewsの作成

## views.pyの編集

ビューとは、Django アプリケーションでユーザーのリクエストに対するレスポンスを処理する関数またはクラスです。<br>
最初のビューを書いてみましょう。ai_recipe/views.py を開いて、以下のコードを書いてください。<br>

```
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, ukouken!")
```

## urls.pyの編集

このビューを呼ぶためには、URL を対応付けさせる必要があります。そのために、URLconf(URL の設定ファイル)を作成していきます。<br>
ai_recipe ディレクトリ内に urls.py というファイルを作ります。ディレクトリは以下のようになるはずです:<br>

ai_recipe/  
├── __init__.py  
├── admin.py  
├── apps.py  
├── migrations/  
│ └── __init__.py  
├── models.py  
├── tests.py  
├── urls.py  
└── views.py  
<br>

ai_recipe/urls.py には以下のコードを書いてください。<br>

```
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```
<br>

プロジェクトの URLconf から先ほど作成したアプリケーションの URLconf を呼び出せるようにしましょう。<br>
mysite/urls.py に以下のコードを書いてください。(注: urls.py は mysite の下と ai_recipe の下とで二つあります)<br>

```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("mainpage/", include("ai_recipe.urls")),
    path("admin/", admin.site.urls),
]
```

これで、index ビューを URLconf に紐づけることができました。<br>

## 動作確認

manage.py と同じ階層でコマンドを実行し、再びサーバーを起動してみましょう。<br>
`$ python manage.py runserver`<br>

ブラウザで localhost:8000/mainpage にアクセスすると、"Hello, ukouken!"と表示されます。これは、ビューの index 関数で書いたものです。
