# Invalid HTTP_HOST header: '0.0.0.0:8000'. You may need to add '0.0.0.0' to ALLOWED_HOSTS.

Run serverをしたときのエラー

Settings.pyで設定すれば良い。

```
ALLOWED_HOSTS = ['0.0.0.0']
```

