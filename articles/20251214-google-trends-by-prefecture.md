---
title: "Google Trendsを使って検索トレンドを都道府県別に比較する方法"
emoji: "📐"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["データ分析", "Python"]
published: true
---
## 1. はじめに
Google検索で使われる検索ワードのトレンドの推移を把握したいと思ったとき、[Google Trends](https://trends.google.com/)が使えることを知りました。しかし、UI経由で利用すると、2つの理由から6つ以上のキーワードの人気度を比較するのが難しいという課題がありました。
1. 1回に入力できるキーワード数は最大で5つまでである
2. キーワードの人気度（0～100）は絶対値ではなく、入力したキーワード間の相対値である

![](/images/20251214-google-trends-by-prefecture/pic1.png)
*UI経由で5つのキーワードの人気度を比較した結果*

この記事では、Pythonを利用して、API経由で6つ以上のキーワードの人気度を比較可能な形式で取得する方法を紹介します。

## 2. スクリプトの解説
今回はGoogle Colaboratoryを使います。また、Google Trendsには公式のパブリックAPIは提供されていませんが、非公式ながら広く使われているライブラリの`pytrends`を使ってデータ取得します。

### `pytrends`によるデータ取得
1. `pytrends`のインストール
`pytrends`は標準ライブラリとして含まれていないため、使用する前に明示的にインストールする必要があります。
```python
# pytrendsのインストール
!pip install pytrends
```
2. ライブラリのインポート
```python
import pandas as pd
from pytrends.request import TrendReq
import time
```

3. 検索ワードの設定
検索する際には、「北海道」以外は「都」「府」「県」を付けないという仮定の下、都道府県リストを用意しています。
```python
# 都道府県リスト
prefectures = [
    "北海道", "青森", "岩手", "宮城", "秋田", "山形", "福島", "茨城", "栃木", "群馬", # 1-10
    "埼玉", "千葉", "東京", "神奈川", "新潟", "富山", "石川", "福井", "山梨", "長野", # 11-20
    "岐阜", "静岡", "愛知", "三重", "滋賀", "京都", "大阪", "兵庫", "奈良", "和歌山", # 21-30
    "鳥取", "島根", "岡山", "広島", "山口", "徳島", "香川", "愛媛", "高知", "福岡", # 31-40
    "佐賀", "長崎", "熊本", "大分", "宮崎", "鹿児島", "沖縄" # 41-47
]

# 都道府県名とともに用いる検索ワード
search_word = '旅行'
```

4. `pytrends`のセットアップ
ホスト言語（表示言語）として**日本語**、タイムゾーンとして**日本標準時（JST）**を設定します。
```python
# pytrendsのセットアップ
## hl: Host language
## tz: Time zone (UTC+9) -> 540 mins = 9 hours
pytrends = TrendReq(hl='ja-JP', tz=540)
```

5. 検索ワードの2次元配列の準備
キーワードの人気度は相対値です。複数回にわたる検索でもキーワードの人気度を比較可能にするため、「**北海道 旅行**」というキーワードはそれぞれのリスト（検索）に基準として含めます。
```python
# 最大5つの検索ワードの2次元配列を準備
## Google Trendsでは最大5つの検索ワードしか比較できないため
prefs_list = []
prefs = [f"{prefectures[0]} {search_word}"]

for pref in prefectures[1:]:
    prefs.append(f"{pref} {search_word}")
    if len(prefs) == 5 or pref == prefectures[-1]:
        prefs_list.append(prefs)
        prefs = prefs[:1]

prefs_list
```
```python
# 出力結果
[['北海道 旅行', '青森 旅行', '岩手 旅行', '宮城 旅行', '秋田 旅行'],
 ['北海道 旅行', '山形 旅行', '福島 旅行', '茨城 旅行', '栃木 旅行'],
 ['北海道 旅行', '群馬 旅行', '埼玉 旅行', '千葉 旅行', '東京 旅行'],
 ['北海道 旅行', '神奈川 旅行', '新潟 旅行', '富山 旅行', '石川 旅行'],
 ['北海道 旅行', '福井 旅行', '山梨 旅行', '長野 旅行', '岐阜 旅行'],
 ['北海道 旅行', '静岡 旅行', '愛知 旅行', '三重 旅行', '滋賀 旅行'],
 ['北海道 旅行', '京都 旅行', '大阪 旅行', '兵庫 旅行', '奈良 旅行'],
 ['北海道 旅行', '和歌山 旅行', '鳥取 旅行', '島根 旅行', '岡山 旅行'],
 ['北海道 旅行', '広島 旅行', '山口 旅行', '徳島 旅行', '香川 旅行'],
 ['北海道 旅行', '愛媛 旅行', '高知 旅行', '福岡 旅行', '佐賀 旅行'],
 ['北海道 旅行', '長崎 旅行', '熊本 旅行', '大分 旅行', '宮崎 旅行'],
 ['北海道 旅行', '鹿児島 旅行', '沖縄 旅行']]
```

6. キーワードの人気度の収集と正規化
`prefs_list`から1つずつ要素（1回分の検索）を取り出して、以下の設定のAPI経由で検索を実行します。人気度は1回の検索（最大5つのキーワード）で0～100に正規化されるため、「**北海道 旅行**」の最も古い時点の人気度で正規化し、複数の検索にわたって比較可能にしています。なお、Google Trendsでは、データ取得期間の長さに応じて、データの粒度（間隔）が自動的に決定されます。
    - 検索カテゴリ (`category`)： `67` (旅行)
    - データ取得期間 (`timeframe`)： 2024/1/1～2024/12/31
    - 検索対象地域： `JP` (日本)
```python
# 検索結果のデータを保存するリストを初期化
trends_data = []

# 検索結果を収集
for i in range(len(prefs_list)):
    pytrends.build_payload(prefs_list[i], cat=67, timeframe="2024-01-01 2024-12-31", geo="JP")
    data = pytrends.interest_over_time()
    data = data.iloc[:, :-1] # 不要な最後のカラム（is_partial）を削除
    data = data / data.iloc[0,0] # 基準となるセル (0,0) でスコアを正規化
    if i == 0:
      trends_data.append(data)
    else:
      trends_data.append(data.iloc[:, 1:])
    # Google Trendsへのアクセス頻度を抑える
    time.sleep(2)

# 検索結果のリストをPandasデータフレームに変換
trends_df = pd.concat(trends_data, axis=1)
trends_df.columns = prefectures

trends_df
```
![](/images/20251214-google-trends-by-prefecture/pic2.png)
*trends_dfの出力結果*

### コロプレスマップによる可視化
Google Trendsのデータの取得は、これまでのプログラムで完了しています。ここでは活用方法の1つとしてコロプレスマップでの可視化を試しています。
:::message
**コロプレスマップ**とは、色のグラデーションを使用して行政区画単位で集計されたデータを表す統計地図です。
:::

1. 都道府県ごとに人気度の平均値を算出・正規化
コロプレスマップに表示するデータとして、都道府県ごとの正規化された人気度の平均値を用意します。
```python
# trends_dfの各列（都道府県）の平均を算出し、データフレームに変換
trends_mean = trends_df.mean().to_frame()

# 平均値（Trend）をMin-Max正規化し、0から1の範囲にスケーリング
trends_mean.columns = ["Trend"]
trends_mean["Trend"] = (trends_mean["Trend"] - trends_mean["Trend"].min()) / (trends_mean["Trend"].max() - trends_mean["Trend"].min())

trends_mean
```

2. GeoJSON表記に合わせた都道府県名の上書き
検索データを取得する段階では、「都」「府」「県」を除いた都道府県名（例：「東京都」ではなく「東京」）をキーワードとして使用していました。しかし、コロプレスマップの表示のために使うGeoJSONファイルの都道府県名と表記を合わせる必要があるため、正式名称（「都」「道」「府」「県」を含む）で上書きします。
```python
# 都道府県リスト（GeoJSONの表記に合わせて修正）
new_prefectures = [
    "北海道", "青森県", "岩手県", "宮城県", "秋田県", "山形県", "福島県", "茨城県", "栃木県", "群馬県", # 1-10
    "埼玉県", "千葉県", "東京都", "神奈川県", "新潟県", "富山県", "石川県", "福井県", "山梨県", "長野県", # 11-20
    "岐阜県", "静岡県", "愛知県", "三重県", "滋賀県", "京都府", "大阪府", "兵庫県", "奈良県", "和歌山県", # 21-30
    "鳥取県", "島根県", "岡山県", "広島県", "山口県", "徳島県", "香川県", "愛媛県", "高知県", "福岡県", # 31-40
    "佐賀県", "長崎県", "熊本県", "大分県", "宮崎県", "鹿児島県", "沖縄県" # 41-47
]

# trends_meanの都道府県名（インデックス）を上書き
trends_mean.index = new_prefectures
```
:::message
**GeoJSON**とは、地理空間データをJSON形式で取り扱うための形式です。地図を表示するために使用します。
:::

3. `folium`のインストール
Pythonでインタラクティブな地図を作成・操作するためのライブラリである`folium`をインストールします。
```python
# foliumのインストール
!pip install folium
```

4. ライブラリのインポート
```python
import folium
import requests
```

5. 都道府県のGeoJSONデータの取得
```python
# 都道府県のGeoJSONデータをインターネットから取得
geojson_url = "https://raw.githubusercontent.com/dataofjapan/land/master/japan.geojson"
response = requests.get(geojson_url)
jp_geojson = response.json()
```

6. コロプレスマップの表示
コロプレスマップを表示した結果、「旅行」と一緒に使われる都道府県として「東京」「北海道」「京都」「大阪」「福岡」などが多いことが分かります。
```python
# trends_meanのインデックス（都道府県名）をPrefectureカラムに変換
trends_map_data = trends_mean.reset_index()
trends_map_data.columns = ['Prefecture', 'Trend']

# マップの初期化（日本の中心付近）
m = folium.Map(location=[36.2048, 138.2529], zoom_start=5, tiles='CartoDB Positron')

# コロプレスマップのレイヤーを追加
folium.Choropleth(
    geo_data=jp_geojson,
    data=trends_map_data,
    columns=['Prefecture', 'Trend'], # [都道府県名, 正規化されたスコア]
    key_on='feature.properties.nam_ja', # 結合キーとして使用されるgeo_dataのプロパティ
    fill_color='YlGnBu', # 色のグラデーション
    fill_opacity=0.7, # 塗りつぶしの透明度
    line_opacity=0.2, # 都道府県の境界線の透明度
    legend_name='検索トレンド指数 (0-1)',
).add_to(m)

# マップを表示
m
```
![](/images/20251214-google-trends-by-prefecture/pic3.png)

## 3. おわりに
この記事では、Google TrendsのデータをAPI経由で取得する方法を紹介しました。1回の検索で入力できるキーワード数は最大5つまでである、人気度は検索ごとの相対値として取得される、という制約があるため、少し工夫が必要でした。

今後も気が向いたらデータ分析に関することも発信していきたいです。

## 4. 参考
https://github.com/ktakta0319/data-analysis
https://trends.google.com/
https://pypi.org/project/pytrends/
