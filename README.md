# 共有リポジトリモデル
## モデルの概要
共有リポジトリモデルとはGit及びGithubを用いてチーム開発を行うための手段である。
プロジェクトに参加するメンバー全員が、共通のリポジトリに対するPush権限を持っている。メンバーは１つの共有リポジトリへのプッシュアクセス権を持ち、変更が必要なときに作業用ブランチを作成する。
プルリクエストは、変更がmainブランチにマージされる前にコードレビューと一連の変更をほかのメンバーに確認してもらい、テストを走らせてから取り込むことができる。
このモデルは、プライベートプロジェクトで共同作業を行う小規模なチームや信頼できるメンバー同士のプロジェクトに向いている。

## 役割及び手順
### 役割分担
* **A　(リード役)** 

* **B　(開発者)** 

### 手順
1. AがGitHub上にリモートリポジトリを用意し、index.html（"Hello"と記述）をmainブランチにPushする。
2. Bがリポジトリをcloneし、作業ブランチを作成。index.htmlを編集してPushし、Aへプルリクエストを出す。
3. AがBのプルリクエストをレビューし、mainブランチにマージする。
4. Aがローカルのmainブランチを最新化（pull）し、作業ブランチを作成。index.htmlを編集してPRを作成・マージする。
5. Bがローカルのmainブランチを最新化（pull）し、作業ブランチを作成。stylesheet.cssを追加してAへプルリクエストを出す。
6. AがBのプルリクエストをレビューし、mainブランチにマージする。

## 演習

### 1: リポジトリの作成と招待
AがGitHub上にリモートリポジトリを作成する。今回はGitで作成した。
<img width="987" height="244" alt="スクリーンショット 2026-08-24 095233" src="https://github.com/user-attachments/assets/f483b3fb-6a85-402d-9073-7e64bc94a270" />


リポジトリができたらGitHub上で出来ているかを確認し、そのリポジトリを開く。
<img width="927" height="101" alt="スクリーンショット 2026-08-24 095310" src="https://github.com/user-attachments/assets/71b8dee9-00c2-4183-ae7f-132d99a85fa1" />



ページ上部にある「Settings」から、左メニューの「Collaborators」を開く。
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 100311" src="https://github.com/user-attachments/assets/db926b65-68b5-4691-bebe-5e0806049604" />


パスワードを求められたら入力をし、「Add people」ボタンを押し、B のGitHubのユーザー名またはメールアドレスを入力して招待する。
<img width="639" height="174" alt="スクリーンショット 2026-08-24 095500" src="https://github.com/user-attachments/assets/d00668aa-f231-4796-9f3c-8393aaa410f5" />
<img width="630" height="180" alt="スクリーンショット 2026-08-24 095533" src="https://github.com/user-attachments/assets/ec62095b-003e-4277-bca1-05c57d030aef" />


Aから届いた招待で、ポジトリへの招待を「Accept invitation」するとBもリポジトリに対してPushができるようになる。
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 095827" src="https://github.com/user-attachments/assets/b70a6e2b-c08c-45d8-b960-e92b39963f69" />
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 095653" src="https://github.com/user-attachments/assets/8e103266-8511-4837-9633-ef793f7d1996" />


### 2: 実際の開発の流れ
準備ができたら手順道理に進める。

#### Aが初期コードをpushする。

```
echo "Hello" >> index.html
git add index.html
git commit -m "first commit"
git branch main
git push -u origin main
```
#### Bがクローンして作業ブランチで開発する

```
git clone <リポジトリのURL>
cd <リポジトリ名>
git branch develop # 適当なブランチ名
git switch develop
vi index.html # ファイルの編集
git add index.html
git commit -m "add index.html"
git push origin develop
```

#### プルリクエストでマージする
GitHub上で「Compare & pull request」を押し、追加や修正の内容を確認し、「Create pull request」をしてから、「Merge pull request」を押して、mainブランチに反映させる。
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 102257" src="https://github.com/user-attachments/assets/5cfccf0c-49e7-406e-914c-a2dda3fc29a2" />
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 102314" src="https://github.com/user-attachments/assets/5b22ba6e-e8dd-41f3-8ab3-7bbd5ff5c4d5" />
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 102410" src="https://github.com/user-attachments/assets/7486115b-036f-4887-be35-745a0248578b" />

#### ※ 「Compare & pull request」が出ない場合

「Compare & pull request」が出ない場合は、ページ上部の「Pull recuests」から、「New pull request」を開く。

<img width="1920" height="1032" alt="スクリーンショット 2026-08-21 092141" src="https://github.com/user-attachments/assets/cfd0a229-32ee-4c03-9fda-0dc7bd625189" />

「Compare changes」の「base」はmainにし、「compare」はpushした際の作業用ブランチ（develop）を選択する。正しく差分が表示されたら「Create pull request」を押すことでマージが完了する。

#### Aがローカルのmainブランチを最新化し、作業ブランチを作成。index.htmlを編集・マージする。

```
git pull origin main
git branch develop2
git switch develop2
vi index.html
git add index.html
git commit -m "add index.html"
git push origin develop2
```

プッシュ後に、先ほどと同じ過程を通し、マージを行う。

#### Bがローカルのmainブランチを最新化し、作業ブランチを作成。stylesheet.cssを追加しプルリクエストを出す。
```
git pull origin main
git switch develop
echo "hello" >> stylesheet.css
git add stylesheet.css
git commit -m "add stylesheet.css commit"
git push -u origin develop
```
#### AがBのプルリクエストをレビューし、mainブランチにマージする。
Bが新しいファイルを作成してもは寧されていることがわかる。

## 参考
* (2025/11/28)「つくって、壊して、直して学ぶ Git＆GitHub 入門」　高橋あおい　9784798191584
* https://docs.github.com/ja/pull-requests/reference/pull-requests
