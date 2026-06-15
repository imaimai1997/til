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

## useState-コンポーネントの状態管理
- 状態とは「時間とともに変わる値」のこと
- ```const [値, 値を変える関数] = useState(初期値); ```

## useEffect-副作用
- Reactコンポーネントの本来の仕事は「画面を描画すること」であり、それ以外の処理を副作用と呼ぶ
- 副作用の例
  - データをAPIから取得する
  - 別の値が変わった時に、連動して別の値も変える
  - タイマーをセットする

基本の形
```
useEffect(() => {
  // 副作用の処理
}, [依存する値]);
```
- useEffectを使用せず、関数の中で直接書いた場合は、無限レンダリングが起きる。コンポーネントの関数は描画のたびに毎回実行されるため、コンポーネントで```setValue```を呼ぶと再描画が起き、また```setValue```が呼ばれて無限ループになる

## カスタムフック-ロジックの分離
カスタムフックとは
- 複数の```useState```や```useEffect```をまとめて、一つの関数にしたもの
- index.tsxは見た目だけ、カスタムフックはロジックだけ（状態・API通信）。という形で責務を分ける
- 名前を必ずuseから始める


