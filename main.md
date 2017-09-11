## 目次

1. [リーダブルコーザ概要](#/2)
2. [初級編: 掃除](#/7)
3. [中級編: 整頓](#/31)
4. 上級編: 富豪
5. [参考文献]()

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

<font size="4.0em">
<ol>
    <li><a href="#/9">Unreadableババ抜きを見る</a></li>
    <li><a href="#/10">BADCODEの定義</a></li>
    <li><a href="#/11">可読性を高める</a></li>
    <ol>
        <li><a href="#/12">表面上の改善</a></li>
        <li><a href="#/13">ifの並び順</a></li>
        <li><a href="#/14">ファイルによる分割</a></li>
        <li><a href="#/15">変数で分割する</a></li>
        <li><a href="#/16">名前で説明する</a></li>
        <li><a href="#/17">コメントで説明する</a></li>
        <li><a href="#/18">break, continue, returnで早く返す</a></li>
        <li><a href="#/19">無駄を削除する</a></li>
        <li><a href="#/20">変数のスコープを縮める</a></li>
        <li><a href="#/21">メソッドによる分割</a></li>
        <li><a href="#/22">TIPS</a></li>
    </ol>
    <li><a href="#/26">掃除を始める</a></li>
    <ol>
        <li><a href="#/27">掃除の前に…</a></li>
        <li><a href="#/28">掃除の流れ</a></li>
        <li><a href="#/29">課題</a></li>
        <li><a href="#/30">プログラム解説</a></li>
    </ol>
</ol>
</font>

---

## Unreadableババ抜きを見る

[Download](./contents/beginner/Unreadable_Babanuki.zip)

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
if (max > 10) ...

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

- 単語を統一する
    - select, choose など意味の似た単語は統一する
- 番号 = number, 数 = count と使い分ける (本来どちらもnumber)
- あえて冗長に名前付けする
    - hand = 手札だがhandCardとしてカードであることを示唆する
- 単語の重複を避ける
    - drawを｢描く｣意味と｢引く｣意味の両方で使わない
- 意味の多い単語は避ける
    - take, makeなど
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

![](./images/too_many_global_variable.png)

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

![forIf攻撃](./images/for_if_attack.png)

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

### 掃除の前に…

[ババ抜きのルールを確認する](https://ja.wikipedia.org/wiki/ババ抜き)

---

### 掃除の流れ

1. [表面上の改善](./contents/beginner/readableBabanuki_1.zip)
1. [解読・コメントを挿入](./contents/beginner/readableBabanuki_2.zip)
1. [適切な名前付け](./contents/beginner/readableBabanuki_3.zip)
1. [変数で分割する、スコープを縮める](./contents/beginner/readableBabanuki_4.zip)
1. [メソッド、ファイルで分割する](./contents/beginner/readableBabanuki_5.zip)
    - [アニメーション削除版](./contents/beginner/readableBabanuki_5_no_animations.zip)
1. 諸々


---

### 課題

#### **[可読性を高める](#/12)を参考にしてババ抜きをリーダブルにする**

- [掃除の流れ](#/28)にサンプルコードを掲載している
    - [2段階目](./contents/beginner/readableBabanuki_2.zip)をダウンロードして、3番目の｢適切な名前付け｣から各自取り組むこと
- サンプルコードは正解ではない 各自読みやすいコードを目指すこと
- クラスなど取り扱ってない項目を使用してもよい
- 構造やアルゴリズムを変えても良い
- 中級編で各自のリーダブルコードを使用する

|||

#### TIPS (随時更新)

- 名前付け
    - 表記を統一する (discard = throw, select = choose)
    - 番号 = number, 数 = count と使い分ける (本来どちらもnumber)
    - あえて冗長に名前付けする (hand = 手札だがhandCardとしてカードであることを示唆する)
    - 名前の置換はProcessingの機能だと不十分なので外部エディタを使うとよい
    - ファイル名も変えて良い
    - 単語の重複を避ける (drawは｢描く｣意味で使用しているのでカードを引く意味の｢draw｣は使わない)
    - 意味の多い単語は避ける (take, makeなど)

---

### プログラム解説

#### 構成要素

- カード(トランプ) [card]
    - 53枚 (ジョーカー1枚)
    - マーク [suit]
        - クラブ [club], ダイヤ [diamond], ハート [heart], スペード [spade], ジョーカー [joker]
    - 数字 [number]
        - A, 2, 3, ..., J, Q, K
    - 表裏の画像 [image]
- プレイヤー [player]
    - 2人
    - 手札(カード) [hand]
- (捨て)場 [field]
    - 一番上のカード

|||

#### ゲームの流れ

1. 53枚のカードをシャッフルする [shuffle cards]
2. カードをプレイヤーにそれぞれ配る [deal cards]
    - 片方が26枚、もう片方が27枚になる
3. お互いペアのカードを捨てる [discard cards]
4. 自分は相手の手札からカードを1枚選ぶ [select a card]
5. 選択したカードを引く [draw a card]
6. ペアのカードを捨てる
7. 相手も同様に4～6を行う

#### 終了条件

プレイヤーの1人を除いた全員の手札がなくなる

#### 勝利条件

ゲーム終了時点で手札にジョーカーがない

|||

#### ちなみに…

- 元のソースコードは構造上の問題で相当読みにくい
- 本来構造やアルゴリズムまで改善しないとリーダブルにはならない
- しかし構造やアルゴリズムが完全に理解できなくてもコメントを元に名前付けや分割はできる
- 中級編を受講する人で最後の行程までできなかった人は、サンプルコードを読んで備えておこう

---

# 中級編

### ババ抜きをクラスを使って整頓する

---

## 目次

<ol>
    <li><a href="#/33">初級編の振り返り</a></li>
    <li><a href="#/34">クラスで整頓する</a></li>
    <ol>
        <li><a href="#/35">クラスの効果</a></li>
        <li><a href="#/36">ババ抜きの構成を見る</a></li>
        <li><a href="#/37">一からクラスを構築する</a></li>
        <li><a href="#/38">setupメソッドの移行</a></li>
    </ol>
</ol>

---

## 初級編の振り返り

- 初級編は**可読性**を重視してリーダブルにした
- ボトムアップ方式でコードを分割していった
    - 先に動くコードを書いて後から分割する
- ソースが暗号に近い上にアニメーションの処理が複雑なため難解だった

|||

### 各工程での考察

#### 1. 表面上の改善

- ただの作業
- 行数が多いと後からこの部分を改善するのは面倒
- 最初から表面的に綺麗にしておくべき

#### 2-1. 解読

- 最も難しい工程
- 本来自分のコードは解読する必要ないので本意ではない

#### 2-2. コメントを挿入

- この段階では全てを理解する必要はない
- 大まかに何をやっているかだけ把握するためのコメント
- 疑問が浮かぶ箇所はメモしておくとよい

|||

#### 3. 適切な名前付け

- 最も悩む工程
- 人の好みが出やすく経験による
- 人のコードを読むことでも語彙が増える (TIPSも参照)

#### 4-1. 変数で分割する

- コードの横幅を狭める工程
- 変数による名前付けという効果もある
- この段階ではほとんどがifの条件文の分割

#### 4-2. スコープを縮める

- 変数の使用箇所を一つ一つ見る
- draw()内でしか使われてない変数は中級編で解決するのでスルー
- クラスなしではあまり効果が現れない

|||

#### 5-1. メソッドで分割する

- 最も効果が現れる工程
- コメントに沿って大まかなくくりで分ける

#### 5-2. ファイルで分割する
- 1ファイル当たりの行数を減らす工程

|||

### 初級編の成果

- [ここ](../beginner/readableBabanuki_5.zip)まで掃除できた
- しかし…
    - 22個のグローバル変数
    - 多くのフラグと一時変数
    - 多くのメソッドがvoidで引数が少ない
    - プレイヤーによって使うメソッドが異なる
    - 複雑なアニメーション
- ただ箱に詰めた感じが残る

---

## **クラス**で整頓する

---

### クラスの効果
- 似たような処理を共通化
- 可読性だけでなく拡張性も高められる

---

### 1. ババ抜きの構成を見る

- 初級編の[プログラム構成](#/30)に従って構築すればよい
- カード、プレイヤー、場の3つのクラスを作る

---

### 2. 一からクラスを構築する

- まず従来のコードは置いておいて枠組みだけ作る
- 1ファイル1クラスを守る
- ファイル名はクラス名と同じにする

#### 手順

1. クラスを作る、コメントを書く
2. インスタンス変数を作る
3. コンストラクタを作る
4. インスタンス化する

|||

#### サンプルコード [[ダウンロード]](./contents/intermediate/readableBabanuki_1.zip)

~~~processing
final int CARD_WIDTH = 100;  //カードの横幅
final int CARD_HEIGHT = 150;  //カードの縦幅

//プレイヤー数は変動しないので定義しない

Player [] players;  //プレイヤー
Player turnPlayer;  //現在のターン
Field field;        //場

void setup() {
  players = new Player [2];
  players[0] = new Player("YOU");
  players[1] = new Player("CP");
  turnPlayer = players[0];
  field = new Field();
}

void draw() {

}

/*
マーク:
  0: ジョーカー
  1: クラブ
  2: ダイヤ
  3: ハート
  4: スペード
数字:
  0: ジョーカー
  1: A
  2: 2
  ...
  10: J
  11: Q
  12: K
*/

//カード(トランプ)
class Card {
  final int SUIT;    //マーク
  final int NUMBER;  //数字
  final PImage SURFACE_IMAGE;  //表の画像(絵柄側)
  final PImage BACK_IMAGE;     //裏の画像
  
  Card(int suit, int number, PImage surfaceImage, PImage backImage) {
    SUIT = suit;
    NUMBER = number;
    SURFACE_IMAGE = surfaceImage;
    BACK_IMAGE = backImage;
  }
}

//捨て場
class Field {
  Card topCard;
  
  Field() {
  }
}

//プレイヤー
class Player {
  final String NAME;  //名前
  ArrayList<Card> handCards;  //手札
  
  Player (String name) {
    NAME = name;
    handCards = new ArrayList<Card>();
  }
}
~~~

---

### 3. setupメソッドの移行

- 初級編で作ったコードから移行を始める
- なお単純化のためサンプルでは[アニメーション削除版](./contents/beginner/readableBabanuki_5_no_animations.zip)を使用する
- まずはゲームの初期化を含むsetupメソッドから
- 基本的には従来のアルゴリズムを継承するべきだが、自分でよりよいアルゴリズムが思いつけばそれを採用してもよい
- 名前はできるだけ従来のコードを真似すること

|||

#### [サンプルコード](./contents/intermediate/readableBabanuki_2.zip)

~~~processing
import java.util.Collections;

final int CARD_WIDTH = 100;  //カードの横幅
final int CARD_HEIGHT = 150;  //カードの縦幅

//プレイヤー数は変動しないので定義しない

Player [] players;  //プレイヤー
Player turnPlayer;  //現在のターン
Field field;        //場

void setup() {
  size(640, 640);
  textSize(30);

  players = new Player [2];
  players[0] = new Player("YOU");
  players[1] = new Player("CP");
  turnPlayer = players[0];
  field = new Field();

  dealCards( createCards() );  //カードを配る
  //プレイヤーそれぞれペアを捨てる
  for (int i = 0; i < 2; i++) {
    Player player = players[i];
    discardPairCards(player);
  }
}

void draw() {

}

/*
マーク:
  0: ジョーカー
  1: クラブ
  2: ダイヤ
  3: ハート
  4: スペード
数字:
  0: ジョーカー
  1: A
  2: 2
  ...
  10: J
  11: Q
  12: K
*/

//カード(トランプ)
class Card {
  final int SUIT;    //マーク
  final int NUMBER;  //数字
  final PImage SURFACE_IMAGE;  //表の画像(絵柄側)
  final PImage BACK_IMAGE;     //裏の画像
  
  Card(int suit, int number, PImage surfaceImage, PImage backImage) {
    SUIT = suit;
    NUMBER = number;
    SURFACE_IMAGE = surfaceImage;
    BACK_IMAGE = backImage;
  }
}

//捨て場
class Field {
  Card topCard;
  
  Field() {
  }
}

//プレイヤー
class Player {
  final String NAME;  //名前
  ArrayList<Card> handCards;  //手札
  
  Player (String name) {
    NAME = name;
    handCards = new ArrayList<Card>();
  }
}

//ペアを捨てる
void discardPairCards(Player player) {
  ArrayList<Card> handCards = player.handCards;

  for (int i = 0; i < handCards.size(); i++) {
    Card card1 = handCards.get(i);
    for (int j = i+1; j < handCards.size(); j++) {
      Card card2 = handCards.get(j);
      if (card1.NUMBER == card2.NUMBER) {
        handCards.remove(card1);
        handCards.remove(card2);
        i--;
        break;
      }
    }
  }
}

//カードをプレイヤーに配る
void dealCards(ArrayList<Card> cards) {
  Collections.shuffle(cards);  //カードをシャッフルする
  
  for (int i = 0; i < cards.size(); i++) {
    //交互に配る
    Player player = players[i%2];
    Card card = cards.get(i);
    player.handCards.add(card);
  }
  
  //山札をシャッフルしたので手札をシャッフルする必要はない
}

//カードの生成 (画像の読み込み)
ArrayList<Card> createCards() {
  ArrayList<Card> cards = new ArrayList<Card>();
  PImage backImage = loadImage("back_red.gif");  //カード裏の画像
  
  //ジョーカーの追加
  Card jokerCard = new Card(0, 0, loadImage("joker_red.gif"), backImage);
  cards.add(jokerCard);
  
  //ジョーカー以外のカードの追加
  for (int suit = 1; suit <= 4; suit++) {
    String suitName = "";
    switch(suit) {
      case 1:
        suitName = "club";
      break;
      case 2:
        suitName = "diamond";
      break;
      case 3:
        suitName = "heart";
      break;
      case 4:
        suitName = "spade";
      break;
    }
    
    for (int num = 1; num <= 12; num++) {
      String path = suitName + num + ".gif";
      Card card = new Card(suit, num, loadImage(path), backImage);
      cards.add(card);
    }
  }
  
  return cards;
}
~~~

|||

#### [補足] `discardPairCards`について
- ペアを捨てるメソッドだが実装方法がいくつかある
- 2つの組を捨てるため3つの組がある場合どれか1つは捨ててはならないことに注意

|||

#### リストから重複する値のペアを探索して削除するアルゴリズム
##### [ダウンロード](contents/intermediate/discardPairCards_algorithm.zip)
~~~processing
/*
before: 1, 2, 3, 2, 4, 2, 3
after: 1, 4, 2 (順不同)
*/

ArrayList<String> sourceList = new ArrayList<String>();
sourceList.add("1");
sourceList.add("2");
sourceList.add("3");
sourceList.add("2");
sourceList.add("4");
sourceList.add("2");
sourceList.add("3");

//例1: 二重for文とremove(int index)を使う方法
ArrayList<String> list = new ArrayList<String>(sourceList);
for (int i = 0; i < list.size(); i++) {
  String str1 = list.get(i);
  for (int j = i+1; j < list.size(); j++) {
    String str2 = list.get(j);
    if (str1.equals(str2)) {
      list.remove(i);
      list.remove(j-1);
      i--;
      break;
    }
  }
}

//例2: 二重for文とremove(Object o)を使う方法
list = new ArrayList<String>(sourceList);
for (int i = 0; i < list.size(); i++) {
  String str1 = list.get(i);
  for (int j = i+1; j < list.size(); j++) {
    String str2 = list.get(j);
    if (str1.equals(str2)) {
      list.remove(str1);
      list.remove(str2);
      i--;
      break;
    }
  }
}

//例3: 二重for文とremoveAll(Collection<?> c)を使う方法
list = new ArrayList<String>(sourceList);
ArrayList<String> pairList = new ArrayList<String>();
for (int i = 0; i < list.size(); i++) {
  String str1 = list.get(i);
  for (int j = i+1; j < list.size(); j++) {
    String str2 = list.get(j);
    if (str1.equals(str2)) {
      pairList.add(str1);
      pairList.add(str2);
      i--;
      break;
    }
  }
}
list.removeAll(pairList);
~~~

|||

#### [余談] アルゴリズムの実装について
- 基本的には実際にプレイする様子を思い浮かべてその通りに実装すればよい
    - `dealCards`の場合、山札をシャッフルして交互に配る
    - ランダムに何かする = `random()`を使うではない
- リアルな行為に近いアルゴリズムは直感的で分かりやすい
- 効率と可読性、拡張性はしばしトレードオフになる


---

## 参考文献

- [リーダブルコード](https://www.amazon.co.jp/dp/4873115655/ref=wl_it_dp_o_pC_nS_ttl?_encoding=UTF8&colid=E8HOB3NQ55TV&coliid=I1K6HSWVGJK4QW), オライリージャパン
- [良いコードを書く技術](https://www.amazon.co.jp/良いコードを書く技術-読みやすく保守しやすいプログラミング作法-WEB-DB-PRESS-plus/dp/4774145963/ref=sr_1_1?s=books&ie=UTF8&qid=1502903104&sr=1-1&keywords=良いコードを書く技術), 技術評論社