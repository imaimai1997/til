# React

## コンポーネント
- reactでは画面を部品（コンポーネント）に分けて作成する
- コンポーネントはJSX記法で作成し、名前は大文字から始める
- UIコンポーネントはレイアウト責務に徹するため、状態はもたせない
```
const NotesSection = ({ register }: Props) => (
  <Box title="備考欄" icon={...}>
    <textarea {...register("notes")} />
  </Box>
);
```

## props
- コンポーネントは引数（props）を受け取ることができる
- 親コンポーネントで渡した引数を子コンポーネントで表示する。（子コンポーネントがUIコンポーネントで、親コンポーネントはページコンポーネント）
```
// 受け取る側（子コンポーネント）
const ActionBar = (props: Props) => (
  <div>
    {props.mode === "create" && <Button>追加</Button>}
    {props.mode === "edit" && <Button onClick={props.onDelete}>削除</Button>}
  </div>
);

// 渡す側（親コンポーネント）
<ActionBar mode="edit" onDelete={handleDeleteCar} onUpdate={handleUpdateCar} />
```
- 分割代入で書くのが一般的。分割方法についてはこちらを参照（[propsにおける分割代入](javascript.md#propsにおける分割代入)）
- 親から子にデータを渡すルールであり、子から親にデータを送ることは直接できない。子から親に何か伝えたい場合は。親が関数をpropsで渡して、子がその関数を呼ぶ
```
// 親
const Parent = () => {
  const handleDelete = () => { /* 削除処理 */ };
  return <ActionBar onDelete={handleDelete} />;
  //                 ↑ 関数を渡す
};

// 子
const ActionBar = ({ onDelete }) => (
  <button onClick={onDelete}>削除</button>
  //               ↑ 呼び出す（実行するのは親の関数）
);
```

