
# keyof
- keyof 操作符接受对象类型，并生成其键的字符串或数值文字联合。
- keyof 可以用来取得一个对象接口的所有 key 值
- 示例：
```
interface IDog {
    name: string;
    age: number;
    sex?: string;
}

type K1 = keyof Person; // "name" | "age" | "sex"
type K2 = keyof Person[];  // "length" | "push" | "pop"  ...
type K3 = keyof { [x: string]: Person };  // string | number

```

# typeof
- 在 JS 中 typeof 可以判断数据类型，在 TS 中，它还有一个作用，就是获取一个变量的声明类型，如果不存在，则获取该类型的推论类型。
- 示例：
```
interface IDog {
  name: string;
  age: number;
  sex?: string;
}

const jack: IDog = { name: 'jack', age: 100 };
type Jack = typeof jack; // -> IDog

function foo(x: number): Array<number> {
  return [x];
}

type F = typeof foo; // -> (x: number) => number[]
-Jack 这个类型别名实际上就是 jack 的类型 Person，而 F 的类型就是 TS 自己推导出来的 foo 的类型 (x: number) => number[]。

```
