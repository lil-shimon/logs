[TOC]



## 配列

### length

().lengtｈで要素の数を取得できる

```typescript
const documents = [
    "one",
    "two"
]

let length = documents.length
console.log(length)
// 2
```

### ~~連番の数字を作成~~

```javascript
const hours = [...Array(24).keys()]
```

上記のコードで実装した場合エラーがでる。

```markdown
Unhandled Runtime Error
TypeError: Invalid attempt to spread non-iterable instance.
In order to be iterable, non-array objects must have a [Symbol.iterator]() method.
```

正しい記述方法は

```typescript
const length = 2  

const tb = [...Array(length).map((_, i) => i)]
  console.log(tb)
// 2
```

### Sort

```javascript
    products.sort(function (a, b) {
      if (a.id > b.id) return -1
      if (a.id < b.id) return 1
      return 0
    })
```

実際に採用したコード

```react
    const sortProducts = products.sort(function (a, b) {
      if (a.id > b.id) return -1
      if (a.id < b.id) return 1
      return 0
    })
                  {sortProducts.map(product => (
                      ...
              ))}
```



## 時間

本日の時間系

```react
const today = new Date()
console.log(today.getDate()) // 2
const month = new Date()
console.log(month.getMonth() + 1) // 12
```

マイクロタイム

```react
const microtime = Date.now()
console.log(microtime) // 1606849608140
```

## string

```javascript
let sample = "abcd"
let result = sample.includes("c") //used it for search in words
```

数字列から文字列に変換

```javascript
const itemId = String(item.id)
```



## Calculation

### 少数を切り上げ

```react
const price = Math.floor(productPrice * postagePrice)
// Math.floor(number)
```

### 値段にコンマを適応

改善案で値段をコンマで区切ってほしいと依頼されたのでその備忘録

#### typescript

```typescript
const purchasedProducts = useSelector(getPurchasedProduct, shallowEqual);  
// purchasedProductはこんな感じの連想配列オブジェクト
// purchasedProduct = [
//{
   // name: example,
    //unit: example,
    //unit_price: example,
    //quantity: example,
    ~~~
//}
//]

 //配列をmapで新しい配列を作成してその中のunit_priceとquantityで１商品あたりの価格を算出
const productPriceList: number[] = purchasedProducts.map<number>(p => {
    const calc: number = Math.floor(p.unit_price * p.quantity);
    return calc;
  });
  const productPrice: number = productPriceList.reduce<number>(function(
    a: number,
    b: number
  ) {
    return a + b;
  },
  0);
  const addSeparator = (n: number) => {
    return String(n).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, '$1,'); //\はバックスラッシュ
  };
  const unitPrice = (n1: number, n2: number) => {
    let Price = Math.floor(n1 * n2);
    return String(Price).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, '$1,');
  };
//税抜き
  const Price = (n1: number, n2: number) => {
    let price = Math.floor(n1 + n2);
    return String(price).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, '$1,');
  };
//税
  const tax = (n1: number, n2: number) => {
    let price = Math.floor(n1 * 0.1 + n2 * 0.1);
    return String(price).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, '$1,');
  };
//税込
  const priceIncludeTax = (n1: number, n2: number) => {
    let price = Math.floor(n1 * 1.1 + n2 * 1.1);
    return String(price).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, '$1,');
  };
```

#### React

```react
export function productPriceField(){
return (
    <React.Fragment>
                {purchasedProducts.map(pp => (
                      ~~~
                    <TableCell className={classes.table}>
                      {addSeparator(pp.unit_price)}
                    </TableCell>
                    <TableCell className={classes.table}>
                      {unitPrice(pp.unit_price, pp.quantity)}
                    </TableCell>
                      ~~~
            ))}
	</React.Fragment>
 )}
 export function  priceField() {
   return (
         <React.Fragment>
                          ~~~
                  <TableCell className={classes.table}>
                    {Price(productPrice, postagePrice)}
                  </TableCell>
                <TableRow>
                    ~~~
                  <TableCell colSpan={2} className={classes.table}>
                    {tax(productPrice, postagePrice)}
                  </TableCell>
                    ~~~
                  <TableCell className={classes.table}>
                    {priceIncludeTax(productPrice, postagePrice)}
                  </TableCell>
~~~
    </React.Fragment>
  );
}


```

## reduce method

it only works on array

```typescript
export const sumProductPrice = (...productsPrice: number[]): number => {
    return productsPrice.reduce((prevTotal, productPrice) => {
        return prevTotal + productsPrice
    }, 0)
}

//prevTotal -> the result of the last calculation
//0 -> initial value of prevTotal
```

## IIFE

IIFE = **Immediately Invoked Function Expression**

normal function is like below

```javascript
function addTogether() {
 var x = 20;
 var y = 20;
 var answer = x + y;
 console.log(answer);
 }
addTogether();
```

IIFE function is like this

```javascript
(function() {
 var x = 20;
 var y = 20;
 var answer = x + y;
 console.log(answer);
 })(); 
```

To notice the end of function, the pair of brankets are needed.

---- reference https://medium.com/javascript-in-plain-english/how-to-use-async-function-in-react-hook-useeffect-typescript-js-6204a788a435

---- with useEffect ---> React 'how to use useEffect with async function'



## setTimeout

数秒後に処理をしたい時に使うメソッド

10秒後なら

```js
setTimeout(() => {
	// 処理
}, 10000)
```

useEffectと組み合わせて実装した。(flash message)(autoHideDurationで自動でスナック・バーを消すことはできるが、ページ遷移した時に遷移先でも新たに同じ通知が飛んでしまうため。)

```react
useEffect(() => {
	setTimeout(() => {
		dispatch(setFlashSuccess(''))
	}, 6000)
}, [])
```

