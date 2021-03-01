

[TOC]

## Type ~array, Object~

### Pick

TypescriptでPickを使える場面が出たので採用。

一覧表示するときとPostするときのオブジェクトの必要量が違うので別々で定義。

今までは型Postage(Product)ほどの必要量がないときは個別に定義していた。（そこでPostage型を定義してしまうと要素が足りないとエラーが出てしまうため）

```typescript
export type Postage = {
  id: number;
  sender_place: string;
  destination_place: string;
  postage_price: number;
  size: any;
  tax: string;
  number: number;
}; //オブジェクトのPostage型を定義

export type PostPostage = Pick<
  Postage,
  'sender_place' | 'destination_place' | 'size' | 'number' | 'postage_price'    //Postage型のなかのこの5つだけを選択
>;

export type Product = {
  id: number;
  name: any;
  unit: string;
  unit_price: number;
  tax: string;
  quantity: number;
};

export type PostProduct = Pick<
  Product,
  'name' | 'unit' | 'unit_price' | 'quantity'
>;
```

TypeError : toLowerCase of null

When you use autoComplete from material-ui, you can set some options for them.  That error means the option's array has object of null, but it is not permitted from material-ui. For this error, you have to remove object of null yo use this function.

```react
  //配列からnullを削除
  const newTermAndConditions = documents.map(
    (d: { term_and_conditions: any }) => {
      if (d.term_and_conditions !== null) {
        return d.term_and_conditions;
      } else {
        return ''
      }
    }
  );

  //配列から''を削除
  const newDocument = [...newTermAndConditions];
  for (let i = 0; i < newDocument.length; i++){
    if (newDocument[i] === '') {
      newDocument.splice(i, 1)
    }
  }

  //かぶっている要素を削除
  let uniqueTermAndConditions = [...new Set(newDocument)];

    <Autocomplete
      id="document-term_and_conditions"
      options={uniqueTermAndConditions} --> It works
      freeSolo
      disableClearable
      value={term_and_conditions}
      onInputChange={newInputValue =>
        handleChangeTermAndConditions(newInputValue)
      }
      renderInput={params => (
        <TextField
          {...params}
          label="契約条件"
          value={term_and_conditions}
          fullWidth
          inputProps={{ ...params.inputProps, type: 'search' }}
          onChange={e => handleChangeTermAndConditions(e.target.value)}
        />
      )}
    />
```

### Ignore all typescript errors

the file you want to ignore the typescript checking, you just add following this description.

```
/// <references no-default-lib='true' />
```

edit ts.config

```
{
  "compilerOptions": {
    "skipDefaultLibCheck": true
  }
}
```

or you add just this description

```
// @ts-ignore
```

But unfortunately it only works for lines. so you will end up putting loads in.

if you want to use this, you add script like this

```
{/* @ts-ignore */}
```



### Manage the type of process.env

initially, that type is

```typescript
interface ProcessEnv {
	[key: string]: string | undefined;
}
```

make global.d.ts and write like this...

```typescript
declare global {
  namespace NodeJS {
    interface ProcessEnv {
      GITHUB_AUTH_TOKEN: string;
      NODE_ENV: 'development' | 'production';
      PORT?: string;
      PWD: string;
    }
  }
}
```

OR, only in case of using process.env as string, you just write

```
const example = process.env['EXAMPLE'] //string
```



## Css module in TS

```
const styles = require('/....')
```

## funcional type 

#### void

void -> there is no return

```typescript
export const message = (message: string): void => {
	console.log('message is' message)
} 
```

#### function have default parameter

```typescript
export const isUserSignedIn = (userId: string, username = 'no name'): boolean => {
    if (userId === id) {
        	console.log('function parameters sample: user is sigined in. username is' username)
    		return true
    }
	else {
        console.log('function parameters sample: user is not signed in.')
        return false
    }
}

isUserSignedIn(id) //function parameters sample: user is sigined in. username is no name
isUserSignedIn(dd) //function parameters sample: user is not signed in.
```

#### function have optional parameter

notice! parameters that have optional must be the last of paramters and it needs "?"

```typescript
export const isUserSignedIn = (userId: string, username?: string): boolean => {
    if (userId === id) {
        	console.log('function parameters sample: user is sigined in. username is' username)
    		return true
    }
	else {
        console.log('function parameters sample: user is not signed in.')
        return false
    }
}

isUserSignedIn(id, kenta) //function parameters sample: user is sigined in. username is kenta
isUserSignedIn(dd) //function parameters sample: user is not signed in.
```

#### function that have rest parameters

reduce method -> 

[]: 



```typescript
export const sumProductPrice = (...productsPrice: number[]): number => {
    return productsPrice.reduce((prevTotal, productPrice) => {
        return prevTotal + productsPrice
    }, 0)
}

sumProductPrice(100, 200, 300, 400)
```

#### Call type signature

it is for function

```typescript
type logmessage = (message: string) => void

export const logMessage = (message) => {
	console.log('function sample', message)
}
```

## Check error log

```
Argument of type '({ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; } | { sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number; })[]'

 is not assignable to parameter of type 

'SetStateAction<{ name: string; unit: string; unit_price: number; number: number; id: number; tax: string; productPrice: number; notes: string; }[]>'.
  Type '({ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; } | { sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number; })[]'

 is not assignable to type 

'{ name: string; unit: string; unit_price: number; number: number; id: number; tax: string; productPrice: number; notes: string; }[]'.
    Type '{ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; } | { sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number; }' 

is not assignable to type

 '{ name: string; unit: string; unit_price: number; number: number; id: number; tax: string; productPrice: number; notes: string; }'.
      Type '{ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; }' 

is missing the following properties from type

 '{ name: string; unit: string; unit_price: number; number: number; id: number; tax: string; productPrice: number; notes: string; }': name, unit, unit_price, number, and 2 more.ts(2345)
```



```react
Argument of type '({ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; } | { sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number; })[]' is not assignable to parameter of type 'SetStateAction<{ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; }[]>'.

  Type '({ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; } | { sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number; })[]' is not assignable to type '{ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; }[]'.

​    Type '{ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; } | { sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number; }' is not assignable to type '{ senderPlace: string; destinationPlace: string; size: string; id: number; tax: number; postagePrice: number; quantity: number; }'.

​      Type '{ sender_place: string; destination_place: string; size: string; id: number; tax: number; postage_price: number; quantity: number;
```



## 自作Params, Query関数で複数クエリ対応（複数QUery string parameters）

```typescript
const get = (path: string, params: string[] = [], query: string[][] = []) => {
  return {
    fetch: async () => {
      let pathParams = '';
      if (params.length) {
        pathParams = `/${params.join('/')}`;
      }
      return axios.get(`${API_URL}${path}${pathParams}`, {
        params: query.reduce((hs: Record<string, string>, param: string[]) => {
          //hsを複数指定すればURLの後ろに追加可能。
          //http://localhost/api/order?page=1&order_by=company_name_asc&query=15
          //query1(first hs) = $order_by=company_name 
          //query2(second hs) = $query=15
          //になる
          hs[param[0]]= param[1], hs[param[2]] = param[3];
          return hs;
        },  {}),
      });
    },
    bindParams: (...args: string[]) => get(path, [...params, ...args], query),
    bindQuery: (...args: string[][]) => get(path, params, [...query, ...args]),
  };
};
```

