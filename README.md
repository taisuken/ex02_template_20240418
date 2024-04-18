# プログラミング演習 Ⅱ 第 ? 回

プログラミング演習の課題提出用のリポジトリ

## 提出方法

下記コマンドを実行すると、正しくコンパイル・実行可能なコードの場合に自動で採点が開始される

```bash
./submit.sh
```

## ローカルでのテスト方法

下記コマンドを実行すると、正しくコンパイル・実行可能なコードで正しい出力をするかを確認出来る

```bash
./test_all.sh
```

## 注意点

全ての課題で以下の項目を確認しており、違反が見られた場合にはその回の課題を 0 点とする

- locked ディレクトリ配下, test_all.sh, submit.sh は一切編集をしないこと

### template 手順 (※ 以下は Class 作成後に消すこと)

※ 以下の具体的なコードは **ex01-1** のものを使用。

※ make コマンドが使える環境を想定。使えない場合は以下を実行。

```bash
sudo apt install make
make --version
```

### 1: このリポジトリをベースに template リポジトリを作成して Clone

![スクリーンショット 2024-04-14 001713](https://github.com/test-prog2/2024_Proexe2_Template_thirofoo/assets/83126064/d32bcb90-6e67-4154-83e0-97083a56ad3f)

### 2: make コマンドで template を展開

```bash
# ⇓ ex{SESSION} で課題の数が NUM_FILES 個の template を展開
make create_template SESSION=1 NUM_FILES=1
```

### 3: 模範解答の c ファイルをコピーしてセット

```c
// ex) ex01_1.c
#include <stdio.h>

int main(void)
{
    int n1, n2;

    printf("二つの整数を入力してください．\n");
    printf(" 整数 1: ");
    scanf("%d", &n1);
    printf(" 整数 2: ");
    scanf("%d", &n2);
    printf(" それらの和は %d です． \n", n1+n2);

    return 0;
}
```

### 4: テストの input をハンドメイドで作成

2 の工程で ./locked/cases/{ASSIGNMENT}/in というディレクトリに 0~5.txt が存在しているはずなので、ハンドメイドでも乱択でも良いので入力情報を入れる。

### 5: make コマンドで出力生成 & Hash 化

```bash
# ASSIGNMENT.c の出力を SHA-256 で Hash 化
make test_hash ASSIGNMENT=ex01_1
```

実行後に ./locked/cases/{ASSIGNMENT}/out の中に Hash 化されたテストケースがあれば完了。

{ASSIGNMENT}_test というディレクトリも同時に作成され、そこには Hash 化する前の出力結果が入っているので、必要に応じてその結果を違う場所に補完することをお勧めする。

### 6: C ファイルを生徒用に直す & 生徒に見せたくない情報を削除

### 7: (任意) .gitignore の追加

6 までの工程を終えて commit をした後に以下の .gitignore を追加 & commit をしておくと、生徒の誤 push 防止として機能するので一番最後に作成を推奨。"ex01" の部分は各回に合わせて変更すること。

```bash
*
!ex01_*.c
```

## 補足

- 入力が無いケース・『正しく動くようにしましょう』みたいなケースは個々で書き換えるしかない
- 以下を実行すると create_template を実行する前の環境まで戻る

```bash
make clear
```

- あくまで template の為、output を違うものにしたい場合は自由にカスタマイズするので OK
