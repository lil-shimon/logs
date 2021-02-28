[TOC]

## edit page

1. 商品情報の一つ分のデータの取得



###                         ///>商品情報の一つ分のデータの取得

```react
import React, {useEffect} from "react"

export const example () {
    
    const [name, setName] = useState("")
    
    useEffect (() => {
        // 1. データの定義をして取得する処理
        const data = // take data
        // 2. それをセットする
        setName(data.name)
        ....
})
}
```

```react
if ( id !== "") {
// in case wanna get data of specific one
}

//like 
export const example () {
    useEffect (() => {
        if (id !== "") {
            /// sth
		}
    })
}
```

#### 連想配列の要素切り取り

```react
export const editDocuments = (
  pid: number,
): AppThunk => async (dispatch: AppDispatch) => {
  try {
    const { data } = await API.get("/document").fetch()
    dispatch(setDocuments(data))
    let editId = pid
    // this shows the list what the pid matches the data.id
    // and create new list that is only matching pid
    const editItem = data.filter((edit: { id: number; }) => {
      return editId === edit.id
    })
    console.log(editId)
      // this is pid 
    console.log(editItem)
      // this is pid's list
  } catch (err) {
    console.log(err);
  }
};
```

## PDF

### React-pdf

```
yarn add @react-pdf/renderer
npm install @react-pdf/renderer --save
```

初期画面のコード。これだけでPDFページ作成可能

```react
import React from 'react';
import { Page, Document, View, Text } from '@react-pdf/renderer';

const MyDocument = () => {
  return (
    <Document>
      <Page size="A4">
        <View>
          <Text>Section #1</Text>
        </View>
        <View>
          <Text>Section #2</Text>
        </View>
      </Page>
    </Document>
  );
};

export default MyDocument;
```



### ｈｔｍｌ−ｐｄｆ

```
git clone https://github.com/stanleyfok/nextjs-pdf.git
npm install
npm run dev
```

pdf page

```react
const Article = () => (
  <div>
    <h1>This is a sample article</h1>
    <img src="https://cdn.pixabay.com/photo/2016/09/21/04/46/barley-field-1684052_1280.jpg"/>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Purus non enim praesent elementum facilisis leo vel. Sodales ut eu sem integer vitae justo. Duis ultricies lacus sed turpis tincidunt id. Non arcu risus quis varius quam. Etiam non quam lacus suspendisse faucibus interdum posuere lorem ipsum. Feugiat vivamus at augue eget arcu. Aliquet porttitor lacus luctus accumsan tortor posuere ac ut consequat. Eget lorem dolor sed viverra ipsum nunc aliquet bibendum. Varius duis at consectetur lorem donec massa sapien faucibus et. Consequat nisl vel pretium lectus. Vitae suscipit tellus mauris a. Mauris nunc congue nisi vitae suscipit.</p>
    <p>Lobortis mattis aliquam faucibus purus. Sollicitudin tempor id eu nisl. Pellentesque elit ullamcorper dignissim cras tincidunt lobortis feugiat vivamus at. Vitae congue eu consequat ac felis donec et odio. Neque convallis a cras semper. Morbi tempus iaculis urna id volutpat. Dictum at tempor commodo ullamcorper. Tincidunt arcu non sodales neque sodales. Neque vitae tempus quam pellentesque. Ac felis donec et odio pellentesque diam. In ornare quam viverra orci sagittis. Orci nulla pellentesque dignissim enim. Nec nam aliquam sem et tortor. Sit amet nulla facilisi morbi. Nisl nisi scelerisque eu ultrices vitae auctor eu augue ut.</p>
    <p>Blandit aliquam etiam erat velit scelerisque in. Eget mi proin sed libero enim sed faucibus turpis. Sed tempus urna et pharetra pharetra massa massa ultricies mi. Mollis nunc sed id semper risus in hendrerit. Eget lorem dolor sed viverra ipsum nunc. Ullamcorper dignissim cras tincidunt lobortis feugiat vivamus at. Bibendum enim facilisis gravida neque convallis a cras. Elit pellentesque habitant morbi tristique senectus et netus. Sit amet nisl suscipit adipiscing bibendum est ultricies integer. Quam adipiscing vitae proin sagittis nisl rhoncus. Augue eget arcu dictum varius duis at consectetur lorem donec. Arcu ac tortor dignissim convallis aenean et tortor at risus. Cursus eget nunc scelerisque viverra mauris. Vitae aliquet nec ullamcorper sit amet risus nullam eget felis. Urna et pharetra pharetra massa.</p>
    <p>Ut sem viverra aliquet eget sit amet tellus. In fermentum posuere urna nec tincidunt praesent semper feugiat nibh. Neque vitae tempus quam pellentesque nec nam aliquam. Facilisis gravida neque convallis a. Consectetur a erat nam at lectus urna duis convallis. Felis bibendum ut tristique et. Est lorem ipsum dolor sit amet consectetur adipiscing elit. Velit dignissim sodales ut eu sem integer vitae justo. Varius sit amet mattis vulputate. Et malesuada fames ac turpis. Lobortis scelerisque fermentum dui faucibus in ornare quam. Enim sed faucibus turpis in eu mi bibendum neque egestas. Venenatis urna cursus eget nunc scelerisque viverra mauris in. Tristique et egestas quis ipsum. Ut diam quam nulla porttitor massa id neque aliquam. Arcu dictum varius duis at. Phasellus egestas tellus rutrum tellus pellentesque eu tincidunt tortor. Blandit cursus risus at ultrices mi tempus imperdiet.</p>
    <p>Imperdiet massa tincidunt nunc pulvinar sapien et ligula ullamcorper. Iaculis nunc sed augue lacus viverra vitae congue eu consequat. Hac habitasse platea dictumst quisque sagittis purus sit amet volutpat. Aliquam sem et tortor consequat. Vitae proin sagittis nisl rhoncus mattis. Augue lacus viverra vitae congue eu consequat. Vel facilisis volutpat est velit egestas dui id ornare. Quis eleifend quam adipiscing vitae proin sagittis nisl rhoncus mattis. Purus gravida quis blandit turpis cursus in hac habitasse platea. Tellus in metus vulputate eu scelerisque. Ornare suspendisse sed nisi lacus. Eu feugiat pretium nibh ipsum consequat. Eget egestas purus viverra accumsan in nisl nisi scelerisque eu. Eget egestas purus viverra accumsan in. Nibh nisl condimentum id venenatis a condimentum vitae. In nibh mauris cursus mattis molestie a. Tortor at risus viverra adipiscing at in. Sapien eget mi proin sed libero enim.</p>
  </div>
);

export default Article;
```

header and footer

```react
import React from 'react';
import PropTypes from 'prop-types';

const renderPDFFooter = () => (
  <div
    id="pageFooter"
    style={{
      fontSize: '10px',
      color: '#666'
    }}
  >
    This is a sample footer
  </div>
);

const PDFLayout = ({ children }) => (
  <html>
    <head>
      <meta charSet="utf8" />
      <link rel="stylesheet" href="http://localhost:1234/static/pdf.css" />
    </head>
    <body>
      {children}
      {renderPDFFooter()}
    </body>
  </html>
);

PDFLayout.propTypes = {
  children: PropTypes.node,
};

export default PDFLayout;
```

pdf rules 

```react
import { renderToStaticMarkup } from 'react-dom/server';
import pdf from 'html-pdf';

const componentToPDFBuffer = (component) => {
  return new Promise((resolve, reject) => {
    const html = renderToStaticMarkup(component);

    const options = {
      format: 'A4',
      orientation: 'portrait',
      border: '10mm',
      footer: {
        height: '10mm',
      },
      type: 'pdf',
      timeout: 30000,
    };

    const buffer = pdf.create(html, options).toBuffer((err, buffer) => {
      if (err) {
        return reject(err);
        }
    
        return resolve(buffer);
    });
  });
}

export default {
  componentToPDFBuffer
}
```

this can be /documents/preview.tsx in my case

```react
import React from 'react';

import Article from '../components/Article';
import PDFLayout from '../components/PDFLayout';
import pdfHelper from '../lib/pdfHelper';

class IndexPage extends React.Component {
  static async getInitialProps({ req, res, query }) {
    const exportPDF = query.exportPDF === 'true';
    const isServer = !!req;

    if (isServer && exportPDF) {
      const buffer = await pdfHelper.componentToPDFBuffer(
        <PDFLayout><Article/></PDFLayout>
      );

      // with this header, your browser will prompt you to download the file
      // without this header, your browse will open the pdf directly
      res.setHeader('Content-disposition', 'attachment; filename="article.pdf');
      
      // set content type
      res.setHeader('Content-Type', 'application/pdf');

      // output the pdf buffer. once res.end is triggered, it won't trigger the render method
      res.end(buffer);
    }

    return {};
  }

  render() {
    return (<Article/>)
  }
}

export default IndexPage;
```



### Property does not exist on type 'JSX IntrinsicElements

```react
import * as React from 'react';
import {
  Page,
  Document,
  View,
  Text,
  StyleSheet,
  Canvas,
  PDFViewer,
} from '@react-pdf/renderer';
import ReactPDF from '@react-pdf/renderer';

const styles = StyleSheet.create({
  page: { backgroundColor: 'tomato' },
  section: { textAlign: 'center', margin: 30 },
});

const doc = () => (
  <Document>
    <Page size="A4" style={styles.page}>
      <View style={[styles.section, { color: 'white' }]}>
        <Text>Section #1</Text>
      </View>
    </Page>
  </Document>
);

// ReactPDF.render(doc, `${__dirname}/example.pdf`);

export default function previewDoc() {
  return (
    <div>
      <PDFViewer>
        <doc />
      </PDFViewer>
    </div>
  );
}

```

上記の文でエラーが出た。

解決策は関数の先頭の文字を大文字にするだけ。

```react
import * as React from 'react';
import {
  Page,
  Document,
  View,
  Text,
  StyleSheet,
  Canvas,
  PDFViewer,
} from '@react-pdf/renderer';
import ReactPDF from '@react-pdf/renderer';

const styles = StyleSheet.create({
  page: { backgroundColor: 'tomato' },
  section: { textAlign: 'center', margin: 30 },
});

const Doc = () => (
  <Document>
    <Page size="A4" style={styles.page}>
      <View style={[styles.section, { color: 'white' }]}>
        <Text>Section #1</Text>
      </View>
    </Page>
  </Document>
);

// ReactPDF.render(doc, `${__dirname}/example.pdf`);

export default function previewDoc() {
  return (
    <div>
      <PDFViewer>
        <Doc />
      </PDFViewer>
    </div>
  );
}

```

## search

1. UI (material-ui)

   ```react
   const [searchWord, setSearchWord] = useState("");
   
   	   <Paper component="form" className={classes.root} onSubmit={handleSearch}>
                 <InputBase
                   className={classes.input}
                   placeholder="検索"
                   onChange={
                     e => setSearchWord(e.target.value)
                   }
                 />
                 <IconButton
                   type="submit"
                   className={classes.iconButton}
                 >
                   <SearchIcon />
                 </IconButton>
               </Paper>
   ```

2. redux(redux-toolkit)

```react
//searchDocuments
export const searchDocuments = (word: string): AppThunk => async(
  dispatch: AppDispatch
) => {
  try {
    const {data} = await API.get("/document").fetch()
    dispatch(setDocuments(data))
    let searchWord = word
    const searchItem = data.filter((item: { document_title: string }) => {
      console.log(item.document_title)
      return item.document_title.includes(searchWord)
    })
      console.log(searchItem)
    dispatch(setDocuments(searchItem))
  } catch (err) {
    console.log(err)
  }
}
```



### Material-ui

#### Select

```react
<FormControl className={classes.something}> {// setting for minWidth}
	<InputLabel>name</InputLabel> {// 選択フォームの上に出る文字}
    <Select
        value={}
        onChange={}
        >
        <MenuItem value={}>something</MenuItem>
        <MenuItem value={}>something</MenuItem>
        <MenuItem value={}>something</MenuItem>
    </Select>
</FormControl>
```

### TextField

#### 文字数に制限をかけたテキストフィールドの実装(Material-ui)

```react
                  <TextField
                    id="remarks"
                    label='備考'
                    multiline
                    rows={5} // 初期行数の指定
                    rowsMax={6} //こちらも上と挙動変わらず
                    className={classes.remarks}
                    value={example.remarks}
                    placeholder='テキストを入力'
                    onChange={e => setExample({ ...example, remarks: e.target.value})}
                  />
```

rowsで列数の指定をしてもその上限を超えた列の入力が可能。

最初の行数を指定したいだけなら有効。

文字数をしっかりと指定したい場合は以下のようにinputPropsでmaxLengthを指定してあげる

```react
                  <TextField
                    id="remarks"
                    label='備考'
                    multiline
                    rows={5}
                    inputProps={{maxLength: 10}} //１０文字までに指定している
                    className={classes.remarks}
                    value={example.remarks}
                    placeholder='テキストを入力'
                    variant='outlined'
                    onChange={e => setExample({ ...example, remarks: e.target.value})}
                  />
```





## 追加ボタンでテーブルを追加して複数の値をPOSTする

### 連想配列オブジェクトの特定の一つのStateの変更方法

今までの方法とは違う方法を見つけたのでメモ。

ちなみにReactで連想配列オブジェクトのStateを変更するのは難易度が高いので推奨されていない。

例えばこんな配列をinitial Stateでもっている

```react
  const [data, setData] = useState([
    {
      name: 'a',
      age: null,
      hobby: '',
      id: 0,
    },
    {
      name: 'b',
      age: 10,
      hobby: 'soccer',
      id: 1,
    },
    {
      name: 'c',
      age: 25,
      hobby: 'React'
      id: 2,
    },
  ]);
```



#### 今までの変え方

```react
export function example () {
    const handleChangeName = (k, v, id) => {
    let temp = [];
    temp = temp.concat(data);
    temp.forEach((a, i) => {
      if (a.id === id) {
        temp.splice(i, 1, { ...a, [k]: v });
      }
    });
    setData(temp);
  };
    
    return (
        ~~~
        {data.map(d => (
         <FormControl>
             <InputLabel>Name</InputLabel>
             <Select
                 value={d.name}
                 onChange={e => handleChangeName('name', e.target.value, d.id)}
                 >
                 ~~~~
             </Select>
         </FormControl>
         ))}
   	   ~~~
    )
}  
```

#### 新しい変え方

わざわざ関数を定義しないでこんな感じで。

```react
export function example () {
    ~~~
    return (
        ~~~
        {data.map(d => (
         <FormControl>
             <InputLabel>Name</InputLabel>
             <Select
                 value={d.name}
                 key={d.id}
                 onChange={e => setData(prev => {
                     return prev.map(i => {
                         if (i.id === d.id) {
                             return {
                                 ...i,
                                 name: e.target.value as string,
                             };
                         }
                     })
                 })}
                 >
                 ~~~~
             </Select>
         </FormControl>
         ))}
   	   ~~~
    )
}  
```



## 並べ替え

#### React

Reduxを使わない方法でもかんたんに実装することができたのでメモ。

```react
// ReduxからStateの状態を持ってくる
const products = useSelector(getListProduct, shallowEqual);

// idが新しい順 （初期のリストはこの順に設定） 
const sortProducts = products.sort(function(a, b) {
    if (a.id > b.id) return -1;
    if (a.id < b.id) return 1;
    return 0;
  });

const [items, setItems] = useState(sortProducts); 

//値段が高い順に並べ替えられる関数を定義
  const upProducts = () => {
    let newProducts = [...sortProducts];
    const upProduct = newProducts.sort(function(a, b) {
      if (a.unit_price > b.unit_price) return -1;
      if (a.unit_price < b.unit_price) return 1;
      return 0;
    });
    setItems(upProduct);
  };

//値段が安い順に並べ替えられる関数を定義
  const downProducts = () => {
    let newProducts = [...sortProducts];
    const downProduct = newProducts.sort(function(a, b) {
      if (a.unit_price > b.unit_price) return 1;
      if (a.unit_price < b.unit_price) return -1;
      return 0;
    });
    setItems(downProduct);
  };

// アイコンにonClickを入れる。
                  <ArrowDownwardIcon
                    onClick={downProducts}
                    fontSize="small"
                    color="action"
                    className={classes.iconSort}
                  />
                  <ArrowUpwardIcon
                    fontSize="small"
                    color="action"
                    className={classes.iconSort}
                    onClick={upProducts}
                  />
```



## AutoComplete

https://github.com/mbrn/material-table/issues/1155



## サイドバー（開閉可能）

```react
// AppSideBar component

import React, { useState, useEffect } from 'react';
import { useSelector } from 'react-redux';
import { RootState } from '@/app/rootReducer';
import { Divider, Drawer, IconButton, List } from '@material-ui/core';
import { useTheme } from '@material-ui/core/styles';
import {
  ChevronLeft,
  ChevronRight,
  Business,
  DeveloperBoard,
} from '@material-ui/icons';
import Inbox from '@material-ui/icons/Inbox';
import ExitToApp from '@material-ui/icons/ExitToApp';

import useStyles from './styles';
import { useLocation } from 'react-router-dom';
import { getLoginUserAndCompanySelector } from '@/selector/users';
import { UserTypeAdmin, UserTypeAgent } from '@/slicers/users';
import SideBarMenuItem from '@/components/organisms/SideBarMenuItem';
import { routeMaps } from '@/routes';
import { RouteProps } from '@/routes/RouteRecursive';
import { route } from '@/routes/url-generator';
import BackwardLogin from '@/components/organisms/BackwardLogin';

export type SideBarProps = { //type
  sideBarWidth: number;
  sideBarOpened: boolean;
  onSideBarClose: () => void;
};

export default function SideBar({
  sideBarWidth,
  sideBarOpened,
  onSideBarClose,
}: SideBarProps) {
  const classes = useStyles(sideBarWidth)();
  const theme = useTheme();
  const location = useLocation();
    
  return (
    <Drawer
      className={classes.drawer}
      variant="persistent"
      anchor="left"
      open={sideBarOpened}
      classes={{
        paper: classes.drawerPaper,
      }}
    >
      <div
        className={[
          classes.drawerHeader,
          isAbstractLogin ? classes.multi : '',
        ].join(' ')}
      >
        {isAbstractLogin && (
          <BackwardLogin>
            <div className={classes.logout}>
              <ExitToApp />
              <span>戻り</span>
            </div>
          </BackwardLogin>
        )}

        <IconButton onClick={onSideBarClose}>
          {theme.direction === 'ltr' ? <ChevronLeft /> : <ChevronRight />}
        </IconButton>
      </div>
      <Divider />

      <List>
          ~~~
    </Drawer>
  );
}


```

```react
//Parent component

import React, { useEffect } from "react";
import { useDispatch, useSelector, shallowEqual } from "react-redux";
import { RootState } from "@/app/rootReducer";
import clsx from "clsx";
import { CssBaseline, Box, Paper } from "@material-ui/core";
import AppHeader from "@/components/organisms/AppHeader";
import AppSidebar from "@/components/ecosystem/AppSideBar";
import useStyles from "./styles";
import UserIcomMenu from "@/components/ecosystem/UserIconMenu";
import FlashMessageSystem from "../FlashMessageSystem";
import ErrorMessage from "../ErrorMessage";
import BreadCrumbs from "../BreadcrumbsSystem";
import Common from "@/components/Common";
import Loading from "@/components/molecules/Loading";
import { toggleSideBar } from "@/slicers/sidebar";
import LoadingSystem from "../Loading";

export const sideBarWidth = 240;

export const AdminContainer: React.FC = ({ children }) => {
  const classes = useStyles();

  const sideBarOpened = useSelector(
    (state: RootState) => state.sidebarState.sideBarOpened
  );

  const handleDrawer = (open: boolean) => () => {
    dispatch(toggleSideBar(open));
  };

  return (
    <div className={classes.root}>
      <CssBaseline />
      <AppHeader
        sideBarWidth={sideBarWidth}
        sideBarOpened={sideBarOpened}
        onSidebarOpen={handleDrawer(true)}
      >
        <UserIcomMenu overrideIconNameClass={classes.userIconMenu} />
      </AppHeader>
      <AppSidebar
        sideBarWidth={sideBarWidth}
        onSideBarClose={handleDrawer(false)}
        sideBarOpened={sideBarOpened}
      />
      <main
        className={clsx(classes.content, {
          [classes.contentShift]: sideBarOpened
        })}
      >
        <div className={classes.drawerHeader} />
        <Box m={2}>
          <BreadCrumbs />
        </Box>
        <Paper elevation={3} className={classes.inner}>
          <LoadingSystem />
          <Common />
          <FlashMessageSystem />
          <ErrorMessage />
          {children}
        </Paper>
      </main>
    </div>
  );
};

export default AdminContainer;
```

#### Redux

```react
//slicers

import { createSlice, PayloadAction } from '@reduxjs/toolkit'

export type IconProps = React.FC<{ className: string }>

export type SidebarState = {  //type
  sideBarOpened: boolean
}

export const initialSidebarState: SidebarState = { //initial State
  sideBarOpened: true
}

const sidebarSlice = createSlice({ //action, reducers
  name: 'sidebar',
  initialState: initialSidebarState,
  reducers: {
    toggleSideBar(state, acttion: PayloadAction<boolean>) {
      state.sideBarOpened = acttion.payload
    }
  }
})

export const { toggleSideBar } = sidebarSlice.actions

export default sidebarSlice.reducer

//selector
import { combineReducers } from '@reduxjs/toolkit';

import userState from './slicers/user';
import loginState from './slicers/login';
import documentState from './slicers/document';
import productState from './slicers/product';
import postageState from './slicers/postage';
import companyLogoState from './slicers/companyLogo';
import sidebarState from './slicers/sideBar'

const rootState = {
  userState,
  loginState,
  documentState,
  productState,
  postageState,
  companyLogoState,
  sidebarState, -> add this state
};

const rootReducer = combineReducers(rootState);

export type RootState = ReturnType<typeof rootReducer>;
export type RawRootState = typeof rootState;
export default rootReducer;
```



## 画像のアップロード

react(ui)

```react
//company-logo/list.tsx

export default function CompanyLogoPage() {
  const classes = useStyles();

  return (
    <div>
      <CssBaseline />
      <main>
        <h2>会社ロゴ一覧</h2>
        <Typography paragraph>
          <SelectCompanyLogoTab />
          <div className={classes.btn}>
            <Link href="/company-logo/list">
              <CreateButton />
            </Link>
          </div>
          <CompanyLogoIndex />
        </Typography>
      </main>
    </div>
  );
}

//companylogo.tsx
  return (
    <div className={classes.root}>
      <Paper>
        <TableContainer className={classes.container}>
          <Table stickyHeader aria-label="sticky tabel">
            <TableHead>
              <TableRow>
                <TableCell>No.</TableCell>
                <TableCell>名前</TableCell>
                <TableCell>画像</TableCell>
                <TableCell>編集</TableCell>
                <TableCell>削除</TableCell>
              </TableRow>
            </TableHead>
            <TableBody>
              {companyLogos.map(companyLogo => (
                <TableRow key={companyLogo.id}>
                  <TableCell component="th" scope="row">
                    {companyLogo.id}
                  </TableCell>
                  <TableCell>{companyLogo.name}</TableCell>
                  <TableCell>
                    <img src="/questar.jpg" alt="company logo" />
                  </TableCell>
                  <TableCell>
                  <div className={classes.btn}>
                    <a
                      onClick={(
                        event: React.MouseEvent<HTMLAnchorElement, MouseEvent>
                      ): void => {
                      }}
                    >
                      <Button
                        startIcon={<EditIcon />}
                        color="primary"
                        className={classes.btn}
                      />
                    </a>
                  </div>
                  </TableCell>
                  <TableCell>
                  <a
                    onClick={(
                      event: React.MouseEvent<HTMLAnchorElement, MouseEvent>
                    ): void => {
                    }}
                  >
                    <Button
                      color="secondary"
                      className={classes.button}
                      startIcon={<DeleteIcon />}
                    />
                  </a>
                  </TableCell>
                </TableRow>
              ))}
            </TableBody>
          </Table>
        </TableContainer>
      </Paper>
    </div>
  );
}
```



## Date

compare date

https://www.webprofessional.jp/date-fns-javascript-date-library/



## Site speed improvement



### preknowledge

#### what's happenned before displaying page after launch browther

1. Http request
2. DNS



#### Http request

```
Response header

DNS protocol (look like machine language)

DNS over HTTPS (DoH) --> DNS si dangerous because it is not secret and hard to read, learn. DoH solved this issue. It be able to run querry as https.

Establish of connection.
```



#### display page by rendering engine

in case of google chrome, they have Blink.

```
DOM --> Document Object Model (which is element that display in developer tool.) In this stage, only first child and last child are made.

style --> analize css by rendering engine and then make Css Object Model Tree. 

Layout --> By rendering tree, decide each element should locate in window. (ex... contente edge, padding edge, border edge, margin edge.)  In this stage, child that in parent component layouted.

Paint --> the element that should display and that styles are calculated so adjust actual px on each element.

Compositor thread --> all rendering process in browther do in main thread. so if use js, the site must be heavy. --> another thread is available.
```



### Calculate site speed of React

#### React devtool disable

effective --> React devtool so it should be disabled. 

#### separate developer tool 

and to use the screen with full, the google dev tool sprate.

--> left icon of dock site ( which is right hand )

#### set PC as low 

set 3G enviornment in setting of CPU --> down grade...

and down level in network setting is also useful.

#### Run performance

just push circle button



```
Network --> Slow 3G
CPU --> 4x slowdown
```



#### read the result of performance

```
Yellow part --> run script (in summary, the time that spend are displayed)
Blue line --> the time the first dom complete ( occur event )
Red line --> the time occur fully reading the page ( occur event)
```



#### Move User timing to know action React

in case u have the source file, you can know where is problem

To see source code, you have to set webpack.config.js..

```
module.exports = {
	mode: 'development',
	devtool: 'source-map',
}
```



#### decreasing re-rendering 

parent component rendering --> all child component are re-rendering.

child component rendering --> just that child component is re-rendering.



#### Solution

to avoid that above, should disable shouldComponentUpdate and overide that setting as false (default is true.) 



--> useMemo is useful for react functional component.

--> allow function is also the cause of heavy because that output is new one. so if you use useMemo, it misunderstood as new state.



In case using nextjs, you can use reportWebVitals... reference nextjs measuring performance page.   



## Error

### Too many re-renders. React limits the number of renders to prevent an infinite loop.

久しぶりにReactでエラーが出たのでその忘備録

無限ループが起きているというエラー

原因はこの箇所

```react
  const handleName = (id: number, text: string | number): any => {
    const newProduct = purchasedProduct.map(p => (p.id === id ? Object.assign({}, p, { text }): p))
    return setPurchasedProduct(newProduct)
  }
  
                                    <Select
                                    value={p.name}
                                    key={p.id}
                                     onChange={handleName(p.id, p.name)}
                                        //このようにしてしまうとsetPurchasedProductがonChange時に呼ばれるのではなく、
                                        //render時に呼ばれてしまうのでrenderとSetの無限ループに。
                                     onChange={() => handleName(p.id, p.name)}
                                        //arrow functionを使えば解決
                                  >
                                    {products.map(product => (
                                      <MenuItem value={product.name}>
                                        {product.name}
                                      </MenuItem>
                                    ))}
                                  </Select>
```

https://www.it-swarm-ja.tech/ja/dom/reactjs：クリック時にコンポーネントを追加する方法は？/823632104/

## How to use useEffect function w async function

This is the wrong description 

```react
const MyFunctionnalComponent: React.FC = (props) => {
  useEffect(async () => {
   await loadContent();
  }, []);
  return <div></div>;
}
```

It should change like this below (the example of normal javascript function)

```react
const MyFunctionnalComponent: React.FC = props => {
  useEffect(() => {
    // Create an scoped async function in the hook
    async function anyNameFunction() {
      await loadContent();
    }
    // Execute the created function directly
    anyNameFunction();
  }, []);
return <div></div>;
};
```

In case you are familier w IIFE, the form must be like this

```react
const MyFunctionnalComponent: React.FC = props => {
  useEffect(() => {
    // Using an IIFE
    (async function anyNameFunction() {
      await loadContent();
    })();
  }, []);
  return <div></div>;
};
```

--- reference -> https://medium.com/javascript-in-plain-english/how-to-use-async-function-in-react-hook-useeffect-typescript-js-6204a788a435

--- more description about IIFE -> javascript, IIFE



# 入れ替え

React-smooth-dnd

https://github.com/kutlugsahin/react-smooth-dnd

https://laravelarticle.com/laravel-6-drag-and-drop-menu-sorting#:~:text=Laravel%206%20drag%20and%20drop%20menu%20sorting.%20In,anything%20user%20wants%20to%20sort%20their%20sorting%20order.