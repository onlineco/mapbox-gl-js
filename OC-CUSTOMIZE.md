# カスタマイズ内容

## 目的

渋滞情報はExpiresヘッダーに従って更新される
渋滞情報の更新頻度を下げて、課金を抑えたい
Tiles.setExpiryData (tile.js)で、渋滞情報の有効期限が指定されるので、この有効期限をExpiresから延長する

## メモ

### コード分析

ui/map.js
refreshExpiredTiles
mapboxglをスタンドアローンライブラリで使う場合、はコンストラクタでしか効果がない

source/sourec_cache.js
_setTileReloadTimerで有効期限切れデータのリロードタイマーが登録される

source/tiles.js
setExpiryDataでExpiresヘッダーに従って有効期限が設定される

source/vector_tile_source.js
loadTile.doneでmap.refreshExpiredTilesがtrueなら有効期限を設定する
 

### Chrome Developer Tool

Networkで、"mapbox-traffic"で絞り込むと渋滞情報の更新が確認できる
Consoleで下記コマンドを実行するとリロード用タイマーが確認できる
map.style.sourceCaches["mapbox://mapbox.mapbox-traffic-v1"]._timers

# ビルド

## 準備
node
```bash
cd mapbox-gl-js &&
yarn install
```

## 開発用

```bash
yarn run build-prod
```

## リリース用

```bash
yarn run build-prod-min
```

下記ファイルが生成される
dist/mapbox-gl.js
dist/mapbox-gl.js.map