# migration

## create model

```python
class Task(models.Model):
    title = models.CharField(max_length=50)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return str(self.id) + " - " + self.title
```

Then, run 

```
python manage.py makemigrations
python manage.py migrate
```

# serializer

Serializer は データ の入出力を扱い、モデルへの橋渡しをするクラス。

# superuser

```
python manage.py createsuperuser
```



# pip freeze

プロジェクトで使っているモジュールの一覧を出力してくれるコマンド

```
pip freeze > requirements-dev.txt
```



# Invalid HTTP_HOST header: '0.0.0.0:8000'. You may need to add '0.0.0.0' to ALLOWED_HOSTS.

Run serverをしたときのエラー

Settings.pyで設定すれば良い。

```
ALLOWED_HOSTS = ['0.0.0.0']
```



# git add . killed

in case django app, you have to add venv dir into git ignore file. otherwise you will get this error.

Or 

```
Another git process seems to be running in this repository, 
e.g. an editor opened by 'git commit'. Please make sure all 
processes are terminated then try again. 
If it still fails, a git process may have crashed in this 
repository earlier: remove the file manually to continue.
```

