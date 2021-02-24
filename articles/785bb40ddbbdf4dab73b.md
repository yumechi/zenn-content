---
title: "Scalaで競技プログラミングの入出力メモ"
emoji: "🎃"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["scala", "競技プログラミング"]
published: false
---

最近、息抜きがてら Scala を書いてみようということで書いているのですが、さらに息抜きで競技プログラミングをたしなみながらコードを書いています。

Scala の標準入出力は [scalaで競技プログラミングを入門する方法　～標準入力～ - Qiita](https://qiita.com/soshi_harami/items/3f1eaf7d4a84d30fac30) などがありますが、自分なりの整理としてまとめてみます。

## 基本的に

Java の Scanner を使って書くのが楽なので、そうしています。

```scala
import java.util.Scanner

object Main extends App {
  val sc = new Scanner(System.in)

  // 今回はここ以降の部分を埋める
}
```

問題については [yukicoder](https://yukicoder.me/) を参照しています。

Scala のバージョンは 2.13 系を使っています（パッチバージョンは忘れました）。

## 1つの数値の入力

いわゆる N が 1 つだけ与えられるケースです。

```scala
val n = sc.nextInt
```

例えばこの問題。

https://yukicoder.me/problems/no/1003


## 2つの数字の入力

N, K が 1 列で与えられるケースです。別々の変数でとりたい場合は下記です。

```scala
val n = sc.nextInt
val k = sc.nextInt
```

配列でとりたい場合は下記です。

```scala
val an = Array.fill(2)(sc.nextInt)
```

例えばこの問題（この問題に関しては double でとった方が楽なので、 `sc.nextDouble` でとりましたが）。

https://yukicoder.me/problems/no/1033

## 1次元配列の入力

```
n
a1 a2 ... an
```

のように最初に要素数が与えられ、配列を取るようなケースです。

```scala
val n = sc.nextInt
val an = Array.fill(n)(sc.nextInt)
```

例えばこの問題（この問題に関しては double でとった方が楽なので、 `sc.nextDouble` でとりましたが（またかい））。

https://yukicoder.me/problems/no/1131

## 2次元配列の入力

```
H W
a11 a12 ... a1w
a21 a22 ... a2w
 :   :   :   : 
ah1 ah2 ... ahw
```

のような、h, w で渡されるケースです。このケースですが、 `Array.fill` をうまく使うことで実現できます（これは[ある人](https://twitter.com/pxfnc)に教えてもらいました）。

```scala
val h = sc.nextInt
val w = sc.nextInt
val al = Array.fill(h, w)(sc.nextInt)
```

Scala のドキュメントで確認できますが、5 次元配列までは fill を活用して作れるようです（5 次元配列なんて使う日が来るんだろうか）

`https://www.scala-lang.org/api/current/scala/Array$.html#fill[T](n1:Int,n2:Int)(elem:=%3ET)(implicitevidence$13:scala.reflect.ClassTag[T]):Array[Array[T]]`

例えばこの問題

https://yukicoder.me/problems/no/1130

## 入力値の処理

```scala
// 文字列
val s = sc.next

// double 型
val d = sc.nextDouble

// 大きい数字は long でとる
val l = sc.hasNextLong

// あとで計算結果が大きく場合は BigInt とかに変換して使ってます
val an = Array.fill(n)(BigInt(sc.nextInt))
```

あとはノリ

## まとめ

配列周りの入力も最初なかなか難しかったのですが、出力側も `an(0)` などとする必要があり、なかなか慣れませんでした。

とはいえ競技プログラミングを通して配列周りの操作にはかなり慣れたので、息抜きがてら書くにはちょうど良かったです。

コンテストに出なくてもこういう脳トレみたいな感じで気軽にコード書くのは良いですね。
