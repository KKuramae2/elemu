EL エミュレータ 非公認改造説明
===============
2025-09-22

---------------------------------------
## 目次

* [本ドキュメントについて](#本ドキュメントについて)
* [Doker環境のでの起動](#docker-environment)

---------------------------------------
## <a id="about">本ドキュメントについて</a>

神奈川工科大学スマートハウス研究センターの ECHONET Lite 機器エミュレータ (https://github.com/KAIT-HEMS/elemu) の独自拡張説明資料です。

## <a id="docker-environment">Doker環境のでの起動</a>

* Windows 11 Pro 上で docker desktop で、Controller 用 Device 用２つのエミュレータを起動するようにしました。
elemu ディレクトリで以下を実行してください。
```
$ docker compose build
$ docker compose up -d
```
* Controller 用については、初回起動時に、正式ユーザマニュアルの [コントローラ](index.md#%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%A9) を参考にした修正が必要です。
* git clone 後にエミュレータを起動すると、data フォルダにエミュレータのデータファイルが作成されます。
doker compose 時に影響が出る可能性があるので、git clone 後、Docker環境以外でエミュレータを起動しないようにしてください。
* 現状、Dockerでビルドするたびに再構築が必要になるのが課題です。