# extends
- 可以用来继承一个class,interface,还可以用来判断有条件类型(很多时候在ts看到extends，并不是继承的意识)
- 示例：
```
T extends U ? X : Y;
```
- 上面的类型意思是，若 T 能够赋值给 U，那么类型是 X，否则为 Y
原理是令 T' 和 U' 分别为 T 和 U 的实例，并将所有类型参数替换为 any，如果 T' 能赋值给 U'，则将有条件的类型解析成 X，否则为Y。 上面的官方解释有点绕，下面举个栗子：
```
type Words = 'a'|'b'|"c";

type W<T> = T extends Words ? true : false;

type WA = W<'a'>; // -> true

type WD = W<'d'>; // -> false

```
- a 可以赋值给 Words 类型，所以 WA 为 true，而 d 不能赋值给 Words 类型，所以 WD 为 false。

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
