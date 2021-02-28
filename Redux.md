## Copy(外部キー)



外部キーのデータを持ったデータを外部キーのデータを保持したままコピー。

#### Redux側

```typescript
// initialState
export const documentInitialState: DocumentState = {
  indexes: {},
};

// reducer, action, actionCreator, initialStateを定義
const documentSlice = createSlice({ 
  name: 'documentState',
  initialState: documentInitialState,
  reducers: {
    setDocuments: (
      state: DocumentState,
      { payload }: PayloadAction<Document[]>
    ) => {
      state.indexes = {};
      payload.forEach(item => {
        state.indexes[item.id] = item;
      });
    },
  },
});

//copy documents
export const copyDocuments = ( // Reactから値を受け取る
  pid: number,
  business_partner_company_name: string,
  document_title: string,
  document_type_id: number,
  honorific_title: string,
  logo_img_path: string,
  payment_terms: string | null,
  quotation_expiration_date: string,
  tax: string,
  term_and_conditions: string | null,
  usage_period: string | null,
  usage_period_start: Date | null,
  usage_period_end: Date | null,
  user_id: number,
  remarks: string,
  customer_part_id: number,
  see_part_id: number,
  sell_part_id: number,
  products: PostProduct, //productsとpostageが外部キーをして保持しているデータ
  postages: PostPostage
): AppThunk => async (dispatch: AppDispatch) => { //非同期
  try {
    let { data } = await API.get('/document').fetch(); //バックエンドからデータを取得
    dispatch(setDocuments(data)); //データをdispatch
    let editId = pid;
    const editItem = data.filter((edit: { id: number }) => {
      return editId === edit.id;
    });
    dispatch(setDocuments(editItem)); //その中から値として受け取ったIdと同じIdのみに絞り込み

    const doc_info = { //そのデータをオブジェクトに
      sell_part_id,
      see_part_id,
      customer_part_id,
      document_type_id,
      business_partner_company_name,
      honorific_title,
      user_id,
      document_title,
      payment_terms,
      usage_period,
      usage_period_start,
      usage_period_end,
      logo_img_path,
      quotation_expiration_date,
      tax,
      term_and_conditions,
    };

    const product_item = products;
    const postage_item = postages;

    const res = await API.post('/document') //Post APIをたたく
      .setBody({ doc_info, remarks, product_item, postage_item }) //独自で定義したsetBodyでデータをセット
      .fetch();
    dispatch(setDocuments(res.data)); //dispatch
  } catch (err) {
    console.log(err);
  }
};

// idでデータに紐付いている外部キーデータを取得
export const setPurchasedPostage = (pid: number): AppThunk => async (
  dispatch: AppDispatch
) => {
  try {
    const { data } = await axios.get(
      'http://yourapi/api/purchasedpostage/' + `${pid}`
    );
    console.log('postage', data);
    dispatch(setDocumentPostage(data));
  } catch (err) {
    console.log(err);
  }
}

export const setPurchasedProduct = (pid: number): AppThunk => async (
  dispatch: AppDispatch
) => {
  try {
    const { data } = await axios.get(
      'http://yourapi/api/purchasedproduct/' + `${pid}`
    );
    console.log('product', data);
    dispatch(setDocumentProduct(data));
  } catch (err) {
    console.log(err);
  }
};
```

#### React

```react
      
//使うものを色々定義
  const dispatch = useDispatch();
  const documents = useSelector(getListDocument, shallowEqual);
  const router = useRouter();
  const [refresh, setRefresh] = useState(0);
  const products = useSelector(getPurchasedProduct, shallowEqual);
  const postages = useSelector(getPurchasedPostage, shallowEqual);
  const tax = '0.1';

  useEffect(() => {
    dispatch(getDocuments());
  }, []);

//ページをリロード
  useEffect(() => {
    const reload = async () => {
      await dispatch(getDocuments());
      setRefresh(0);
    };
    reload();
  }, [refresh]);

~~~~
	<TableCell>
                  <a
                    onClick={(
                      event: React.MouseEvent<HTMLAnchorElement, MouseEvent>
                    ): void => {
		      //Reduxで定義したものを使用して外部キーデータを取得
                      dispatch(setPurchasedPostage(document.id)); 
                      dispatch(setPurchasedProduct(document.id));
                       //ReactからReduxに値を送信。この場合はボタンを押したらその要素のデータを渡している
                      dispatch(
                        copyDocuments(
                          document.id,
                          document.business_partner_company_name,
                          document.document_title,
                          document.document_type_id,
                          document.honorific_title,
                          document.logo_img_path,
                          document.payment_terms,
                          document.quotation_expiration_date,
                          tax,
                          document.term_and_conditions,
                          document.usage_period,
                          document.usage_period_start,
                          document.usage_period_end,
                          document.user_id,
                          document.remarks,
                          document.customer_part_id,
                          document.see_part_id,
                          document.sell_part_id,
                          products,
                          postages
                        )
                      );
                      setRefresh(1);
                    }}
                  >
                    <Button color="primary" startIcon={<FileCopyIcon />} />
                  </a>
                </TableCell>
~~~
```

### Search（複数）

一つの値で複数のカラムにヒットするように編集した。

以前は一つの検索フォームに一つの検索結果で実装していた。

実装はかんたんで、検索の結果をカツで設定するだけ。



#### Redux

```typescript
// search Document
export const searchDocuments = (word: string): AppThunk => async (
  dispatch: AppDispatch
) => {
  try {
    const {data} = await API.get('/document').fetch()
    const searchItem = data.filter((item: { document_title: string , id: number, business_partner_company_name: string | number }) => {
      let itemId = String(item.id);
      let itemPartner = String(item.business_partner_company_name)
      return ((item.document_title.includes(word) ||
        itemId.includes(word) ||
        itemPartner.includes(word)
      ))
    });
    console.log(searchItem);
    dispatch(setDocuments(searchItem));
  } catch (err) {
    console.log(err);
  }
};
```

#### React

```react
                <Paper
                  component="form"
                  className={classes.root}
                  onSubmit={handleSearch}
                >
                  <InputBase
                    className={classes.input}
                    placeholder="見積もりを検索する"
                    onChange={e => setSearchWord(e.target.value)}
                  />
                  <IconButton type="submit" className={classes.iconButton}>
                    <SearchIcon />
                  </IconButton>
                </Paper>
```

