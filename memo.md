## 初級編

### BADCODEの定義
- 詰まったコード (空白のないコード)
    - 表面上の改善
- 一行が長い、{}内が長い
    - 変数、メソッド、クラスにより分割
- 解読できない
    - 名前による改善
- コメントが少なすぎる/多すぎる
    - コメントで説明する
- 文字がインデントで右側に寄りすぎている
    - break, continue, returnで早く返す
    - メソッド、クラスによる分割
- グローバル変数が多すぎる
    - 変数のスコープを縮める
- 3次以上の配列を使っている
    - クラスを作る

Note:
グローバル変数とローカル変数の説明

### 表面上の改善 (★☆☆)

#### スペース
- 算術演算子以外の演算子の前後 (=, >, ==, !=...)
- ,の後
- ( hoge.fuga() ) (カッコが被るとき)
    - [], <>の後(前)
    - if, for, whileの後
    - 算術演算子の前後
    - {}の前後

#### 空行
- メソッドの前後
- 区切りをつけたいとき

#### インデント下げ
- {の次の行

### ファイルによる分割 (Processing特有) (★☆☆)
- クラスごとに分ける
- `setup()` と `draw()` は `main`、`key`, `mouse`関係は `input` など
- 本来は全てクラス化させることが望ましい

### 変数で説明する (★☆☆)
- 変数は行為を説明する道具
- 変数は式を分割する

```java
[before]
if ( squares.get( squares.size()-1 ).getValue() == 0 ) ...

[after]
Square lastSquare = squares.get( squares.size()-1 );
if (lastSquare.getValue() == 0) ...
```

```java
[before]
if (leftPosition < mouseX && rightPosition >= mouseX) ...

[after]
boolean inRange = leftPosition < mouseX && rightPosition >= mouseX;
if (inRange) ...
```

### 名前による改善 (★★☆)
- 名前の種類
    - キャメルケース
        - `drawImage`
        - 単語の先頭を大文字から始める (最初は小文字)
    - スネークケース
        - `draw_image`
        - 単語の間に `_` を使う
    - 好みでどちらかに従う
    - クラスは先頭だけ大文字
    - 定数は全て大文字、必ずスネークケース
- 分かりづらい省略をしない
    - string -> str, number -> num ぐらいは分かるが
    - score -> sc, background -> bg はやめよう
- グローバル変数は長く、ローカル変数は短く
    - ローカルとグローバル変数で重複するのを防ぐ
- 一文字の変数は使わない (for, whileのi, jなどを除く)
- 名前に形容詞をつける
    - x, y, size, numberだけでは分からない
- 意味を成さない単語を使わない
    - flag, switch, temp, aaaなど
    ```java
    [before]
    boolean drawingFlag = false;    //boolean型なんだからflagなのは自明

    [after]
    boolean drawing = false;
    ```
- (ローマ字を使わない)
    - ローマ字否定派と容認派がいる
    - ほとんどの言語は英語でできているので、個人的には否定派
    - [プログラミングでよく使う英単語のまとめ](http://qiita.com/Ted-HM/items/7dde25dcffae4cdc7923)
    - [うまくメソッド名を付けるための参考情報](http://qiita.com/KeithYokoma/items/2193cf79ba76563e3db6)

### コメントで説明する (★★☆)
- コメントはコードの補助的に説明する方法
- コメントは多すぎても少なすぎてもいけない
    - コメントしなくても分かるようなことは書かない
- 用途
    - メソッド、メソッドの引数、クラスの説明
    - 分かりづらい複雑な処理の説明
    - 既定値の説明 (`int MAX_LENGTH = 2;  //なんで2なのか書く`)
    - 欠陥の説明 (//～～のときバグが発生する)

### ifの並び順 (★☆☆)
- 定数を右側に
    ```java
    if (max > 10) ...
    if (posX > maxX) ...
    ```

### break, continue, returnで早く返す (★★☆)
- for, while文を途中で抜けるのがbreak、スキップして次のループに行くのがcontinue
- メソッド内で複数のreturnを使う
~~~java
[before]
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

[after]
for (int i = 0; i < chains.size(); i++) {
    int chain = chains.get(i);
    if (chain == null) {    //例外なら早く次にスキップさせる
        emptyCounter++;
        continue;
    }

    ...     //通常処理のネストが下がる
}
~~~
~~~java
[before]
int compare(int n, int m) {
    int r = -1;
    if(n >= m)
        r = 0;
    if(n > m)
        r = 1;
    return r;
}

[after]
int compare(int n, int m) {
    if (n > m) return 1;
    if (n < m) return -1;
    return 0;   //(n == m)のとき
}
~~~

### 無駄を削除する (★★★)
- コメントアウトしたコードを削除する
- 無駄な処理を削除する

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
- グローバル変数だらけの例

![](./images/too_many_global_variable.png)
- スコープを縮める例
~~~processing
[before]
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

[after]
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

- 変数のスコープを縮めると
    - 変数の宣言と使用が近くなるので分かりやすい
    - 変数を間違って書き換えにくくなる
- グローバル変数は全てメインファイルの先頭に
    - メソッドとメソッドの間はNG 

Note:
公園のフリーマーケットとスーパーマーケットの違い  
どちらも"変数"を売ってるとする どちらが安全か

### メソッド (★★☆)
- メソッドはコードを分割する箱
    - 結果的にネストが浅くなる
- メソッド化する = その処理を名前で説明する

~~~processing
[before]
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

[after]
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

- メソッド化が必要なとき
    - {}の中が50行を超える
    - ネストが4[マトリョーシカ](https://ja.wikipedia.org/wiki/マトリョーシカ人形)になる
    - 似たような処理がある
- メソッドを使うべきありがちな状況
    - setup(), draw(), keyPressed()内が長すぎる
    - 読者への怒濤のfor, if攻撃
    - ![forIf攻撃](images/for_if_attack.png)
    - ifの条件が長い
- 引数と返り値について
    - メソッドの基本: 何かを与えたら何かを返してくる
        - インプット: 引数
        - アウトプット: 返り値
        - 返り値なし(void)、引数なしの時はグローバル変数を処理している可能性が高い
            - ローカル変数やクラスで変数のスコープを縮める
    - メソッドの基本2: 1メソッド1処理
        - 複数のことをやらない
- [参考](http://qiita.com/Mic-U/items/1ec901864d4ab11c8d6f)

### TIPS

#### ifからswitchに変える
- 同じ変数の条件分岐をする場合、switch文を使うと分かりやすくなる
~~~processing
[before]
void keyPressed() {
    if (key == 'a') {
        //処理A
    } else if (key == 'b') {
        //処理B
    } else {
        //処理C
    }
}

[after]
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
- ifと違い、==(等価)しか判定できない
- nullは条件に指定できない
- breakをしないと次のcaseに行ってしまう
    - breakしない記述は分かりづらいためやめよう

#### {}の省略 (場合による)
- {}内が一行の場合、{}を省略できる
- 好みの部分が大きい
~~~processing
[before]
for (int i = 0; i < array.length; i++) {
    if (array[i] == 0) {
        continue;
    }

    ...
}

[after]
for (int i = 0; i < array.length; i++) {
    if (array[i] == 0) continue;

    ...
}
~~~
- elseを使っているときはやめよう
~~~processing
[BADCODE]
for (int i = 0; i < array.length; i++) {
    if (array[i] == 0) println("zero");
    else if (array[i] > 0) println("plus");
    else println("minus");
}
~~~

#### final
- 変数にfinalをつけると変更不可、つまり定数になる
- より安全に変数を扱うことができる
~~~processing
final String IP_ADDRESS = "localhost";
IP_ADDRESS = "192.168.0.1";     //エラー
~~~
- オブジェクトの中身は書き換えられてしまう
~~~processing
final int [] ADDRESSES = {
    "192.168.0.2", "192.168.0.3"
};
ADDRESSES[0] = "localhost";     //エラーなし
~~~
- 定数の配列は列挙型によって実装できる (上級編で扱う)