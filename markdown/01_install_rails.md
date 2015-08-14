class: center, middle

# Railsのインストール
(for Mac)

---

## コマンドラインツールをインストール

```bash
$ xcode-select --install
```

---

## Homebrewをインストール

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

---

## Homebrewをインストール

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

---

## rbenvをインストール

```bash
brew update
brew install rbenv rbenv-gem-rehash ruby-build
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
echo 'export PATH="$HOME/.rbenv/shims:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
```

---
## Rubyをインストール

```bash
rbenv install 2.2.1
```

---
## デフォルトのRubyを設定

```bash
rbenv global 2.2.1
```

---
## Railsのインストール

```bash
gem i rails --no-ri --no-rdoc
```

---

## 参考

[Rails Girls インストールレシピ](http://railsgirls.jp/install/)
