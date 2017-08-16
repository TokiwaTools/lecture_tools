## 目次

1. [リーダブルコーザ概要](#/3)
2. [初級編: 掃除](#/8)
3. 中級編: 整頓
4. 上級編: 富豪

---

## [リーダブルコーザ概要](https://atnd.org/events/89946)

### 目標
**他人が読みやすい、いじりやすい｢リーダブルコード｣を書く**

---

### いいプログラムを目指す上で

- 可読性 (読みやすい)
    - スペース、タブ、空行による見やすさ
    - 単純な構造やコメントによる理解のしやすさ
- 拡張性 (いじりやすい)
    - 変数、メソッド、クラスなど構造による拡張性、柔軟性

|||

#### 可読性と拡張性はトレードオフ

- どちらも高いは幻想
- 実は拡張性の方が難しい

---

### リーダブルコードを書けると…

- グループワークなどで他人が自分のコードを解読しやすくなる
- 後に自分のコードを見返した時に理解が早い
- 機能追加やデバッグが容易になる

---

### 講座の進め方

- 言語: Processing
- 1回2時間、3回に分けて実施

|||

- [**初級編**](#/8): 掃除
    - ある人が書いた｢ババ抜き｣のコードを綺麗にする
    - 可読性重視のコードを目指す
    - 全学年向け
- **中級編**: 整頓
    - クラスを取り入れて｢ババ抜き｣の可読性と拡張性をより高める
    - よりオブジェクト指向寄り
    - 2年生以上向け
- **上級編**: 富豪
    - ｢ババ抜き｣のコードを再利用して｢大富豪｣を作る
    - 各自リーダブルにコードを書いてもらい講師が評価する
    - 2年生以上向け

---

### 諸注意

- 読みやすさは人それぞれ
    - 正解はない
- この講座は私の習慣と主観に基づいています

---

# 初級編
### Unreadableババ抜きを掃除する

---

## 目次

<font size="5.0em">
<ol>
    <li><a href="#/10">Unreadableババ抜きを見る</a></li>
    <li><a href="#/11">BADCODEの定義</a></li>
    <li><a href="#/12">可読性を高める</a></li>
    <ol>
        <li><a href="#/13">表面上の改善</a></li>
        <li><a href="#/14">ifの並び順</a></li>
        <li><a href="#/15">ファイルによる分割</a></li>
        <li><a href="#/16">変数で分割する</a></li>
        <li><a href="#/17">名前で説明する</a></li>
        <li><a href="#/18">コメントで説明する</a></li>
        <li><a href="#/19">break, continue, returnで早く返す</a></li>
        <li><a href="#/20">無駄を削除する</a></li>
        <li><a href="#/21">変数のスコープを縮める</a></li>
        <li><a href="#/22">メソッドによる分割</a></li>
        <li><a href="#/23">TIPS</a></li>
    </ol>
    <li><a href="#/27">掃除を始める</a></li>
</ol>
</font>

---

## Unreadableババ抜きを見る

[Download](contents/beginner/Unreadable_Babanuki.zip)

---

## BADCODEの定義
- 詰まったコード (空白のないコード)
- 一行が長い、{}内が長い
- 解読できない
- コメントが少なすぎる/多すぎる
- 文字がインデントで右側に寄りすぎている
- グローバル変数が多すぎる
- 3次以上の配列を使っている

Note:
グローバル変数とローカル変数の説明

---

## 可読性を高める

---

### 表面上の改善 (★☆☆)

#### スペースを挿入する箇所
- 算術演算子以外の演算子の前後 (`=`, `>`, `==`, `!=` ...)
- `,`の後
- (ここからは好み)
- [], <>の後
- if, for, whileの後
- 算術演算子の前後
- {}の前後
- ( hoge.fuga() ) (カッコが被るとき)

|||

~~~processing
/*---BEFORE---*/
int[]array=[1,2,3,4];
int maxNum=array[0];
for(int i=0;i<array.length;i++){
    if(maxNum<array[i]){
        maxNum=array[i];
    }
}

/*---AFTER---*/
int[] array = [1, 2, 3, 4];
int maxNum = array[0];
for (int i = 0; i < array.length; i++) {
    if (maxNum < array[i]) {
        maxNum = array[i];
    }
}
~~~

|||

#### 空行
- メソッドの前後
- 区切りをつけたいとき

#### インデント下げ
- `{` の次の行

---

### ifの並び順 (★☆☆)
- 定数を右側に

~~~processing
/*---BEFORE---*/
if (max > 10) ...

/*---AFTER---*/
if (posX > maxX) ...
~~~

---

### ファイルによる分割 (★☆☆)
- 役割ごとに分ける
- `setup()` と `draw()` は `main.pde`、`key`, `mouse`関係は `input.pde` など
- 本来は全てクラス化させることが望ましい

---

### 変数で分割する (★☆☆)
- 変数は式を分割する
- 変数は行為を説明する道具

|||

~~~processing
/*---BEFORE---*/
if ( squares.get( squares.size()-1 ).getValue() == 0 ) ...

/*---AFTER---*/
Square lastSquare = squares.get( squares.size()-1 );
if (lastSquare.getValue() == 0) ...
~~~

~~~processing
/*---BEFORE---*/
if (leftPosition < mouseX && rightPosition >= mouseX) ...

/*---AFTER---*/
boolean inRange = leftPosition < mouseX && rightPosition >= mouseX;
if (inRange) ...
~~~

---

### 名前で説明する (★★★)
- 名前付けはプログラミングで一番悩む作業
- 名前に使う単語の語彙は経験による部分が大きい
- ただ慣習や伝わるコツがある
- 参考
    - [プログラミングでよく使う英単語のまとめ](http://qiita.com/Ted-HM/items/7dde25dcffae4cdc7923)
    - [うまくメソッド名を付けるための参考情報](http://qiita.com/KeithYokoma/items/2193cf79ba76563e3db6)

|||

#### 名前付けの慣習
- キャメルケース
    - `drawImage`
    - 単語の先頭を大文字から始める (最初は小文字)
- スネークケース
    - `draw_image`
    - 単語の間に `_` を使う
- 好みでどちらかに従う
- クラスは先頭は大文字から、変数やメソッドは小文字から
- 定数は全て大文字、必ずスネークケース

|||

#### コツ
- 分かりづらい省略をしない
    - `string` -> `str`, `number` -> `num` ぐらいは分かるが
    - `score` -> `sc`, `background` -> `bg` はやめよう
- グローバル変数は長く、ローカル変数は短く
    - ローカルとグローバル変数で重複するのを防ぐ
- 一文字の変数は使わない (for, whileの`i`, `j`などを除く)
- 名前に形容詞をつける
    - `x`, `y`, `size`, `number` だけでは分からない
- 意味を成さない単語を使わない
    - `flag`, `switch`, `temp`, `aaa`など

    ~~~processing
    /*---BEFORE---*/
    boolean drawingFlag = false;    //boolean型ならflagなのは自明

    /*---AFTER---*/
    boolean drawing = false;
    ~~~

Note:
tempは形容詞がついたらあり 他は意味なし

|||

- (ローマ字を使わない)
    - ローマ字否定派と容認派がいる
    - ほとんどの言語は英語でできているので、個人的には否定派

---

### コメントで説明する (★★☆)
- コメントはコードの補助的に説明する方法
- コメントは多すぎても少なすぎてもいけない
    - コメントしなくても分かるようなことは書かない
- 用途
    - メソッド、メソッドの引数、クラスの説明
    - 分かりづらい複雑な処理の説明
    - 既定値の説明

    ~~~processing
    int MAX_LENGTH = 2;  //なんで2なのか書く
    ~~~

    - 欠陥の説明 (～～のときバグが発生する)

---

### break, continue, returnで早く返す (★★☆)
- for, while文を途中で抜けるのが`break`、スキップして次のループに行くのが`continue`
- メソッド内で複数の`return`を使う

|||

~~~processing
/*---BEFORE---*/
for (int i = 0; i < chains.size(); i++) {
    int chain = chains.get(i);
    if (chain == null) {
        //例外処理
        emptyCounter++;
    } else {
        //通常処理
        ...
    }
}

/*---AFTER---*/
for (int i = 0; i < chains.size(); i++) {
    int chain = chains.get(i);
    if (chain == null) {    //例外なら早く次にスキップさせる
        emptyCounter++;
        continue;
    }

    ...     //通常処理のネストが下がる
}
~~~

|||

~~~processing
/*---BEFORE---*/
int compare(int n, int m) {
    int r = -1;
    if(n >= m)
        r = 0;
    if(n > m)
        r = 1;
    return r;
}

/*---AFTER---*/
int compare(int n, int m) {
    if (n > m) return 1;
    if (n < m) return -1;
    return 0;   //(n == m)のとき
}
~~~

---

### 無駄を削除する (★★★)
- コメントアウトしたコードを削除する
- 無駄な処理を削除する

---

### 変数のスコープを縮める (★★★)
- 変数のスコープ: その変数が使える範囲

~~~processing
int total = 0;  //totalのスコープ開始
...
for (int i = 0; i <= 10; i++) {
    int squaredNum = i*i;   //squaredNumのスコープ開始
    total += squaredNum;    //squaredNumのスコープ終了
}
...
println(total); //totalのスコープ終了
~~~

|||

- グローバル変数だらけの例

![](../images/too_many_global_variable.png)

|||

- スコープを縮める例

~~~processing
/*---BEFORE---*/
int maxNum = points[0][0];
...
for (int j = 0; j < points.length; j++) {
    for (int i = 0; i < points[0].length; i++) {
        int point = points[j][i];
        if (point > maxNum) {
            maxNum = point;
        }
    }
    
    if (maxNum > 10) {
        ...
    }
}
//ここでもmaxNumは使える

/*---AFTER---*/
...
for (int j = 0; j < points.length; j++) {
    int maxNum = points[0][0];

    for (int i = 0; i < points[0].length; i++) {
        int point = points[j][i];
        if (point > maxNum) {
            maxNum = point;
        }
    }

    if (maxNum > 10) {
        ...
    }
}
//ここではmaxNumは使えない
~~~

|||

- 変数のスコープを縮めると
    - 変数の宣言と使用が近くなるので分かりやすい
    - 変数を間違って書き換えにくくなる
- グローバル変数は全てメインファイルの先頭に
    - メソッドとメソッドの間はNG 

Note:
公園のフリーマーケットとスーパーマーケットの違い  
どちらも"変数"を売ってるとする どちらが安全か

---

### メソッドによる分割 (★★☆)
- メソッドはコードを分割する箱
    - 結果的にネストが浅くなる
- メソッド化する = その処理を名前で説明する

|||

~~~processing
/*---BEFORE---*/
void draw() {
    background(255);
    ...
    stroke(0);
    for (int i = 1; i < 8; i++){
        line(i*100, 0, i*100, height);
        line(0, i*100, width, i*100);
    }
    ...
}

/*---AFTER---*/
void draw() {
    background(255);
    ...
    drawLines();
    ...
}

//メソッド化と同時に処理の説明をする
void drawLines() {
    stroke(0);
    for (int i = 1; i < 8; i++){
        line(i*100, 0, i*100, height);
        line(0, i*100, width, i*100);
    }
}
~~~

|||

- メソッド化が必要なとき
    - `{}`の中が50行を超える
    - ネストが4[マトリョーシカ](https://ja.wikipedia.org/wiki/マトリョーシカ人形)以上になる
    - 似たような処理がある
- メソッドを使うべきありがちな状況
    - `setup()`, `draw()`, `keyPressed()` 内が長すぎる
    - 読者への怒濤のforIf攻撃
    - ifの条件が長い

Note:
ifの中にifがあるみたいな入れ子構造が4つ以上になる

|||

#### forIf攻撃

![forIf攻撃](../images/for_if_attack.png)

|||

#### メソッドの基本

1. 何かを与えたら何かを返してくる
    - インプット: 引数
    - アウトプット: 返り値
    - 返り値なし(void)、引数なしの時はグローバル変数を処理している可能性が高い
        - ローカル変数やクラスで変数のスコープを縮める
1. 1メソッド1処理
    - 複数のことをやらない

参考: [ネストの深さは闇の深さ](http://qiita.com/Mic-U/items/1ec901864d4ab11c8d6f)

---

### TIPS

---

### ifからswitchに変える
- 同じ変数の条件分岐をする場合、switch文を使うと分かりやすくなる

~~~processing
/*---BEFORE---*/
void keyPressed() {
    if (key == 'a') {
        //処理A
    } else if (key == 'b') {
        //処理B
    } else {
        //処理C
    }
}

/*---AFTER---*/
void keyPressed() {
    switch(key) {
        case 'a':
            //処理A
            break;
        case 'b':
            //処理B
            break;
        default:
            //処理C
    }
}
~~~

|||

#### switchの注意

- ifと違い、`==`(等価)しか判定できない
- `null`は条件に指定できない
- `break`をしないと次の`case`に行ってしまう
    - `break`しない記述は分かりづらいためやめよう

---

### {}の省略 (場合による)
- {}内が一行の場合、{}を省略できる
- 好みの部分が大きい

~~~processing
/*---BEFORE---*/
for (int i = 0; i < array.length; i++) {
    if (array[i] == 0) {
        continue;
    }

    ...
}

/*---AFTER---*/
for (int i = 0; i < array.length; i++) {
    if (array[i] == 0) continue;

    ...
}
~~~

|||

#### 注意

- elseを使っているときはやめよう

~~~processing
//BADCODE
for (int i = 0; i < array.length; i++) {
    if (array[i] == 0) println("zero");
    else if (array[i] > 0) println("plus");
    else println("minus");
}
~~~

---

### final
- 変数にfinalをつけると変更不可、つまり定数になる
- より安全に変数を扱うことができる

    ~~~processing
    final String IP_ADDRESS = "localhost";
    IP_ADDRESS = "192.168.0.1";     //エラー
    ~~~

- オブジェクトの中身は書き換えられてしまう

    ~~~processing
    final String[] ADDRESSES = {
        "192.168.0.1", "192.168.0.5"
    };
    ADDRESSES[0] = "localhost";     //エラーなし
    ~~~

- 定数の配列は列挙型によって実装できる (上級編で扱う)

---

## 掃除を始める

---

