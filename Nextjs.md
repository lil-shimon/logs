[TOC]

## Dynamic Routes

1. create `[id].tsx` under folder
2. **getStaticPaths** which returns an array of possible value for **id**
3. **getStaticProps** which fetches necessary data for the post with **id** 

```tsx
import Layout from "../components/layout"

export default function Post () {
    return <layout>....</layout>
}

export async function getStaticPaths () {
    //return a list of possible value for id
}

export async function getStaticProps ({params}) {
    //return necessary data for the post using params.id
}
```



## ページ遷移

### Next/link

```react
<Link href="/">
    <a>something</a>
</Link>

import Link from "next/link"
```

### next/router

```typescript
import { useRouter } from "next/router"

function example () {
    const handleClick = (e) => {
        e.prevent.Default()
        router.push("url")
    }
}
```

## implement loading screen w next js

The only needs of implementing loading on nextjs app is changing  _app.tsx

```react
_app.tsx

import React, { useEffect } from 'react'
import { AppProps } from 'next/app'
import nprogress from 'nprogress' // Import NProgress
import 'nprogress/nprogress.css' // Import default styles of bar
import '../styles/globals.css'

// setting of bar
//showSpinner: display loading spinner w bar or not
// speed: The time of disappearing bar
// minimum: The start point of bar
nprogress.configure({ showSpinner: false, speed: 400, minimum: 0.25 })

const App: React.FC<AppProps> = ({ Component, pageProps }) => {
  if (process.browser) {
      // Start displaying of bar
    nprogress.start()
  }

  useEffect(() => {
      // Finish displaying of bar
    nprogress.done()
  })

  return <Component {...pageProps} />
}

export default App
```



## PDF

### jsPDF

next jsでPDFを出力

```
npm install jspdf
```

```react
import React from 'react';
import jsPDF from 'jspdf';
import { Button } from '@material-ui/core';

export default function() {
  //jsPdf Generator function
  const jsPdfGenerator = () => {
    //new document in jsPdf
    const doc = new jsPDF('p', 'pt');

    //add some text to pdf document
    doc.text('this is defautl text', 20, 20);

    //set the font of pdf document
    doc.setFont('courier');

    doc.text('this is text with courier font', 20, 20);

    //save the pdf document
    doc.save('generated.pdf');
  };

  // making the render function of the component
  return <Button onClick={jsPdfGenerator}>Generate PDF</Button>;
}

```

チュートリアルとしてはこんな感じ

この状態だとテキストでしかPDFを出力できない。しかもプレビューのような感じでどのような画面なのかも確認できない。

ボタンを押したら設定しているデータがPDFとしてダウンロードされる感じ。



#### jsPDf heavy

There are some solutions.

```
pdf.addImage(imgData, 'PNG', 0, 0, width, height, 'undefined', 'FAST')
```



```

```



### jsPDF / html2canvas

上記の問題を解決したのがこの２つの組み合わせ。

html2canvasはページをスクリーンショットみたいな感じでキャプチャーするJSライブラリ。

それをjsPDFでPDFとして出力している感じ。

```
yarn add jspdf
yarn add html2canvas
```

チュートリアルのソースコード↓

gitのブランチ名はpdfで保存してあるので、迷ったらここを参照。

ここではclassで書いてしまったのでfunctionで書き直そう。

```react
import React, { Component } from 'react';
import jsPDF from 'jspdf';
import { Button } from '@material-ui/core';
import html2canvas from 'html2canvas';

class Invoice extends Component {
  handlePdf = () => {
    const input = document.getElementById('page');

    html2canvas(input).then(canvas => {
      const imgData = canvas.toDataURL('image/png');
      const pdf = new jsPDF('p', 'px', 'a4');
      const imgProps = pdf.getImageProperties(imgData);
      const width = pdf.internal.pageSize.getWidth();
      const height = (imgProps.height * width) / imgProps.width;

      pdf.addImage(imgData, 'JPEG', 0, 0, width, height);
      pdf.save('test.pdf');
    });
  };

  render() {
    const hrStyle = {
      border: '5px solid rgb(23, 162, 184)',
    };

    return (
      <React.Fragment>
        <div className="col-12 col-lg-6" id="page">
          <div className="container-fluid bg-info text-white">
            <div className="row">
              <div className="col text-left m-2">
                <p>Your Company Name</p>
                <h2>Invoice</h2>
              </div>
              <div className="col text-right">
                <p>22 Yusen St</p>
                <br />
                <p>borburn</p>
                <br />
                <p>WSN</p>
              </div>
            </div>
          </div>
          <div className="container-fluid">
            <div className="row">
              <div className="col-4">
                <h5>Billed To</h5>
              </div>
              <div className="col-4">
                <div>
                  <h5>Invoive number</h5>
                  <p>Za{Math.floor(Math.random() * 100 + 1)}</p>
                </div>
                <div>
                  <h5>Date</h5>
                </div>
              </div>
              <div className="col-4">
                <div>
                  <h5>Invoice Totals</h5>
                </div>
              </div>
            </div>
          </div>
          <hr style={hrStyle} />
          <div className="Invoices">
            <table className="table">
              <thead>
                <tr>
                  <th>Description</th>
                  <th>Unit Price</th>
                  <th>Quantity</th>
                  <th>Total</th>
                </tr>
              </thead>
              <tbody />
            </table>
          </div>
          <hr />
        </div>
        <button
          onClick={this.handlePdf}
          className="btn btn-primary btn-lg mx-auto"
        >
          Generate PDF
        </button>
      </React.Fragment>
    );
  }
}

export default Invoice;

```

### HTML2canvas

#### 画質を上げる

```react
html2canvas(input, {
    scope: 6, //数字の数を上げていく。効果あり。
    dpi: 192, //効果は検証していないが、公式によるとあるらしい。数字の上げ方もいまいちわからない。
})
```



## Web performance

### reportwebVitals

```
//_app.ts

export function reportWebvitals (metric) {
	console.log(metric)
}
```

that function let me know about page performance.





## Error

スクロールして下の方にボタンを置くと半分切れたようなPDFが出来上がる。

解決策としては一番上に作成ボタンを置く。



#### build failed because of webpack error





### next: command not found 

```
npm upgrade
```



## an unexpected error has occured

backendのshell scriptを実行した後に特定のページだけアクセスできなくなった。

dockerをbuildし直しても効果なし

本番環境も開発環境も同じエラーはなし(検証環境だけ)

#### 原因

shell scriptを実行した際にseederが生成されてdatabaseにない外部キーidのデータが生成されたことが問題。

データを削除することで問題なく表示された。