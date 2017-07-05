# genegene

## Q1

```java
@AllArgsConstructor
@NoArgsConstructor
class Int {
  private int x;

  public void print() {
    System.out.println(x);
  }
}
```

このようなクラス `Int` があるとき、
`List<Int>` を受け取って、リストの各要素に対して `Int#print` を呼び出す関数
`printA` を作ってください。
こんなコードが通ればOK

```java
List<Int> intList = new ArrayList<>();
printA(intList);
```

## Q2

クラス `Int` に加えてクラス `Str` を作り、`print` メソッドを interface に切り出すことにしました。

```java
interface Printable<T> {
    void print();
}

@AllArgsConstructor
@NoArgsConstructor
class Int implements Printable {
    private int x;

    @Override
    public void print() {
        System.out.println(x);
    }
}

@AllArgsConstructor
@NoArgsConstructor
class Str implements Printable {
    private String x;

    @Override
    public void print() {
        System.out.println(x);
    }
}
```

`List<Int>` か `List<Str>` を受け取って、リストの各要素に対して `Printable#print` を呼び出す関数
`printB` を作ってください。
こんなコードが通ればOK

```java
List<Int> intList = new ArrayList<>();
List<Str> strList = new ArrayList<>();
printB(intList);
printB(strList);
```

## Q3

2倍可能であることを表す `HasTwice` インターフェイスを作り、`Int` と `Str` が実装しました。

```java
interface HasTwice<T> {
    T twice();
}

interface Printable<T> {
    void print();
}

@AllArgsConstructor
@NoArgsConstructor
class Int implements HasTwice<Int>, Printable {
    private int x;

    @Override
    public Int twice() {
        return new Int(x * 2);
    }

    @Override
    public void print() {
        System.out.println(x);
    }
}

@AllArgsConstructor
@NoArgsConstructor
class Str implements HasTwice<Str>, Printable {
    private String x;

    @Override
    public Str twice() {
        return new Str(x + x);
    }

    @Override
    public void print() {
        System.out.println(x);
    }
}
```

`List<Int>` か `List<Str>` を受け取って、リストの各要素に対して `HasTwice#twice` を呼び出し
た結果を `List<Int>` か `List<Str>` で返す関数 `twiceB` を作ってください。
こんなコードが通ればOK

```java
List<Int> intList = Arrays.asList(new Int(2), new Int(3), new Int(4));
List<Str> strList = Arrays.asList(new Str("abc"), new Str("00"));
List<Int> intList2 = twiceB(intList); // [Int(4), Int(6), Int(8)] を返す
List<Str> strList2 = twiceB(strList); // [Str("abcabc"), Str("0000")] を返す
```

## Q4

Q3 と同じクラスが定義されてる状態で、
`List<Int>` か `List<Str>` を受け取って、リストの各要素に対して `HasTwice#twice` を呼び出し
つつ `Printable#print` も呼びだして2倍した結果を表示して、
結果を `List<Int>` か `List<Str>` で返す関数 `twiceAndPrint` を作ってください。
こんなコードが通ればOK

```java
List<Int> intList = Arrays.asList(new Int(2), new Int(3), new Int(4));
List<Str> strList = Arrays.asList(new Str("abc"), new Str("00"));
List<Int> intList2 = twiceAndPrint(intList); // 4, 6, 8 を表示し、[Int(4), Int(6), Int(8)] を返す
List<Str> strList2 = twiceAndPrint(strList); // "abcabc", "0000" を表示し、[Str("abcabc"), Str("0000")] を返す
```

`?` とかが出てこないのでおまけ問題追加

## Q5

twiceAndPrint の twice を任意の関数で置き換えられるようにしたいです。
Q3 と同じクラスが定義されてる状態で、
任意の `List` と、そのリスト要素に適用可能な関数 `function` を受け取って、
リストの各要素に対して `function.apply` を呼び出しつつ
 Printable#print も呼びだして表示して、
結果を `List<型>` で返す関数 applyAndPrint を作ってください。
こんなコードが通ればOK

```java
List<Int> intList = Arrays.asList(new Int(1), new Int(2), new Int(3));
Function<HasTwice<?>, Str> g = t -> new Str(t.twice().toString());
List<Str> strList = applyAndPrint(intList, g);
```




