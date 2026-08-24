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


ページ上部にある「Settings」から、左メニューの「Collaborators」を開く。
<img width="1920" height="1032" alt="スクリーンショット 2026-08-24 100311" src="https://github.com/user-attachments/assets/db926b65-68b5-4691-bebe-5e0806049604" />


パスワードを求められたら入力をし、「Add people」ボタンを押し、B のGitHubのユーザー名またはメールアドレスを入力して招待する。

Aから届いた招待で、ポジトリへの招待を「Accept invitation」するとBもリポジトリに対してPushができるようになる。
<img width="284" height="123" alt="スクリーンショット 2026-08-20 170735" src="https://github.com/user-attachments/assets/791c8010-388c-495a-92e4-5b9cd5b0c8b2" />

### 2: 実際の開発の流れ
準備ができたら手順道理に進める。

#### Aが初期コードをpushする。

```
git add index.html
git commit -m "first commit"
git branch main
git push -u origin main
```
#### Bがクローンして作業ブランチで開発する

```
git clone <リポジトリのURL>
cd <リポジトリ名>
git branch develop
git switch develop
vi index.html
git add index.html
git commit -m "add index.html"
git push origin develop
```

#### プルリクエストでマージする
Aは、GitHub上で「Compare & pull request」を押し、追加や修正の内容を確認し、「Merge pull request」を押して、mainに反映させる。
#### ※ 「Compare & pull request」が出ない場合
「Compare & pull request」が出ない場合は、ページ上部の「Pull recuests」から、「New pull request」を開く。

<img width="1920" height="1032" alt="スクリーンショット 2026-08-21 092141" src="https://github.com/user-attachments/assets/cfd0a229-32ee-4c03-9fda-0dc7bd625189" />

「Compare changes」の「base」はmainにし、「compare」はpushした際の作業用ブランチ（develop）を選択する。正しく差分が表示されたら「Create pull request」を押すことでマージが完了する。



## 参考
https://docs.github.com/ja/pull-requests/reference/pull-requests
