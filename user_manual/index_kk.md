EL エミュレータ 非公認改造説明
===============
2025-09-24

---------------------------------------
## 目次

* [本ドキュメントについて](#本ドキュメントについて)
* [Doker環境での起動](#docker-environment)
* [WebAPI経由ELデバイスのプロパティアクセス](#webapi経由elデバイスのプロパティアクセス)
* [To Do](#to-do)

---------------------------------------
## <a id="about">本ドキュメントについて</a>

神奈川工科大学 (KAIT) スマートハウス研究センターの ECHONET Lite 機器エミュレータ (https://github.com/KAIT-HEMS/elemu) の独自拡張説明資料です。

## <a id="docker-environment">Doker環境での起動</a>

* Windows 11 Pro 上で docker desktop で、Controller 用 Device 用２つのエミュレータを起動するようにしました。
elemu ディレクトリで以下を実行してください。
```
$ docker compose build
$ docker compose up -d
```
* Controller 用 Device 用いずれも初回起動時は蓄電池デバイスが１台登録されるようにしています（KAITのエミュレータは家庭用エアコンでしたが変更しています）。Controller 用については、初回起動時に、正式ユーザマニュアルの [コントローラ](index.md#%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%A9) を参考にした修正が必要です。
* Dockerでビルドするたびにエミュレータが初期化されないよう、ホスト側の ./data/controller, ./logs/controller, ./data/device, ./logs/controller にデータを保存するようにしています。

## <a id="webapi-to-drDevices">WebAPI経由ELデバイスのプロパティアクセス</a>

* WebAPIで ECHONET Liteのリモートデバイスに対してプロパティアクセスが可能です。
* まず、コントローラ用エミュレータのUIから、リモートデバイスの機器探索をする必要があります。この探索により、リモートデバイスのEOJとIPアドレスの紐づけがされます。
デプロイ後も、必ずコントローラ用エミュレータ画面から、機器探索を再度実行するようにしてください。
* APIは以下の通り
```
GET {baseUrl}/api/drDevices/{eoj_id}/properties/{epc_id もしくは MRA で定義されたプロパティ名}
```
```
PUT {baseUrl}/api/drDevices/{eoj_id}/properties/{epc_id もしくは MRA で定義されたプロパティ名}
Content-Type: application/json

{
  "edt": "16進数を先頭0xなしで、正しい桁数で設定"
}
```

## <a id="to-do">To do</a>

* 独立した別メソッドで、コントローラ側で何等かの処理をして、[WebAPI経由ELデバイスのプロパティアクセス](#webapi経由elデバイスのプロパティアクセス)等の処理をしたい。現行エミュレータへの影響を与えずに処理を追加したい。
* 時刻指定によるコントローラ用エミュレータのスケジュール動作実現。現行エミュレータへの影響を与えずに処理を追加したい。
* OpenAPI利用による動作定義。現行エミュレータへの影響を与えずに処理を追加したい。
* [優先度低] Docker初回起動時に、コントローラ用エミュレータとデバイス用エミュレータで、起動時の設定を変えたい