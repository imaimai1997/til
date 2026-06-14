# javascript

## 分割代入
### 基本
配列から値を取り出して、あるいはオブジェクトからプロパティを取り出して別個の変数に代入すること
```
const arr = [1, 2];
const [a, b, c] = arr;

console.log(a, b, c);
// 出力　1 2 undefined
```

```

const languages = {
  ja: '日本語',
  en: '英語'
};
const { ja, en } = languages;

console.log(ja, en);
// 出力　日本語 英語
```

### propsにおける分割代入
例えば```const props = { register, watch, employees };```のようなオブジェクトが渡されることを想定した場合、下記の3パターンでプロパティを取り出すことができる。

①分割代入を使わない基本
```
const ManagerInfoSection = (props) => (
  <p>{props.register}</p>
  <p>{props.watch}</p>
  <p>{props.employees}</p>
);
```
②コンポーネント内で分割代入
```
const ManagerInfoSection = (props) => (
const { register, watch, employees } = props;
  <p>{register}</p>
  <p>{watch}</p>
  <p>{employees}</p>
);
```
③引数で分割代入
```
const ManagerInfoSection = ({ register, watch, employees }) => (
  <p>{register}</p>
  <p>{watch}</p>
  <p>{employees}</p>
);
```
