## LINE notify

プログラミンググループへのアクセストークン

MLT8ZR5McAM1hYpydpcTb9M9jUttlbVl03qJeAqTGIF

LKYvxRI4TjrGwMMb1KMW3UQfkUZ577NPfOdF

とりあえずJSで描いてみた

```javascript
const axios = require('axios');
const qs = require('querystring');

const LINE_NOTIFY_API_URL = 'https://notify-api.line.me/api/notify';

const LINE_NOTIFY_TOKEN = MLT8ZR5McAM1hYpydpcTb9M9jUttlbVl03qJeAqTGIF;

let config = {
	url: LINE_NOTIFY_API_URL,
	method: 'post',
	headers: {
		'Content-Type': 'application/x-www-form-urlencoded',
		Authorization: 'Bearer ' + LINE_NOTIFY_TOKEN,
	},
	data: qs.stringify({
		message: '自動化のテストしてます',
	}),
};

async function getRequest() {
	try {
		const responseLINENotify = await axios.request(config);
		console.log(responseLINENotify.data);
	} catch (error) {
		console.error(error);
	}
}

getRequest();
```

node line.jsを叩くとエラー。

```
➜ node line.js 
internal/modules/cjs/loader.js:834
  throw err;
  ^

Error: Cannot find module 'axios'
Require stack:
- /home/lilshimon/project/line.js
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:831:15)
    at Function.Module._load (internal/modules/cjs/loader.js:687:27)
    at Module.require (internal/modules/cjs/loader.js:903:19)
    at require (internal/modules/cjs/helpers.js:74:18)
    at Object.<anonymous> (/home/lilshimon/project/line.js:1:15)
    at Module._compile (internal/modules/cjs/loader.js:1015:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1035:10)
    at Module.load (internal/modules/cjs/loader.js:879:32)
    at Function.Module._load (internal/modules/cjs/loader.js:724:14)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:60:12) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [ '/home/lilshimon/project/line.js' ]
}
```

npm install axios is fine

next error is below

```
➜ node line.js 
/home/lilshimon/project/line.js:6
const LINE_NOTIFY_TOKEN = MLT8ZR5McAM1hYpydpcTb9M9jUttlbVl03qJeAqTGIF;
                          ^

ReferenceError: MLT8ZR5McAM1hYpydpcTb9M9jUttlbVl03qJeAqTGIF is not defined
    at Object.<anonymous> (/home/lilshimon/project/line.js:6:27)
    at Module._compile (internal/modules/cjs/loader.js:1015:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1035:10)
    at Module.load (internal/modules/cjs/loader.js:879:32)
    at Function.Module._load (internal/modules/cjs/loader.js:724:14)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:60:12)
    at internal/main/run_main_module.js:17:47
```

'' is working. I have to invite line notify in my group.

