[TOC]



# Snippets

## fun (function for controller)

```php
public function FunctionName(Type $var = null)
{
	# code...
}
```

# CODE

## DB

### === reference ===

#### Laravelでトランザクション処理の方法をサンプル付きで解説

https://gitlab.com/questarteam/back.mamozon.com.git

#### 【Laravel】transactionメソッド

https://qiita.com/yukachin0414/items/97194eb8e6f51cece9f3

#### transactionメソッドって何？

https://www.hypertextcandy.com/laravel-tips-transaction-method-returns-value

### ============

### Transaction

```php
DB::transaction(function () {
    // code
});
```

Transaction method is auto transaction.



### beginTransaction

```php
DB::beginTransaction();
```

hand transaction method. it indicates start point.

### commit

```php
DB::commit();
```

it indicates commit

### rollback

```php
DB::rollback();
```

it indicates rollback

## \Throwable

```php
catch(\Throwable $th) {
	return $th
}
```



## Fill

in case want to edit some data from array, fill is useful. example code is like that below/

```php
public function update(Request $request)
{
    $flight = App\Flight::find($request->id);
    $flight->fill($request->all())->save();
}
```



### === references ===

#### (Laravel) fillを使ってモデルの複数カラムを更新する

https://qiita.com/tkt989/items/c2e01ec2fe91ef5f08d2

===============



## dd()

for debug



## AUTH



## find() get() first()



### === references ===

#### 【Laravel】DB登録値取得時のfind()、get()、first()の返り値早見表

https://qiita.com/sola-msr/items/fac931c72e1c46ae5f0f



## With

Order_management_system (pre)

```
$documents = $this->document->with("Users")->get();
return $documents
```

"Users" is relation name

Ex in case of that relationship, it must be "Users"

```php
return $this->belongsTo('App\Users', 'user_id', 'id');
```



## orderby

### BASIC (like SQL)

```php
// order by ascending
$post = POST::orderBy('post.name', 'asc')->get();
// SELECT * FROM 'posts' ORDER BY 'name' ASC

// order by descending
$post = POST::orderBy('post.name', 'desc')->get();
// SELECT * FROM 'posts' ORDER BY 'name' DESC
```



### ELOQUENT

```php
POST::orderBy('name', 'asc')
		->orderBy('email', 'desc')
		->get();
// SELECT * FROM 'posts' ORDER BY 'name' ASC 'email' DESC
```



## GROUP BY

the group by function is popular as grouping the query results in laravel.

the groupby function belongs to Collection, not eloquent. so always use get() method before groupby otherwise it will not work as expected.

```php
<?php

namespace App\Http\Controllers;
use Illuminate\Http\Request;
use Student;

class StudentController extends Controller
{
  
    public function index(Request $request)
    {
        $students = Student::orderBy('created_at')->get()->groupBy(function($data) {
            return $data->created_at->format('Y-m-d');
        });

        return view('home', compact('students'));
    }

}
```



# Extension / Method

## FormRequest class (Validation

by formrequest, controller do not have to have validation.  -> decrease the quantity of content / code.

### in case do not use FormRequest

```php
...
class BooksController extends Controller
{
    public function store( Request $request ){

        //------------------------------------------------------------------
        //*** Validation：[Start] ***
        //------------------------------------------------------------------
        //バリデーションルールを設定
        $validator = Validator::make($request->all(), [
                'item_name' => 'required|min:3|max:255',
                'item_number' => 'required|min:1|max:3',
                'item_amount' => 'required|max:6',
                'published' => 'required',
        ]);
        //バリデーションルールにでエラーの場合 
        if ($validator->fails()) {
                return redirect('/')->withInput()->withErrors($validator);
        }
        //------------------------------------------------------------------
        //*** Validation：[End] ***
        //------------------------------------------------------------------


        // 本作成処理...
```

### in case use FormRequest

```php
        //バリデーションルールにでエラーの場合 
        if ($validator->fails()) {
                return redirect('/')->withInput()->withErrors($validator);
        }
```



### Advatage of using that

- return redirect to form origin automatically

- do not need withErrors() <automatically>

- do not need withInput() <automatically>



### Usage

```
php artisan make:request filename
```

then edit file. the ex is like below

```php
<?php
namespace App\Http\Requests;
use Illuminate\Foundation\Http\FormRequest;

class BookInputPost extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize()
    {
        return true; //[ *1.変更：default=false ]
    }
https://qiita.com/daisu_yamazaki/items/e44d4b744d9d5f9bc8b3
    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        //[ *2.追加：Validationルール記述箇所 ]
        return [
            'item_name'   => ['required','min:3','max:10'],
            'item_number' => ['required','max:3'],
        ];
    }

    //[ *3.追加：Validationメッセージを設定（省略可） ]
    //function名は必ず「messages」となります。
    public function messages(){
        return [
            'item_name.required'  => '名前を入力してください。',
            'item_name.min'       => '名前は3文字以上でお願いします。',
            'item_name.max'       => '名前は10字以内でお願いします。',
            'item_number.required'=> '冊数を入力してください。',
            'item_number.max'     => '冊数は3字以内でお願いします。',
        ];
    }

}

```

then edit controller. before using this, the type is (Request $request)

```php
...
use App\Http\Requests\BookInputPost; //*1 FormRequestを使用してValidate

class BooksController extends Controller {

    //---------------------------------------------------------------
    // *store: 引数[Requestクラス → BookInputPostクラス]に変更
    //---------------------------------------------------------------
    public function store( BookInputPost $request ){ //*2 Request → BookInputPost
        $books = new Book;
        $books->item_name = $request->item_name;
        $books->item_number = $request->item_number;
        $books->item_amount = $request->item_amount;
        $books->published = $request->published;
        $books->save();
        return redirect('/');
    }

...
```

### === references ===

#### Laravel : FormRequestクラスを使ってValidation(MyMemo)

https://qiita.com/daisu_yamazaki/items/e44d4b744d9d5f9bc8b3



## withError()

display the error of validation. 

## withInput()

pass data to the next page which is redirect path.

## SELECT

特定のカラムデータだけの配列を作成する際に仕様。

### reference

#### Laravelでfindしたレコードから特定のカラムを抽出したい

https://qiita.com/hppRC/items/25fb5af10d87618f2889

# Error

## undefined index ''

Laravel で作成した API を React/Redux で叩いたときにエラーが出た (undefined Index tax)

#### Laravel

```php
     @return

    public function add_document(array $doc_info, array $product_item, array $postage_item, string $remarks = null)
    {
        $current_user = Auth::user();
        $this->document->insert([
            [
                "document_type_id" => $doc_info["document_type_id"],
                ~~~
                ~~~
                "quotation_expiration_date" => $doc_info["quotation_expiration_date"]
            ]
        ]);
        $id = $this->document->max("id");
        foreach ($product_item as $item) {
            if ($item["name"] == "") {
                continue;
            }
            $this->purchasedproduct->insert([
                [
                    "document_id" => $id,
                    "name" => $item["name"],
                    "quantity" => $item["quantity"],
                    "unit" => $item["unit"],
                    "unit_price" => $item["unit_price"],
                    "tax" => $item["tax"],
                ]
            ]);
        }
```

#### React

```react
  const dispatch = useDispatch()
  const router = useRouter();
  const [purchasedProduct, setPurchasedProduct] = useState([
    { name: 'a', unit: '', unit_price: '100', quantity: 1, id: 0, tax: '0.1' },
    { name: 'b', unit: '', unit_price: '5000', quantity: 1, id: 1, tax: '0.1' },
    { name: 'c', unit: '', unit_price: '70000', quantity: 1, id: 2, tax: '0.1' },
  ]);

  const handleSubmit = (e: { preventDefault: () => void }) => {
    e.preventDefault();
    dispatch(
      newDocuments(
	~~~
        purchasedProduct,
	~~~
      )
    );
    router.push('/documents/mitsumori');
  };
```

#### Redux

```typescript
export const newDocuments = (
~~~
  product_item: Product,
~~~
): AppThunk => async (dispatch: AppDispatch) => {
  try {
    const doc_info = {
        ~~~
    };

    const postage_item = [
      {
          ~~~
      },
    ];

    const res = await API.post('/document')
      .setBody({ doc_info, remarks, product_item, postage_item })
      .fetch();
    dispatch(setDocuments(res.data));
  } catch (err) {
    console.log(err);
  }
};
```

Docker を再度ビルドしたら解決した。

https://qiita.com/tearoom6/items/326895f0a35774d70729

## PHP Warning: include(/var/www/vendor/composer/../../app/Console/Kernel.php): failed to open stream: No such file or directory in /var/www/vendor/composer/ClassLoader.php on line 444

When I try to php artisan make:migration, it will throw the above exception.

solution 1

```bash
composer update
```

You can simply do the composer update. Then I got those errors.

PHP Fatal error: Uncaught ReflectionException: Class App\Console\Kernel does not exist in /var/www/vendor/laravel/framework/src/Illuminate/Container/Container.php:809

Script @php artisan package:discover --ansi handling the post-autoload-dump event returned with error code 255

![](/home/lilshimon/Desktop/Screenshot_20201215_100937.png)

なぜかファイルが削除されていたのでもとに戻してもう一度マイグレーションファイルを作成するコマンドをたたいたら無事に実行された。

## Column not found: 1054 Unknown column 'quantity' in 'field list'

This is the full message of the error

```php
Column not found: 1054 Unknown column 'quantity' in 'field list' (SQL: insert into `purchased_products` (`document_id`, `name`, `notes`, `quantity`, `tax`, `unit`, `unit_price`) values (23, \u30c7\u30b8\u30bf\u30eb\u30b5\u30a4\u30cd\u30fc\u30b8\u8ca9\u58f2(\u5c4b\u5916)32\u30a4\u30f3\u30c1, ?, 1, 0.1, \u500b, 550000))",
```

The solution was

## BadMethodCallException (php artisan migrate)

when i tried 2 type 'php artisan migrate', i had this error.

the descirtion was like this--->Method Illuminate\Database\Schema\Blueprint::product_types_id does not exist.

Just change migration file is working

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateFlightsTable extends Migration
{
    /**
     *
     * @return void
     */
    public function up()
    {
        Schema::create('flights', function (Blueprint $table) {
            $table->id(); // from product_types_id 2 id
            $table->string('name');
            $table->string('airline');
            $table->timestamps();
        });
    }

    /**
     *
     * @return void
     */
    public function down()
    {
        Schema::drop('flights');
    }
}
```



## Test error

### SQLSTATE[42S22]: Column not found: 1054 Unknown column 'orders.deleted_at' in 'where clause'

this error implies there are no data in database. 

tried solution1 ---> add deleted_at in database by migrating.

to do that, I add deleted_at in migration file.



```php
$table->softDeletes();
```



## https://qiita.com/daisu_yamazaki/items/e44d4b744d9d5f9bc8b3The stream or file \"/var/www/storage/logs/laravel.log\" could not be opened: failed to open stream: Permission denied



the error display  in postman when tries to store json. in this case the error messages are not showed.

```
php artisan cache:clear
php artisan config:clear
php artisan config:cache
php artisan optimize:clear

chmod -R 775 storage/logs/
chmod -R 777 storage/logs/
```

now you get error message right. hope you get it

### === references ===

https://stackoverflow.com/questions/48619445/permission-denied-error-using-laravel-docker





## "Argument 2 passed to App\\Http\\Repositories\\OrderRepository::store() must be of the type array, null given, called in /var/www/app/Http/Controllers/OrderController.php on line 49",



```php
// line 49 of OrderController

public function store (Request $request)
{
    $this->orderRepository->store($order_info, $order_item, $attachments);
}

// run store api with this json data
{
   "order_info": [
       {
           "start_date":  "Oct 20",
           "end_date": "Oct 21",
           "expected_start_date": "Oct 22",
           "expected_end_date": "Oct 23",
           "invoice_note": "note",
           "sale_note": "note",
           "maintainance_note": "note",
           "sim_number": "123",
           "signnage_id": "456",
           "condition_id": "1",
           "user_id": "1"
           }
   ]
}
```


so just forget array of order_item  and attachment.

add like this below

```json
{
   "order_info": [
       {
           "start_date":  "Oct 20",
           "end_date": "Oct 21",
           "expected_start_date": "Oct 22",
           "expected_end_date": "Oct 23",
           "invoice_note": "note",
           "sale_note": "note",
           "maintainance_note": "note",
           "sim_number": "123",
           "signnage_id": "456",
           "condition_id": "1",
           "user_id": "1"
           }
   ],
   "order_item": [{
       
   }],
   "attachment": [{
       
   }]
}
```



### table already exist when i run migration

Add this code in migration file

```php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        if (Schema::hasTable('users')) {
            // テーブルが存在していればリターン
            return;
        }
        Schema::create('users', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name');
            $table->string('email')->unique();
            $table->string('password', 60);
            $table->rememberToken();
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop('users');
    }
}
```

in case want to skip column, like this

```php
Scheme::hasColumn('tablename', 'columnname')
```



# Create Table

## create migration file

```
php artisan make:migration create_product_types_table
```

If you type above command, and then it must be created migration file in database/migrations

2. See inside of the file you created

It should be like this below.

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateProductTypesTable extends Migration
{

    public function up() //add new table or column into database
    {
        Schema::create('product_types', function (Blueprint $table) {
            $table->id();
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('product_types');
    }
}
```

#### SQLSTATE[HY000]

General error: 1215 Cannot add foreign key contraint (SQL: alter table 'product_list' add contraint 'products_list_product_types_id_foreign' foreign key ('product_types_id') references 'product_types' ('id'))

In General, this error occurs the type of foreign key and reference key are different. If u positive u did not mistake, u should check ur phpmyadmin and see structure. In my case, I mistook bigint and int of id.

SQLSTATE[23000]

SQLSTATE[23000] Integrity constraint violation: 1452 Cannot add or update a child row: a foreign key constraint fails

solution1 ---> https://ja.stackoverflow.com/questions/66169/laravel



# Create API

## Make Model

```
php artisan make:model MODELNAME -m
```

The `-m` option is short for `--migration` and it tells Artisan to create one for our model. Here’s the generated migration:

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateArticlesTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('articles', function (Blueprint $table) {
            $table->increments('id');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('articles');
    }
}
```

- The `up()` and `down()` methods will be run when we migrat e and rollback respectively;

  then, run

  ```
  php artisan migrate
  ```

#### In case you run php artisan make:migration ....

You also have to create a model...

run

```
php artisan make:model NAME
```

#### fillable

use it ain't change the value in DB. It is similar to guarded.

DIFFERENCES ---

fillable --> whitelist guarded --> blacklist.

```php
$fillable = ['name', 'company'] // able to edit the value.
```



# REST API tuto

## migration



### index

to add index 

run this command in workspace

```
php artisan make:migrate migrationfilename --table=tablename
```

then edit migration file

```
$table->index('column name');
```

and

```
php artisan migrate
```

that is all.

### hasMany



```php
public function modelname 
{
	return $this->hasMany('App\modelname')
}
```



### belongsTo



```php
public function modelname
{
	return $this->hasMany('App\modelname')
}
```



or 



```php
public function modelname
{
	return $this->belongsTo(MODEL::class);
}
```



I got error when i wrote the above one.

## Model

```
php artisan make:model name -mf
```

automatically create both migration file and factory file

```
php artisan migrate
```

## Factory

edit factory

## Seeder

```
php artisan make:seed nameSeeder
```

edit seeder file and then edit databaseSeeder to add what you make.

## API URL

edit Route.



## Controller

```
php artisan make:controller nameController
```

## Resource (show)

api json -> one array is better for front-end. like data{}

```
php artisan make:resource OrderResource
```

edit Resource file and also edit Controller file to array



## Collection (index)

```
php artisan make:resource OrderResourceCollection --collection
```

just resource ---> jsonResource (normal)

collection -->  Resource collection (for index)



## Store

make store public function in Controller and also add fillable to Model.



## Update

controller -> 

put is json in row.(postman)



#### fill

#### (Laravel) fillを使ってモデルの複数カラムを更新する

https://qiita.com/tkt989/items/c2e01ec2fe91ef5f08d2

### === references ===

#### LaravelのORMで初心者から職人へ

https://qiita.com/henriquebremenkanp/items/cd13944b0281297217a9





# make controller

run this command

```php
php artisan make:controller NAME --api
```

\*optional --> put --api the last of the command = it automatically create function for api

it will be like this below ...

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class OrdersController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function show($id)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function update(Request $request, $id)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function destroy($id)
    {
        //
    }
}
```

---> complete!

finally put routing in ur api route file.,,,

```php
//api.php

Route::apiResource('table name', 'controller name')
// this url can be working... access /api/table name
```

## Faker

To decide the type of dammy data, you need factory.php

faker is prepared for insert dammy data

```
php artisan make:factory NameFactory
```

```php
<?php

/** @var \Illuminate\Database\Eloquent\Factory $factory */

use App\Model;
use Faker\Generator as Faker;

$factory->define(App\Http\Models\Orders::class, function (Faker $faker) {

    return [
        'start_date' => $faker->dateTimeThisMonth(),
        'end_date' => $faker->dateTimeThisMonth(),
        'expected_start_date' => $faker->dateTimeThisMonth(),
        'expected_end_date' => $faker->dateTimeThisMonth(),
        'invoice_note' => $faker->sentence,
        'sale_note' => $faker->sentence,
        'maintainance_note' => $faker->sentence,
        'sim_number' => $faker->numberBetween(1, 100),
    ];
});
```

https://qiita.com/tosite0345/items/1d47961947a6770053af#

#### --- faker cheetsheet. this is useful

## Database Seeding

Database seeding is the process of filling up our database with dummy data that we can use to test it. Laravel comes with [Faker](https://github.com/fzaninotto/Faker), a great library for generating just the correct format of dummy data for us. So let’s create our first seeder:

```
php artisan make:seeder NAMETABLESeeder
```

#### === references ===

[LaravelでFactoryとSeederを使ってダミーデータを追加する簡単な例](https://hubarifront.hatenablog.com/entry/2019/05/10/130008)

https://hubarifront.hatenablog.com/entry/2019/05/10/130008

# test



## structure of tests

- tests
  - Feature
  - Unit
  - Fixture
  - Lib

Feature ---> for a whole API test.

Unit ---> test of per class. 

Fixture ---> write data for test.

Lib ---> store some basic class for some tests.



each test code should write in other files.  create files each domain.  and the file name is [domain name]Test.php

for example..

Feature/Chat/RoomTest.php

also function name is same. ---> Test



## Create database for test

```sql
mysql> create database laravel_test;
```



## make .env for test

```
cp .env.example .env.testing
```

THEN, change those two 

```
// testing
APP_ENV=testing

// change to the name of database you created for test
DB_DATABASE=laravel_test
```



## create APP_KEY for test

```
php artisan key:generate --env=testing
```

Application key set successfully --> check .env.testing

you must be got APP_KEY

---> to be continue to PHPUnit ....

# PHPUnit

Change phpunit.xml like this below

```
<env name="DB_connection" value="mysql"
```



## migrating for test db

```
php artisan migrate --env=testing
```

THEN, check it works or not.



## Create Feature file for test

```
php artisan make:test Api/AdminUserTest
```

check the file successfully created or not.



## implement sh file

laravel has cache to move fast as they can, so they recommended officially to use php artisan config:clear

thus make this file that is test.sh

```sh
//test.sh
#!/bin/bash

php artisan config:clear
./vendor/bin/phpunit tests/Feature/Api
```

then run this command

```
chmod +x test.sh //only needs first time
./test.sh
```



## create admin test account

for prepare like that, you should use factory.

```
php artisan make:factory --model=AdminUser
```

then edit database/factories/AdminUserFactory.php.

But in case of ordermanagement system, I've already have like that file, so i will use that.

that file should be like this

```php
<?php

/** @var \Illuminate\Database\Eloquent\Factory $factory */

use App\AdminUser;
use Faker\Generator as Faker;

$factory->define(AdminUser::class, function (Faker $faker) {
    static $password;

    return [
        'name' => $faker->name,
        'email' => $faker->unique()->safeEmail,
        'email_verified_at' => now(),
        'password' => $password ?: $password = bcrypt('secret'),
        'remember_token' => Str::random(10),
    ];
});
```



## Add index ( all data ) test case in tests/Feature/Api/AdminUserTest.php



```php
<?php

namespace Tests\Feature\Api;

use App\AdminUser;

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithFaker;
use Tests\TestCase;

class AdminUserTest extends TestCase
{
    // テストデータのリセット
    use RefreshDatabase;
    // ミドルウェアの無効化
    use WithoutMiddleware;

    private $adminUser;

    public function testIndex()
    {
        // テストデータをFactoryで作成
        $adminUser1 = factory(AdminUser::class)->create();
        $adminUser2 = factory(AdminUser::class)->create();

        $response = $this->json('GET', '/api/admin_users');
        $response
            ->assertStatus(200)
            ->assertJson(
                [
                    [
                        'id' => $adminUser1->id,
                        'name' => $adminUser1->name,
                        'email' => $adminUser1->email,
                    ],
                    [
                        'id' => $adminUser2->id,
                        'name' => $adminUser2->name,
                        'email' => $adminUser2->email,
                    ]
                ]
            );
    }
}
```



in laravel,  they have popular things that provide as trait.

in this case above, RefreshDatabase and WithoutMiddleware.

## run test command	(tinker)

the preparation for test is above all.

run 

```
php artisan tinker --env-testing
```

then,

```php
App\Orders::all() //example
```

if return 

```php
Illuminate\Database\Eloquent_Collection {#3156
	all:[],
}
```

it works.



## run test command (phpunit)

want to test all of the file --> on top directory, run 

```
phpunit or ./vender/bin/phpunit
```

wanto to test specific file --> run this

```
phpunit tests/Feature/()()ControllerTest.php 
```



## ==== Error =====

### phpunit error -- Access denied for user `oooo' @ '%'  to database 

```
GRANT ALL TO test_db_name.* TO user;
```

I tried above command to include user into accessable to test db. but it is does not work somehow. 

this time, i found phpunit.xml is something wrong....

```
<server name='DB_DATABASE' value=':memory'/> ---> error content said username is not able to connect :memory db. so I guess I should revise that.
```



### InvalidArgumentException: Unable to locate factory for [].

Just create factory is working well.



### Response status code [500] does not match expected 200 status code. Failed asserting that false is true



# Useful commands ( + explaination)

## php artisan tinker



===

references ---> 

Laravel 標準搭載のデバッグ機能 tinker コマンドのご紹介

https://qiita.com/ucan-lab/items/0e9537be6d5709e1d099

===

# Postman



## To know what error occurs

set Headers.

Key ---> Accept , and Value--->application/json

Key---> Content-Type, and Value--->application/json



## $this->withoutExceptionHandling()

in case you are not trying to attempt irregular moving test, add this code.

it stop test with irregular and phpunit tells us what error is occuring.

=== references ===

https://teratail.com/questions/225665



# Route

## check route list

```
php artisan route:list
```



# Composer



## === error ===

### Error: Class ()()()() not found

#### solution 1

usually this error occur when u change class name. that is because in Laravel, they have autoloader so composer manage class. To tell the change of class name, run

```
composer dump-autoload
```

### composer dump-autoload error ( skipping )

class name should make the same format as its file name.

for example, if file name is App\Http\Models\Orders, 

```
namespace App\Http\Models\Orders // wrong
namespace App\Http\Models //correct.

class Orders ~~~~
```

### ==== reference ====

https://teratail.com/questions/198159

=================



# Repository



### ==== refernce =====

#### リポジトリパターンと Laravel アプリケーションでのディレクトリ構造

https://qiita.com/karayok/items/d7740ab2bd0adbab2e06

=================



# Eloquent

## get data

### MODEL::all()

get all data from database but it does not sort by options like desc or asc.

```
USER::all();
```



### MODEL::orderby('value', 'desc')

```
USER::orderBy('created_at', 'desc')
```

in general, to take data from database, put first() or get() at the last of code



### MODEL::SELECT('')

```
USER::select('name')
```

In case above, only data that have column name is picked 



### MODEL::where(''. Value )

```
USER::where('name', $name);
```



# DRAG AND DROP

https://teratail.com/questions/37281https://teratail.com/questions/37281

priority(優先度)のカラムを追加

既存データに1000単位でデータを入れていく(1レコード目は1000、²レコード目は2000)

入れ替えが発生したとき前後のpriorityを半分の値にして更新をかける

前後のpriorityの値が1になってしまったとき全レコードを1000単位で振り分けし直す(定期的な更新でも良い)



# Jwt-token refresh

Jwt tokenでauth認証を行った時にtokenの有効期限を自動更新するAPI

```php
// controller
public function refresh() {
    return $this->respondWithToken(Auth::guard('api')->refresh());
}
```

APIルートの修正

```php
// api.php

...
Route::group(['middleware' => 'auth:api'], function(){
    ...
    Route::get('refresh', 'JWTAuthController@refresh')->name('api.jwt.refresh');
    ...
});
...
```



POSTMANで

- Url --> API path/api/refresh
- header -> Autorization, Bearer jwt_token

で新しいjwt tokenが帰ってくるかを検証。

# File Upload

## [The Local Driver](https://laravel.com/docs/8.x/filesystem#the-local-driver)

###### When using the `local` driver, all file operations are relative to the `root` directory defined in your `filesystems` configuration file. By default, this value is set to the `storage/app` directory. Therefore, the following method would write to `storage/app/example.txt`:

```php
use Illuminate\Support\Facades\Storage;

Storage::disk('local')->put('example.txt', 'Contents');
```



best API reference

https://reffect.co.jp/laravel/laravel-storage-manipulation-master#i-3





== reference ==

https://stackoverflow.com/questions/40129372/laravel-how-to-send-image-or-file-to-api



## S3

#### laravelにS3を変更する

```php
composer require league/flysystem-aws-s3-v3
```

error == set version

```
composer require league/flysytem-aws-s3-v3 ~1.0
```



### ドライバ設定

config/filesystems.phpのAWS環境設定を編集

#### キャッシュ

s3の設定ファイルでキャッシュの設定可能。

```php
's3' => [
    'driver' => 's3',

    // Other Disk Options...

    'cache' => [
        'store' => 'memcached',
        'expire' => 600,
        'prefix' => 'cache-prefix',
    ],
],
```

### S3の一時的なURL　temporaryUrl method

```php
$url = Storage::temporaryUrl(
    'file.jpg', now()->addMinutes(5)
  	// file path + DateTime instance
);
```

#### Response header options

```
response-content-type
	// application/octet-stream
response-content-language //jp
response-expires //
```



### S3 file upload special settings

laravel putfile methodで設定が可能

```php
Storage::putFile('model name', new File('/path/to/'), 'public')
```

### set file name w S3

```php
$file = $data->file('file_path')->storeAs(
	'file_paths', $data->order()->id, 'S3'
)
```

### S3 delete file

```php
Storage::disk('s3')->delete('file_path/file_name)')
```

#### === reference ===

#### Laravel 5.8 file storage

https://readouble.com/laravel/5.8/ja/filesystem.html



### display s3 file infomation on brawser

ブラウザでURLを叩いたときのエラー。

```
This XML file does not appear to have any style information associated with it. The document tree is shown below.
＜Error＞
＜Code＞AccessDenied＜/Code＞
＜Message＞Access Denied＜/Message＞
＜RequestId＞7F91C2D657A3B816＜/RequestId＞
＜HostId＞
TsFf5WHTPoU6ddu6mSJ3EOWPjcxfLzzC/OQPYl2aDi8i1mHItmKdMqVR0y3Qa/WFcXatifPiGHE=
＜/HostId＞
＜/Error＞
```

考えられる原因

・S3のバケットポリシー

・CloudFrontからのみのアクセス設定(今回はなし)



get all files list on s3

```php
// ファイル一覧
$list = Storage::disk('s3')->files('');

//下の階層のファイル一覧も取得
$list = Storage::disk('s3')->allFiles('');
```



### ファイル名が異なって保存

s3では本来のファイル名で保存されているのにphpmyadminでは自動生成された名前で保存されてしまう。

保存している関数の一つの例

```php
    /**
     * @param array $orderItem
     * @param string $orderId
     */
    public function update(array $orderItem, string $orderId)
    {
        try {
            DB::beginTransaction();

            $order_item = $this->order_item->where('order_id', $orderId)->first();

            //見積書がセットされていたら実行
            if (isset($orderItem['quotation'])) {
                if (!preg_match('/null/', $orderItem["quotation"])) {
                    $quotation_name = $orderItem['quotation']->getClientOriginalName();
                    Storage::putFileAs('/public', $orderItem["quotation"], $quotation_name);
                }
            }

            //注文書がセットされていたら実行
            if (isset($orderItem['invoice'])) {
                if (!preg_match('/null/', $orderItem["invoice"])) {
                    $invoice_name = $orderItem['invoice']->getClientOriginalName();
                    Storage::putFileAs('/public', $orderItem["invoice"], $invoice_name);
                }
            }

            // 見積もり部がなければ作成
            if (!$order_item) {
                $order_item = new OrderItem;

                if (isset($orderItem['quotation'])) {

                    if (!preg_match('/null/', $orderItem["quotation"])) {
                        $quotation_name = $orderItem['quotation']->getClientOriginalName();
                        Storage::putFileAs('/public', $orderItem["quotation"], $quotation_name);
                    }
                }

                if (isset($orderItem['invoice'])) {
                    if (!preg_match('/null/', $orderItem["invoice"])) {
                        $invoice_name = $orderItem['invoice']->getClientOriginalName();
                        Storage::putFileAs('/public', $orderItem["invoice"], $invoice_name);
                    }
                }

                $order_item->fill(array_merge($orderItem, ["order_id" => $orderId]))->save();
            }

            $order_item->fill($orderItem)->save();

            DB::commit();
        } catch (\Throwable $th) {
            DB::rollBack($th);
        }
    }
}

```

phpmyadminでファイル名を確認->自動生成された文字列(以前から挙動は変化していない。)

s3では指定したファイル名(この関数の場合アップロードしたファイル名を取得して保存している)でしっかりと保存されている。

原因

Storage::putFileAsでgetClientOriginalNameで取得したファイルをs3に保存していたから満足していたが、dbへの保存はfill->save()で行っていた。そのためファイル名はdb上だと自動生成文字列でcommitされていた。

なのでfillの時にarray_merge

```php
$order->fill(array_merge($order, ['file' => $file_name]))->save();
```



# Orderby null last

ASCでカラムを並べ替えした場合、MYSQLの仕様だとnullが一番上になる。

nullを一番下にしたい場合は

```
->orderByRaw('column name IS NULL ASC') // add
->orderBy('column name', 'asc')
```



# Array_mergeのわな

nullや''をarray_mergeするとarrayが全てからになってしまう。

空の配列をセットして入れてあげないと結果すべて上書きされてしまう。

```php
            if (!preg_match('/null/', $orderItem["file_path"])) {
                $file_one_name = $orderItem['file_path']->getClientOriginalName();
                $file_one = ['file_path' => $file_one_name];
                Storage::putFileAs('/public', $orderItem["file_path"], $file_one_name);
            }
            if (isset($orderItem['file_path_two'])) {
                if (!preg_match('/null/', $orderItem["file_path_two"])) {
                    $file_two_name = $orderItem['file_path_two']->getClientOrinalName();
                    $file_two = ['file_path_two' => $file_two_name];
                    Storage::putFileAs('/public', $orderItem["file_path_two"], $file_two_name);
                }
            } else {
                $file_two = array();
            }
            if (isset($orderItem['file_path_three'])) {
                if (!preg_match('/null/', $orderItem["file_path_three"])) {
                    $file_three_name = $orderItem['file_path_three']->getClientOriginalName();
                    $file_three = ['file_path_three' => $file_three_name];
                    Storage::putFileAs('/public', $orderItem["file_path_three"], $file_three_name);
                }
            } else {
                $file_three = array();
            }

            $files = array_merge($file_one, $file_two, $file_three);
            $order_item->fill($files)->save();
```

