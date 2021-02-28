## POSTMAN

URL： https://www.postman.com

## 既存のデータベースにカラムを追加

フロント => React, Redux, Typescript バックエンド => Laravel

作業工程としては

1. バックエンド(laravel)でデータベースを修正
2. バックエンドでAPIを修正
3. APIがしっかり動作するかをテスト
4. フロントエンド(React)でAPIを叩く
5. しっかり動作しているかをデータベースで確認
6. フロントエンド(React)でデータを受け取って表示

#### Laravel

1. docker workspaceで以下コマンドを実行 && Migrate

```bash
docker-compose exec workspace bash
-> php artisan make:migration add_notes_to_example_table --table=example 
// step1
// Migration File 修正後下記コマンド
-> php artisan migrate
```

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddNotesToExampleTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('example', function (Blueprint $table) {
            // notesカラム追加
            $table->string("notes")->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('Example', function (Blueprint $table) {
            //
        });
    }
}
```

2. APIを修正

```php
        foreach ($example_item as $item) {
            if ($item["name"] == "") {
                continue;
            }
            $this->example->insert([
                [
                    ~~~~
                    "notes" => $item["notes"] //既存のAPIに追加
                ]
            ]);
        }
```

3. Postmanなどを使ってAPIの動作チェック
4. APIを叩く

#### Redux

今回は連想配列オブジェクトで定義していたためReduxの修正はこれだけ。もし配列やオブジェクト、個別で状態を管理していたなら追加の修正点あり。（実際にAPIを叩くところなど）

```typescript
export type Example = {
~~~~
  notes: string //型定義を既存のTypeエイリアスに追加
};
export interface ExamplesState {
  examples: Record<number, Example>; //interfaceにも追加
}
export const exampleInitialState: ExampleState = { //initial Stateに上記の型定義が反映される
  examples: {},
};
const exampleSlice = createSlice({
  name: 'exampleState',
  initialState: exampleInitialState,
  reducers: {
    setExamples: (
      state: ExamplesState,
      { payload }: PayloadAction<Example[]>
    ) => {
      state.examples = {};
      payload.forEach(item => {
        state.examples[item.id] = item;
      });
    },
});
export const newExamples = (
    example: Example
): AppThunk => async (dispatch: AppDispatch) => {
  try {
    const res = await API.post('/your api url')
      .setBody({ example })
      .fetch();
    dispatch(setExamples(res.data));
  } catch (err) {
    console.log(err);
  }
};
```

#### React

実際にAPIを叩いてみる

```react
  const handleSubmit = (e: { preventDefault: () => void }) => {
    e.preventDefault();
    dispatch(
      newExamples(
          examples
      )
    );
  };
  const handleChangeExamples = (key, value, id) => {
    let temp = []
    temp = temp.concat(example)
    temp.forEach((a, i) => {
      if (a.id === id) {
        temp.splice(i, 1, {...a, [key]: value})
      }
    })
    setExample(temp)
  }
                                  <TextField
                                    value={e.examples}
                                    onChange={e => handleChangeExamples('examples', e.target.value, e.id)}
                                  />
```

POST OK だったら次はGET

これはGETメソッドでAPI叩いてみてしっかりとPOSTしたデータが表示されているかを見るだけ。データベースで確認しても良い。