# APIの導入・動作確認

## OpenAI APIの導入

OpenAI APIを使ってGPT-4を導入します。
以下のコードをai_recipe/views.pyに書き込んでください。

```
from openai import OpenAI
client = OpenAI()

def get_recipe(input_text):
    instruction = ''''''入力として受け取った食材リストを用いて、料理のレシピを提案してください。
    ・筑波大学生向けです。
    ・提示された食材を全て使ってください。
    ・簡潔に作り方のみを説明してください。
    '''

    completion = client.chat.completions.create(
        model = "gpt-4-turbo",
        temperature = 0,
        messages = [
                {"role": "system", "content": instruction},
                {"role": "user", "content": input_text}
        ],
    )
    result = completion.choices[0].message.content.strip()
    return result
```
<br>
instructionの内容は好みに応じて書き換えてOKです。<br>

先ほど作成したビューも編集しましょう。indexビューを以下のように書き換えてください。
```
def index(request):
    recipe = ""
    if request.method == "POST":
        ingredients = request.POST.get('ingredients', '')
        recipe = get_recipe(ingredients)
    return render(request, 'ai_recipe/index.html', {'recipe': recipe, 'ingredients': ingredients if request.method == "POST" else ''})
```

OpenAI APIを使うには、APIキー(有料)が必要です。ここではAPIキーを用意してあるので、部員に聞いてください。<br>
自宅でGPT-4を動かすためには、各自APIキーを入手する必要があります。<br>
以下のコマンドを実行して、APIキーをターミナルの環境変数に登録してください。<br>

Macの場合<br>
```
$ export OPENAI_API_KEY='ここにAPIキーを入力'
```
<br>

PowerShellの場合<br>
```
$Env:OPENAI_API_KEY='ここにAPIキーを入力'
```
注: PowerShellの場合のみ、$は省略せず入力してください
<br>

Windows(コマンドプロンプト)の場合<br>
```
$ setx OPENAI_API_KEY "ここにAPIキーを入力"
```
<br>

ここまでで一通りコーディングが完了しました。次の章で動作確認を行ってみましょう。

参考: https://platform.openai.com/docs/quickstart<br>

## 動作確認
サーバーを起動します。
`$ python manage.py runserver`
<br>

ブラウザでlocalhost:8000/mainpageへアクセスします。<br>
上のテキストボックスに食材を入力し、「実行」ボタンを押します。下のテキストボックスにレシピが表示されれば成功です。<br>
これから毎日のレシピ決めはAIが全て行ってくれます。やったね！<br>