# はじめてのRailsアプリ

---

## アプリケーションを作る

```bash
$ mkdir projects
$ cd projects
$ rails new my_first_app
$ cd my_first_app
$ rails server
```

---

## アプリケーションを作る(説明)

```bash
$ mkdir projects           # projectsディレクトリの作成
$ cd projects              # projectsディレクトリに移動
$ rails new my_first_app   # railsコマンドによりアプリケーションを新規作成
$ cd my_first_app          # アプリケーションのディレクトリに移動
$ rails server             # アプリケーションを起動
```

`http://localhost:3000`へアクセス

---

## Ideaのscaffoldをする

```bash
$ rails generate scaffold idea name:string description:text picture:string
```

```bash
rake db:migrate
rails server
```

`http://localhost:3000/ideas`へアクセス

---

## デザインする

---

### [Twitter Bootstrap](http://getbootstrap.com/)を使えるようにする

`app/views/layouts/application.html.erb`に下記を追記

```ruby
<link rel="stylesheet" href="//railsgirls.com/assets/bootstrap.css">        <%# 追記 %>
<link rel="stylesheet" href="//railsgirls.com/assets/bootstrap-theme.css">  <%# 追記 %>
<%= stylesheet_link_tag "application", media: "all", "data-turbolinks-track" => true %>
```

```ruby
<div class="container">  <%# 追記 %>
  <%= yield %>
</div>                   <%# 追記 %>
```
---

### ナビゲーションバーの追加

`app/views/layouts/application.html.erb`の`<body>`の直後に下記を追記

<nav class="navbar navbar-default navbar-fixed-top" role="navigation">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="/">The Idea app</a>
    </div>
    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <li class="active"><a href="/ideas">Ideas</a></li>
      </ul>
    </div>
  </div>
</nav>
```

---
### フッターの追加

`app/views/layouts/application.html.erb`の`</body>`の直前に下記を追記


```
<footer>
  <div class="container">
    Rails Girls 2015
  </div>
</footer>
<script src="//railsgirls.com/assets/bootstrap.js"></script>
```

---

### 表に枠線を追加

`app/assets/stylesheets/application.css`に下記を追記


```css
body { padding-top: 100px; }
footer { margin-top: 100px; }
table, td, th { vertical-align: middle; border: none; }
th { border-bottom: 1px solid #DDD; }
```

---

### 確認してみる

`http://localhost:3000/ideas`へアクセス

---

## 写真アップロード機能を追加

---

### gemの追加

`Gemfile`を開き、`group :development, :test do`の直前に`下記を追加

```
gem 'carrierwave'
```

gemをインストール

```
bundle install
```
---

### アップロード用コードの生成

```bash
rails generate uploader Picture
```

---

### アップロード用コードの生成

```bash
rails generate uploader Picture
```

`app/models/idea.rb`の`class Idea < ActiveRecord::Base`の直下に下記を追記

```ruby
mount_uploader :picture, PictureUploader
```

---

### フォームから写真をアップロードできるようにする

`app/views/ideas/_form.html.erb`を開いて、`<%= f.text_field :picture %>`を下記に書き換える。

```erb
<%= f.file_field :picture %>
```

場合によっては…

`<%= form_for(@idea) do |f| %>`を下記に変える。

```
<%= form_for @idea, :html => {:multipart => true} do |f| %>
```

---

### アップロードした写真を見れるようにする

`app/views/ideas/show.html.erb`の`<%= @idea.picture %>`を下記に変える。

```erb
<%= image_tag(@idea.picture_url, width: 600) if @idea.picture.present? %>
```

---

## トップページにアクセスしたときに`/ideas`を表示

`http://localhost:3000/ideas`へアクセスすると、微妙なページ。
主たるコンテンツの`idea`一覧ページにしたい。

`config/routes.rb`の2行目に下記を追加。

```
root to: redirect('/ideas')
```
`http://localhost:3000/ideas`へアクセス。

---

## 開発者の情報を表示できるようにする

```bash
rails generate controller pages info
```

`app/views/pages/info.html.erb`を編集して、自己紹介を入れてみる。

```
<h1>About me</h1>
<p>
  <img src="http://gravatar.com/avatar/6d5dbb7f4489227b5e85860f37bceb52?s=120">
</p>
<p>
  ken1flan
</p>
```

`http://localhost:3000/pages/info`にアクセスしてみる

---

## 参考

[Rails Girls インストールレシピ](http://railsgirls.jp/install/)

