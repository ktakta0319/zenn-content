---
title: "データビジュアリゼーション手法 60種類"
emoji: "📈"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["可視化"]
published: true
---
## 1. はじめに
データ分析においては、分析フェーズに焦点を当てられることが多いですが、その結果を適切にビジュアリゼーション（可視化）することも重要です。実際に使うかどうかは別として、ビジュアリゼーションの手法を網羅的に把握しておきたいと思って調べたのですが、日本語でいい感じにまとまったサイトは見つけられませんでした。

そこで、この記事では **[The Data Visualisation Catalogue](https://datavizcatalogue.com)** でリストアップされている60種類のビジュアリゼーション手法を整理します。

## 2. データビジュアリゼーションの種類
### 01. Arc Diagram（アーク・ダイアグラム）
ノードを1本の直線上に配置し、それらのノード間のつながりを弧（アーク）で表現します。データ内の共起関係（同時に現れる関係）を見つけるのに役立ちます。
- 全体像
![](/images/20251219-data-viz-catalogue/arc_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/arc_diagram_anatomy.png)

### 02. Area Graph（面グラフ）
折れ線グラフの一種で、線の下の部分を特定の色や模様で塗りつぶしたものです。折れ線グラフと同様に時系列的な数量の変化を表しますが、正確な数値を伝えるよりも、全体的な傾向を示す目的で用いられることが多いです。
- 全体像
![](/images/20251219-data-viz-catalogue/area_graph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/area_graph_anatomy.png)

### 03. Bar Chart（棒グラフ）
各カテゴリの数量を棒（バー）の長さや高さで表したグラフです。カテゴリごとの数量の違いを比較するのに役立ちます。
- 別名
    - Bar Graph
    - Column Graph
- 全体像
![](/images/20251219-data-viz-catalogue/bar_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/bar_chart_anatomy.png)
:::message
棒グラフはヒストグラムとは異なります。**棒グラフ**がカテゴリごとの値を比較するのに対して、**ヒストグラム**は連続的な数値データの分布の形を表現します。
:::

### 04. Box & Whisker Plot（箱ひげ図）
四分位数を用いてデータの分布を表現します。外れ値をひげ（whiskers）の延長線上にプロットすることもあります。データの分布を表現するスペースが小さいため、多数のグループやデータセット間で分布を比較するのに有用です。
- 別名： Box Plot
- 全体像
![](/images/20251219-data-viz-catalogue/box_plot.png)
- 詳細
![](/images/20251219-data-viz-catalogue/box_plot_anatomy.png)

### 05. Brainstorm（ブレインストーム）
中心テーマ（中央ノード）からサブカテゴリを分岐させ、関連するアイディア、単語、イメージ、概念を図としてまとめるための手法です。アイディアの発想、関連性の発見、情報の整理、学習の補助など様々な用途で使われます。
- 別名： Mind-map
- 全体像
![](/images/20251219-data-viz-catalogue/brainstorm.png)
- 詳細
![](/images/20251219-data-viz-catalogue/brainstorm_anatomy.png)

### 06. Bubble Chart（バブル・チャート）
散布図と比例面積チャートの要素を組み合わせた多変量グラフです。X軸、Y軸に加えて、円の面積が第3の変数を表現します。
- 全体像
![](/images/20251219-data-viz-catalogue/bubble_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/bubble_chart_anatomy.png)

### 07. Bubble Map（バブル・マップ）
地理的エリアに表示した円の面積がそのエリアのデータ量を表現します。コロプレス・マップでは「面積の大きい領域ほどデータ量が多く見える」という課題がありますが、バブルマップは円の面積を使うため誤認識を防げます。
- 全体像
![](/images/20251219-data-viz-catalogue/bubble_map.png)
- 詳細
![](/images/20251219-data-viz-catalogue/bubble_map_anatomy.png)

### 08. Bullet Graph（ブレット・グラフ）
棒グラフのように機能しますが、中心の棒（主要測定値：Feature Measure）と棒に垂直に入った線（比較測定値：Comparative Measure）の導入によって、比較測定値（目標値）に対する主要測定値（実績値）を表現します。そのため、業績評価や目標達成度の管理に使われます。主要測定値の背景のカラーバーは、その色によって定性的な評価範囲（例：悪い・普通・良い）を示します。
- 全体像
![](/images/20251219-data-viz-catalogue/bullet_graph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/bullet_graph_anatomy.png)

### 09. Calendar（カレンダー）
カレンダーは時間の経過やイベントの日付を表示するために利用されます。現在最も一般的なカレンダーはグレゴリオ暦で、1ヶ月ごとに7列（曜日）、5～6行（週）のグリッドで表現されます。
- 全体像
![](/images/20251219-data-viz-catalogue/calendar.png)
- 詳細
![](/images/20251219-data-viz-catalogue/calendar_anatomy.png)

### 10. Candlestick Chart（ローソク足チャート）
始値・終値・高値・安値などの価格情報をローソクのようなシンボルで表現し、証券、デリバティブ、株式などの価格変動を可視化します。ローソクは、市場が強気（Bullish、始値 < 終値）の場合は白または緑色、弱気（Bearish、始値 > 終値）の場合は黒または赤色で表示されます。
- 別名： Japanese Candlestick Chart
- 全体像
![](/images/20251219-data-viz-catalogue/candlestick_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/candlestick_chart_anatomy.png)

### 11. Chord Diagram（コード・ダイアグラム）
円周上に配置されたノード（エンティティ）のつながりを弧（アーク）やベジェ曲線を使って表現し、エンティティ間の相互関係を可視化します。国同士の貿易量、部署間のメール送信数など、エンティティごとのつながりの強さを定量的に示すのに適しています。
- 全体像
![](/images/20251219-data-viz-catalogue/chord_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/chord_diagram_anatomy.png)

### 12. Choropleth Map（コロプレス・マップ）
区分された地理的エリアごとの集計データを色分け、濃淡、パターンで表現する地図です。地図全体にわたって、エリアごとの変数の違いや分布パターンを示すことができます。
- 全体像
![](/images/20251219-data-viz-catalogue/choropleth.png)
- 詳細
![](/images/20251219-data-viz-catalogue/choropleth_anatomy.png)
:::message
コロプレスマップは、通常、人口などの生データをそのまま使うのではなく、$1 km^2$あたりの人口のように面積で正規化した値を用いた密度マップとして表現します。面積が大きいエリアほど人口が多くなる傾向にあるため、正規化しないと面積の影響を正しく考慮した比較ができません。
:::

### 13. Circle Packing（サークル・パッキング）
長方形の代わりに円を用いるツリーマップ（Treemap）の一種です。円同士の包含関係によって階層関係が表現されます。
- 別名： Circular Treemap
- 全体像
![](/images/20251219-data-viz-catalogue/circle_packing.png)
- 詳細
![](/images/20251219-data-viz-catalogue/circle_packing_anatomy.png)

### 14. Connection Map（コネクション・マップ）
地図上に配置された地点同士を直線または曲線で結ぶことで描かれます。地理的なつながりや関係性、ある地点から別の地点へのルート、コネクションの分布などを表現するのに役立ちます。
- 別名
    - Link Map
    - Ray Map
- 全体像
![](/images/20251219-data-viz-catalogue/connection_map.png)
- 詳細
![](/images/20251219-data-viz-catalogue/connection_map_anatomy.png)

### 15. Density Plot（密度プロット）
連続した区間や時間軸に沿ったデータの分布を可視化するグラフです。ヒストグラムの発展形で、カーネル平滑化によって滑らかに描画されます。ヒストグラムとは異なり、ビンの数に左右されずに分布を表現できるという利点があります。
- 別名
    - Kernel Density Plot
    - Density Trace Graph
- 全体像
![](/images/20251219-data-viz-catalogue/density_plot.png)
- 詳細
![](/images/20251219-data-viz-catalogue/density_plot_anatomy.png)

### 16. Donut Chart（ドーナツ・チャート）
円グラフの中央部分をくり抜いたグラフです。中央の空白部分を利用して、数値やラベルなどの追加情報を表示できます。
- 全体像
![](/images/20251219-data-viz-catalogue/donut_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/donut_chart_anatomy.png)

### 17. Dot Map（ドット・マップ）
地図上に等しい大きさの点を配置することで、空間的なパターンやデータの分布を可視化します。1つの点が1つのカウントや対象物を表す「1対1型」と1つの点が特定の単位（例：1つの点 = 10本の木）を表す「1対多型」の2種類があります。
- 別名
    - Point Map
    - Dot Distribution Map
    - Dot Density Map
- 全体像
![](/images/20251219-data-viz-catalogue/dot_map.png)
- 詳細
![](/images/20251219-data-viz-catalogue/dot_map_anatomy.png)

### 18. Dot Matrix Chart（ドット・マトリックス・チャート）
カテゴリごとに色分けされたドットを用いて離散データを表示するグラフです。データセット内のカテゴリの分布や割合、他のデータセットと比較したパターンの違いを把握するために使われます。
- 全体像
![](/images/20251219-data-viz-catalogue/dotmatrix.png)
- 詳細
![](/images/20251219-data-viz-catalogue/dotmatrix_anatomy.png)

### 19. Error Bars（エラー・バー）
エラーバー自体は単独のチャートではありません。しかし、散布図、ドットプロット、棒グラフ、折れ線グラフなどに適用して、推定誤差や不確実性を示すことで、測定値の精度を把握するのに役立ちます。一般的には、標準偏差、標準誤差、信頼区間または最小値・最大値（範囲）を表示します。
- 全体像
![](/images/20251219-data-viz-catalogue/error_bars.png)
- 詳細
![](/images/20251219-data-viz-catalogue/error_bars_anatomy.png)

### 20. Flow Chart（フロー・チャート）
プロセスの連続した手順を図式化したチャートです。複雑または抽象的な手順、システム、概念、アルゴリズムがどのように機能するかを示すのに役立ちます。記号（シンボル）は種類ごとに固有の形として標準化され、各手順の説明（ラベル）は対応する記号の中に記入されます。
- 別名
    - Flow Diagram
    - Flow Process Chart
    - Process Chart
    - Process Map
    - Process Model
    - Work Flow Diagram
- 全体像
![](/images/20251219-data-viz-catalogue/flow_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/flow_chart_anatomy.png)

### 21. Flow Map（フロー・マップ）
情報や物体がある地点から別の地点に移動する数量を線の太さで示した地図です。一般的には、人、動物、製品などの移動を表現するために使用されます。
- 全体像
![](/images/20251219-data-viz-catalogue/flow_map.png)
- 詳細
![](/images/20251219-data-viz-catalogue/flow_map_anatomy.png)

### 22. Gantt Chart（ガント・チャート）
タスクまたは作業の一覧とそれぞれの所要時間を時間の流れに沿って表示するプロジェクト管理ツールです。矢印によってタスクや作業の依存関係が示され、プロジェクト完了に不可欠なクリティカルパスも可視化されます。
- 全体像
![](/images/20251219-data-viz-catalogue/gantt_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/gantt_chart_anatomy.png)

### 23. Heatmap（ヒートマップ）
色の変化を用いてデータを可視化する手法です。一般的にはテーブル形式で表現され、行と列に異なるカテゴリを配置し、交差するセルを数値の大小やカテゴリに応じた色で塗り分けます。カテゴリ変数間のパターンや相関の有無を視覚的に発見するのに役立ちます。
- 全体像
![](/images/20251219-data-viz-catalogue/heatmap.png)
- 詳細
![](/images/20251219-data-viz-catalogue/heatmap_anatomy.png)

### 24. Histogram（ヒストグラム）
連続的なデータの分布を可視化するグラフです。各棒はその区間（ビン）における度数（出現回数）を表します。データのばらつき具合、極端な値や欠けている区間の有無、確率分布の形状などを把握するのに役立ちます。
- 全体像
![](/images/20251219-data-viz-catalogue/histogram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/histogram_anatomy.png)

### 25. Illustration Diagram（イラストレーション・ダイアグラム）
画像に注釈、ラベル、凡例などを添えて表示し、概念や方法、物体や場所の描写、物事の仕組みや変化などを理解するのに役立ちます。画像にはイラスト、ラフスケッチ、ワイヤーフレーム、写真など様々なものが使用されます。
- 全体像
![](/images/20251219-data-viz-catalogue/illustration_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/illustration_diagram_anatomy.png)

### 26. Kagi Chart（カギ足チャート）
一連の線のパターンによって価格の動きを可視化し、特定の資産における需要と供給の全体的な傾向を把握するために使用されます。X軸は日付や時刻、Y軸は価格を表しますが、ローソク足チャートとは異なり、時間ごとに必ずデータが描画されるわけではありません。事前に設定された反転幅（例：10円）を超える価格変動があった場合のみ線を反転させて記録し、線の太さや色の変化によって強気・弱気の傾向を視覚的に示します。
- 全体像
![](/images/20251219-data-viz-catalogue/kagi_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/kagi_chart_anatomy.png)

### 27. Line Graph（折れ線グラフ）
時間の経過に伴うデータの変動を表現するグラフです。通常、X軸には時間軸や連続した区間、Y軸には量的データが設定されます。
- 全体像
![](/images/20251219-data-viz-catalogue/line_graph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/line_graph_anatomy.png)

### 28. Marimekko Chart（マリメッコ・チャート）
2つの変数にわたるカテゴリデータを可視化するチャートです。X軸・Y軸の両方が変数であり、各セグメント（区分）の幅と高さはそれぞれの変数の割合によって決まります。そのため、2方向の100%積み上げ棒グラフのように機能します。
- 別名： Mosaic Plot
- 全体像
![](/images/20251219-data-viz-catalogue/marimekko_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/marimekko_chart_anatomy.png)

### 29. Multi-set Bar Chart（マルチセット棒グラフ）
複数のデータ系列を同じ軸上に表示し、親カテゴリごとにグループ化して比較したい場合に使用される棒グラフの一種です。また、親カテゴリを特定の時間（例：月・年）に設定して、時間経過に伴うデータの変化を示すこともできます。
- 別名
    - Grouped Bar Chart
    - Clustered Bar Chart
- 全体像
![](/images/20251219-data-viz-catalogue/multiset_barchart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/multiset_barchart_anatomy.png)

### 30. Network Diagram（ネットワーク図）
ノード（点）とリンク（線）を使って、エンティティの相互のつながりを可視化します。ノードの大きさやリンクの太さを特定の値に比例させることで追加の変数を表現することもできます。ノードのクラスタリング、つながりの密度、全体のレイアウトを観察して、ネットワーク構造を理解します。
- 別名
    - Network Graph
    - Network Map
    - Node-Link Diagram
- 全体像
![](/images/20251219-data-viz-catalogue/network_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/network_diagram_anatomy.png)

### 31. Nightingale Rose Chart（ローズ・ダイアグラム）
データの各カテゴリや区間を円形チャート上で等しい角度のセグメントに分け、そのセグメントの値を半径として表します。ナイチンゲールがクリミア戦争中の兵士の回避可能な死亡数を伝えるために使用しました。極座標の中心から外側に行くほどリングの面積が大きくなるため、値の増加を過大に表現してしまうことが欠点です。
- 別名
    - Coxcomb Chart
    - Polar Area Diagram
- 全体像
![](/images/20251219-data-viz-catalogue/nightingale_rose_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/nightingale_rose_chart_anatomy.png)

### 32. Non-ribbon Chord Diagram（非リボン型コード・ダイアグラム）
ノード（点）とリンク（線）のみを表示した、コード・ダイアグラムの簡略版です。データ内の接続関係により重点を置いて可視化します。
- 全体像
![](/images/20251219-data-viz-catalogue/non_ribbon_chord_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/non_ribbon_chord_diagram_anatomy.png)

### 33. Open-High-Low-Close Chart（四本値チャート）
一定期間ごとの始値、終値、高値、安値を用いて、証券、デリバティブ、株式などの価格変動を可視化します。X軸は時間、Y軸は価格を表し、各期間について、縦線で高値と安値の範囲を、左右の小さな線で始値と終値を表現します。色分けによって、市場が強気（Bullish、始値 < 終値）か弱気（Bearish、始値 > 終値）かを示します。
- 別名
    - OHLC Chart
    - Price Chart
    - Bar Chart
- 全体像
![](/images/20251219-data-viz-catalogue/OHLC_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/OHLC_chart_anatomy.png)

### 34. Parallel Coordinates Plot（並行座標プロット）
多変量の数値データをプロットし、それらの関係性を把握するために使われます。各変数に軸が割り当てられ、全ての軸は互いに平行に配置されます。隣接する軸の変数間の関係は、非隣接の変数間の関係よりも認識しやすいため、軸の順序がデータの理解のされ方に影響を与えます。
- 全体像
![](/images/20251219-data-viz-catalogue/parallel_coordinates.png)
- 詳細
![](/images/20251219-data-viz-catalogue/parallel_coordinates_anatomy.png)

### 35. Parallel Sets（パラレル・セット）
フローや割合を示す点でサンキー図（Sankey Diagram）に似ていますが、矢印は使われず、ラインセットごとにフローパスが分割されます。変数ごとにラインセットが配置され、カテゴリごとの値がラインの分割で表現されます。
- 全体像
![](/images/20251219-data-viz-catalogue/parallel_sets.png)
- 詳細
![](/images/20251219-data-viz-catalogue/parallel_sets_anatomy.png)

### 36. Pictogram Chart（ピクトグラム・チャート）
アイコンを使って、小規模な離散データの全体像を分かりやすく表示するチャートです。各アイコンは1単位または任意の単位（例：1アイコン = 10人）を表すことができます。
- 別名
    - Pictograph Chart
    - Pictorial Chart
    - Pictorial Unit Chart
    - Picture Graph
- 全体像
![](/images/20251219-data-viz-catalogue/pictograph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/pictogram_anatomy.png)

### 37. Pie Chart（円グラフ）
円を比率に応じた扇形に分割することで、カテゴリ間の割合やパーセンテージを示します。プレゼンテーションなどで広く使われる一方、表示できるカテゴリ数が少ない、他の手法よりも表示スペースを必要とする、複数の円グラフ間の比較が難しい、などの欠点があります。
- 全体像
![](/images/20251219-data-viz-catalogue/pie_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/pie_chart_anatomy.png)

### 38. Point & Figure Chart（ポイント＆フィギュア・チャート）
特定の資産における需要と供給の関係を、X（価格上昇）とO（価格下落）で構成された列によって表現するチャートです。時間の経過には依存せず、事前に定義したボックスサイズ（例：1ドル）以上に価格が変動した場合のみXまたはOを描きます。トレンドが反転したと判断する基準の価格変動幅（例：3ドル）をリバーサル量と呼び、これ以上の価格変動があればXとOとを切り替えて新しい列に移ります。また、列内に表示される1〜9およびA〜Cは月の区切りを示しており、1〜9は1月から9月、A・B・Cはそれぞれ10月・11月・12月を表します。
- 別名： P&F Chart
- 全体像
![](/images/20251219-data-viz-catalogue/point_and_figure_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/point_and_figure_chart_anatomy.png)

### 39. Population Pyramid（人口ピラミッド）
男女それぞれについて背中合わせに配置された2つのヒストグラムで構成され、全ての年齢階級の人口分布を示します。人口構成の変化や違いを把握するのに適しています。複数の人口ピラミッドを用いることで、国ごとや特定の人口集団間のパターンを比較できます。
- 別名： Age & Sex Pyramid
- 全体像
![](/images/20251219-data-viz-catalogue/population_pyramid.png)
- 詳細
![](/images/20251219-data-viz-catalogue/population_pyramid_anatomy.png)

### 40. Proportional Area Chart（比例面積チャート）
値の大きさや数量などの割合を面積で表現し、データ内の相対的な大きさを素早く把握するのに適したチャートです。通常は正方形や円が使われますが、面積でデータを表現する限り、どのような形状でも使用できます。
- 全体像
![](/images/20251219-data-viz-catalogue/proportional_area_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/proportional_area_chart_anatomy.png)

### 41. Radar Chart（レーダー・チャート）
複数の定量的変数を比較するチャートで、各変数は中心から放射状に伸びる軸にプロットされ、値を線で結ぶことで多角形を形成します。これにより、変数間の相対的な値やパフォーマンスの傾向、外れ値を視覚的に把握できます。
- 別名
    - Spider Chart
    - Web Chart
    - Polar Chart
    - Star Plots
- 全体像
![](/images/20251219-data-viz-catalogue/radar_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/radar_chart_anatomy.png)

### 42. Radial Bar Chart（放射状バー・チャート）
通常の棒グラフを極座標系にプロットしたチャートです。同じ値を表していても外側に配置された棒は長くなるため、カテゴリ間の値を比較する際に誤解を招きやすいという問題があります。
- 全体像
![](/images/20251219-data-viz-catalogue/radial_bar_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/radial_bar_chart_anatomy.png)

### 43. Radial Column Chart（放射状カラム・チャート）
極座標の中心から放射状に伸びた棒の長さでカテゴリごとの値を表します。ゼロを中心の外側に設定することで、負の値も表現可能です。
- 別名
    - Circular Column Graph
    - Star Graph
- 全体像
![](/images/20251219-data-viz-catalogue/radial_column_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/radial_column_chart_anatomy.png)

### 44. Sankey Diagram（サンキー・ダイアグラム）
矢印や線を使って、フローとその量を示す図です。エネルギー、資金、資材の移動やシステムやプロセスにおける流れを視覚的に表現します。フローを示す矢印や線は、プロセスの各段階で合流・分岐することができます。
- 全体像
![](/images/20251219-data-viz-catalogue/sankey_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/sankey_diagram_anatomy.png)

### 45. Scatterplot（散布図）
2つの変数の値を直交座標に点としてプロットし、それらの間に関係性や相関が存在するか確認できます。全体的な傾向を一目で示したり、観測されていない点を補間するために、グラフ上に回帰線を重ねることがあります。
- 全体像
![](/images/20251219-data-viz-catalogue/scatterplot.png)
- 詳細
![](/images/20251219-data-viz-catalogue/scatterplot_anatomy.png)

### 46. Span Chart（スパン・チャート）
データの最小値と最大値との範囲を表示するチャートです。主にカテゴリ間で範囲を比較するのに役立ちます。
- 別名
    - Range Bar/Column Graph
    - Floating Bar Graph
    - Difference Graph
    - High-Low Graph
- 全体像
![](/images/20251219-data-viz-catalogue/span_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/span_chart_anatomy.png)

### 47. Spiral Plot（スパイラル・プロット）
時系列データをアルキメデスの螺旋上に配置して表示します。グラフは螺旋の中心から始まり、外側へ向かって進行します。スパイラル・プロットは柔軟性が高く、螺旋の経路に沿って棒、線、点などをプロットできます。
- 別名： Time Series Spiral
- 全体像
![](/images/20251219-data-viz-catalogue/spiral_plot.png)
- 詳細
![](/images/20251219-data-viz-catalogue/spiral_plot_anatomy.png)

### 48. Stacked Area Graph（積み上げ面積グラフ）
基本的な面積グラフと同じ仕組みですが、複数のデータ系列を重ねて表示する点が異なります。グラフ全体は、プロットされた全てのデータの合計を表します。時間の経過に伴って変化する複数の変数を比較するのに適しています。
- 全体像
![](/images/20251219-data-viz-catalogue/stacked_area_graph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/stacked_area_graph_anatomy.png)

### 49. Stacked Bar Graph（積み上げ棒グラフ）
複数のデータ系列を積み上げて表示する棒グラフです。各セグメントの実数値を用いる通常の積み上げ棒グラフのほか、各セグメントの割合を用いて常に棒の高さを100%とする「100%積み上げ棒グラフ」があります。
- 全体像
![](/images/20251219-data-viz-catalogue/stacked_bar_graph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/stacked_bar_graph_anatomy.png)

### 50. Stem and Leaf Plot（幹葉図）
数値の位取り（桁）に基づいてデータを整理し、分布を示す手法です。「幹」の列には位の値が昇順に並べられ、それぞれの位に属するデータは「葉」として横方向に並べて表示されます。
- 別名
    - Stemplot
    - Stem & Leaf Display
- 全体像
![](/images/20251219-data-viz-catalogue/stem_and_leaf_plot.png)
- 詳細
![](/images/20251219-data-viz-catalogue/stem_and_leaf_plot_anatomy.png)

### 51. Stream Graph（ストリーム・グラフ）
複数カテゴリの時間的変化を、中央の基準線を中心に値を上下にずらして配置する面積グラフの一種です。大規模データのトレンドや周期的パターンを把握するのに適していますが、値の正確な比較や小さいカテゴリの把握には向きません。
- 別名： Theme River
- 全体像
![](/images/20251219-data-viz-catalogue/stream_graph.png)
- 詳細
![](/images/20251219-data-viz-catalogue/stream_graph_anatomy.png)

### 52. Sunburst Diagram（サンバースト・ダイアグラム）
複数のリングを用いて階層構造を表現します。中央の円がルートノードを表し、リングが外側へ向かうほど階層が深くなります。
- 別名
    - Sunburst Chart
    - Ring Chart
    - Multi-level Pie Chart
    - Belt Chart
    - Radial Treemap
- 全体像
![](/images/20251219-data-viz-catalogue/sunburst_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/sunburst_diagram_anatomy.png)

### 53. Tally Chart（タリー・チャート）
タリーマーク（棒線）を用いてデータの出現頻度を記録し、視覚的に示すための手法です。全てのデータをカウントしたら次の列または行に総数を表示します。最終的な結果は、ヒストグラムと似た形になります。
- 全体像
![](/images/20251219-data-viz-catalogue/tally_chart.png)
- 詳細
![](/images/20251219-data-viz-catalogue/tally_chart_anatomy.png)

### 54. Timeline（タイムライン）
出来事のリストを時系列順に表示します。単純に出来事を順番に並べるだけのタイムライン（Sequential Timeline）もあれば、スケールに基づくタイムライン（Scaled Timeline）もあります。
- 全体像
![](/images/20251219-data-viz-catalogue/timeline.png)
- 詳細
![](/images/20251219-data-viz-catalogue/timeline_anatomy.png)

### 55. Timetable（タイムテーブル）
予定された出来事やタスク、行動を参照・管理するためのツールです。交通機関の出発・到着時刻を表示する際に一般的に用いられています。
- 全体像
![](/images/20251219-data-viz-catalogue/timetable.png)
- 詳細
![](/images/20251219-data-viz-catalogue/timetable_anatomy.png)

### 56. Tree Diagram（樹形図）
階層構造を木のような形で視覚的に表現する手法です。親ノードを持たないノードを「ルートノード（根ノード）」、子ノードを持たないノードを「リーフノード（葉ノード）」と呼びます。家系図や血縁関係、進化学における種の起源、コンピュータサイエンスや数学での構造など様々な表示に使われます。
- 別名
    - Organisational chart
    - Linkage Tree
- 全体像
![](/images/20251219-data-viz-catalogue/tree_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/tree_diagram_anatomy.png)

### 57. Treemap（ツリーマップ）
樹形図（Tree Diagram）の階層構造を可視化すると同時に、各カテゴリの量を面積の大きさで表現する手法です。階層構造をコンパクトかつ効率的に表示でき、階層の全体像を素早く把握するのに適しています。面積の大きさによってカテゴリ間の比率を比較することも可能です。
- 全体像
![](/images/20251219-data-viz-catalogue/treemap.png)
- 詳細
![](/images/20251219-data-viz-catalogue/treemap_anatomy.png)

### 58. Venn Diagram（ベン図）
複数の集合間の論理的な関係を視覚的に示す図です。各集合の内部には、共通の特性を持つ要素が含まれます。集合が重なる部分は、重なった集合全ての特性を持つ要素が含まれます。
- 別名： Set Diagram
- 全体像
![](/images/20251219-data-viz-catalogue/venn_diagram.png)
- 詳細
![](/images/20251219-data-viz-catalogue/venn_diagram_anatomy.png)

### 59. Violin Plot（バイオリン・プロット）
箱ひげ図（Box Plot）と密度プロット（Density Plot）を組み合わせ、データの分布と確率密度を可視化するためのグラフです。箱ひげ図はシンプルな見た目のため、データの詳細な分布情報が隠れてしまうことがあります。例えば、箱ひげ図だけでは分布が二峰性（2つの山がある）や多峰性（複数の山がある）かどうかは分かりません。
- 全体像
![](/images/20251219-data-viz-catalogue/violin_plot.png)
- 詳細
![](/images/20251219-data-viz-catalogue/violin_plot_anatomy.png)

### 60. Word Cloud（ワード・クラウド）
文章中の単語の出現頻度を文字サイズで表現します。主にキーワードやタグの傾向を把握したり、複数の文章を比較したりするのに適しています。しかし、長い単語や文字の形状による強調が起きやすく、正確な分析には向かないため、視覚的・美的な目的で使われることが多いです。
- 別名： Tag Cloud
- 全体像
![](/images/20251219-data-viz-catalogue/wordcloud.png)
- 詳細
![](/images/20251219-data-viz-catalogue/wordcloud_anatomy.png)

## 3. データビジュアリゼーションの分類方法
### 種類による分類
| No. | 種類 | グラフ/<br>プロット | 図/<br>図解 | 表 | 地図 | その他 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1  | Arc Diagram               |  | ✅ |  |  |  |
| 2  | Area Graph                | ✅ |  |  |  |  |
| 3  | Bar Chart                 | ✅ |  |  |  |  |
| 4  | Box & Whisker Plot        | ✅ |  |  |  |  |
| 5  | Brainstorm                |  | ✅ |  |  |  |
| 6  | Bubble Chart              | ✅ |  |  |  |  |
| 7  | Bubble Map                |  |  |  | ✅ |  |
| 8  | Bullet Graph              |  |  |  |  |  |
| 9  | Calendar                  |  |  | ✅ |  |  |
| 10 | Candlestick Chart         | ✅ |  |  |  |  |
| 11 | Chord Diagram             |  | ✅ |  |  |  |
| 12 | Choropleth Map            |  |  |  | ✅ |  |
| 13 | Circle Packing            |  |  |  |  | ✅ |
| 14 | Connection Map            |  |  |  | ✅ |  |
| 15 | Density Plot              | ✅ |  |  |  |  |
| 16 | Donut Chart               |  |  |  |  |  |
| 17 | Dot Map                   |  |  |  | ✅ |  |
| 18 | Dot Matrix Chart          |  |  |  |  | ✅ |
| 19 | Error Bars                | ✅ |  |  |  |  |
| 20 | Flow Chart                |  | ✅ |  |  |  |
| 21 | Flow Map                  |  |  |  | ✅ |  |
| 22 | Gantt Chart               |  |  | ✅ |  |  |
| 23 | Heatmap                   |  |  | ✅ |  |  |
| 24 | Histogram                 | ✅ |  |  |  |  |
| 25 | Illustration Diagram      |  | ✅ |  |  |  |
| 26 | Kagi Chart                | ✅ |  |  |  |  |
| 27 | Line Graph                | ✅ |  |  |  |  |
| 28 | Marimekko Chart           | ✅ |  |  |  |  |
| 29 | Multi-set Bar Chart       | ✅ |  |  |  |  |
| 30 | Network Diagram           |  | ✅ |  |  |  |
| 31 | Nightingale Rose Chart    |  |  |  |  | ✅ |
| 32 | Non-ribbon Chord Diagram  |  | ✅ |  |  |  |
| 33 | Open-High-Low-Close Chart | ✅ |  |  |  |  |
| 34 | Parallel Coordinates Plot | ✅ |  |  |  |  |
| 35 | Parallel Sets             |  |  |  |  | ✅ |
| 36 | Pictogram Chart           |  |  |  |  | ✅ |
| 37 | Pie Chart                 |  |  |  |  | ✅ |
| 38 | Point & Figure Chart      | ✅ |  |  |  |  |
| 39 | Population Pyramid        | ✅ |  |  |  |  |
| 40 | Proportional Area Chart   |  |  |  |  | ✅ |
| 41 | Radar Chart               | ✅ |  |  |  |  |
| 42 | Radial Bar Chart          | ✅ |  |  |  |  |
| 43 | Radial Column Chart       | ✅ |  |  |  |  |
| 44 | Sankey Diagram            |  | ✅ |  |  |  |
| 45 | Scatterplot               | ✅ |  |  |  |  |
| 46 | Span Chart                | ✅ |  |  |  |  |
| 47 | Spiral Plot               | ✅ |  |  |  |  |
| 48 | Stacked Area Graph        | ✅ |  |  |  |  |
| 49 | Stacked Bar Graph         | ✅ |  |  |  |  |
| 50 | Stem and Leaf Plot        |  |  | ✅ |  |  |
| 51 | Stream Graph              | ✅ |  |  |  |  |
| 52 | Sunburst Diagram          |  |  |  |  | ✅ |
| 53 | Tally Chart               |  |  | ✅ |  |  |
| 54 | Timeline                  |  | ✅ |  |  |  |
| 55 | Timetable                 |  |  | ✅ |  |  |
| 56 | Tree Diagram              |  | ✅ |  |  |  |
| 57 | Treemap                   |  |  |  |  | ✅ |
| 58 | Venn Diagram              |  | ✅ |  |  |  |
| 59 | Violin Plot               | ✅ |  |  |  |  |
| 60 | Word Cloud                |  |  |  |  | ✅ |
### 可視化の対象による分類
| No. | 種類 | 比較 | 割合 | 関係性 | 階層 | 概念 | 地理的位置 | 全体に対する部分 | 分布 | 仕組み | プロセス／方法 | 移動／流れ | パターン | 範囲 | 時間変化 | テキスト分析 | 参照ツール |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1  | Arc Diagram               |  |  | ✅ |  |  |  |  |  |  |  |  | ✅ |  |  |  |  | 
| 2  | Area Graph                |  |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 3  | Bar Chart                 | ✅ |  |  |  |  |  |  |  |  |  |  | ✅ |  |  |  |  | 
| 4  | Box & Whisker Plot        | ✅ |  |  |  |  |  |  | ✅ |  |  |  | ✅ | ✅ |  |  |  | 
| 5  | Brainstorm                |  |  | ✅ |  | ✅ |  |  |  |  |  |  |  |  |  |  |  | 
| 6  | Bubble Chart              | ✅ | ✅ | ✅ |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 7  | Bubble Map                |  | ✅ |  |  |  | ✅ |  | ✅ |  |  |  |  |  |  |  |  | 
| 8  | Bullet Graph              | ✅ |  |  |  |  |  |  |  |  |  |  |  | ✅ |  |  |  | 
| 9  | Calendar                  |  |  |  |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ | 
| 10 | Candlestick Chart         |  |  |  |  |  |  |  |  |  |  |  | ✅ | ✅ | ✅ |  |  | 
| 11 | Chord Diagram             | ✅ |  | ✅ |  |  |  |  |  |  |  |  |  |  |  |  |  | 
| 12 | Choropleth Map            | ✅ |  |  |  |  | ✅ |  |  |  |  |  | ✅ |  |  |  |  | 
| 13 | Circle Packing            |  | ✅ |  | ✅ |  |  |  |  |  |  |  |  |  |  |  |  | 
| 14 | Connection Map            |  |  | ✅ |  |  | ✅ |  | ✅ |  |  | ✅ | ✅ |  |  |  |  | 
| 15 | Density Plot              |  |  |  |  |  |  |  | ✅ |  |  |  | ✅ |  |  |  |  | 
| 16 | Donut Chart               | ✅ | ✅ |  |  |  |  | ✅ |  |  |  |  |  |  |  |  |  | 
| 17 | Dot Map                   |  |  |  |  |  | ✅ |  | ✅ |  |  |  | ✅ |  |  |  |  | 
| 18 | Dot Matrix Chart          | ✅ | ✅ |  |  |  |  |  | ✅ |  |  |  | ✅ |  |  |  |  | 
| 19 | Error Bars                |  |  |  |  |  |  |  |  |  |  |  |  | ✅ |  |  |  | 
| 20 | Flow Chart                |  |  |  |  | ✅ |  |  |  | ✅ | ✅ | ✅ |  |  |  |  |  | 
| 21 | Flow Map                  |  |  |  |  |  | ✅ |  | ✅ |  |  |  |  |  |  |  |  | 
| 22 | Gantt Chart               |  |  |  |  |  |  |  |  |  | ✅ |  |  | ✅ | ✅ |  | ✅ | 
| 23 | Heatmap                   | ✅ |  | ✅ |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 24 | Histogram                 |  |  |  |  |  |  |  | ✅ |  |  |  | ✅ |  |  |  |  | 
| 25 | Illustration Diagram      |  |  |  |  | ✅ |  |  |  | ✅ | ✅ |  |  |  |  |  |  | 
| 26 | Kagi Chart                |  |  |  |  |  |  |  |  |  |  |  | ✅ | ✅ |  |  |  | 
| 27 | Line Graph                | ✅ |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 28 | Marimekko Chart           | ✅ | ✅ | ✅ |  |  |  | ✅ |  |  |  |  |  |  |  |  |  | 
| 29 | Multi-set Bar Chart       | ✅ |  |  |  |  |  |  | ✅ |  |  |  | ✅ |  |  |  |  | 
| 30 | Network Diagram           |  |  | ✅ |  |  |  |  |  |  |  |  |  |  |  |  |  | 
| 31 | Nightingale Rose Chart    | ✅ | ✅ |  |  |  |  |  |  |  |  |  |  |  | ✅ |  |  | 
| 32 | Non-ribbon Chord Diagram  |  |  | ✅ |  |  |  |  |  |  |  |  |  |  |  |  |  | 
| 33 | Open-High-Low-Close Chart |  |  |  |  |  |  |  |  |  |  |  | ✅ | ✅ | ✅ |  |  | 
| 34 | Parallel Coordinates Plot | ✅ |  | ✅ |  |  |  |  |  |  |  |  | ✅ |  |  |  |  | 
| 35 | Parallel Sets             | ✅ | ✅ |  |  |  |  |  | ✅ |  | ✅ | ✅ |  |  |  |  |  | 
| 36 | Pictogram Chart           | ✅ |  |  |  |  |  |  | ✅ |  |  |  |  |  |  |  |  | 
| 37 | Pie Chart                 | ✅ | ✅ |  |  |  |  | ✅ |  |  |  |  |  |  |  |  |  | 
| 38 | Point & Figure Chart      |  |  |  |  |  |  |  |  |  |  |  | ✅ |  |  |  |  | 
| 39 | Population Pyramid        | ✅ |  |  |  |  |  |  | ✅ |  |  |  | ✅ |  |  |  |  | 
| 40 | Proportional Area Chart   | ✅ | ✅ |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 
| 41 | Radar Chart               | ✅ |  | ✅ |  |  |  |  |  |  |  |  | ✅ |  |  |  |  | 
| 42 | Radial Bar Chart          | ✅ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 
| 43 | Radial Column Chart       | ✅ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 
| 44 | Sankey Diagram            |  | ✅ |  |  |  |  |  |  | ✅ | ✅ | ✅ |  |  |  |  |  | 
| 45 | Scatterplot               |  |  | ✅ |  |  |  |  |  |  |  |  | ✅ |  |  |  |  | 
| 46 | Span Chart                | ✅ |  |  |  |  |  |  |  |  |  |  |  | ✅ |  |  |  | 
| 47 | Spiral Plot               |  |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 48 | Stacked Area Graph        | ✅ |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 49 | Stacked Bar Graph         | ✅ | ✅ |  |  |  |  | ✅ |  |  |  |  |  |  |  |  | 
| 50 | Stem and Leaf Plot        |  |  |  |  |  |  |  | ✅ |  |  |  |  |  |  |  | ✅ |
| 51 | Stream Graph              |  |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ |  |  | 
| 52 | Sunburst Diagram          |  |  |  | ✅ |  |  | ✅ |  |  |  |  |  |  |  |  |  | 
| 53 | Tally Chart               | ✅ |  |  |  |  |  |  | ✅ |  |  |  |  |  |  |  |  | 
| 54 | Timeline                  |  |  |  |  |  |  |  | ✅ |  |  |  | ✅ |  | ✅ |  |  | 
| 55 | Timetable                 |  |  |  |  |  |  |  |  |  |  |  |  |  | ✅ |  | ✅ | 
| 56 | Tree Diagram              |  |  | ✅ | ✅ |  |  |  |  |  |  |  |  |  |  |  | ✅ | 
| 57 | Treemap                   | ✅ | ✅ |  | ✅ |  |  | ✅ |  |  |  |  |  |  |  |  |  | 
| 58 | Venn Diagram              | ✅ |  | ✅ |  | ✅ |  |  |  |  |  |  |  |  |  |  |  | 
| 59 | Violin Plot               |  |  |  |  |  |  |  | ✅ |  |  |  | ✅ | ✅ |  |  |  | 
| 60 | Word Cloud                |  | ✅ |  |  |  |  |  |  |  |  |  |  |  |  | ✅ |  | 

## 4. おわりに
この記事では、データビジュアリゼーション手法を60種類紹介しました。知識として把握しておくことは、資料作りのアイディアを出したり、資料を理解したりする際にも役立つかなと思います。
整理する過程で知らない手法もあって勉強になりました。もちろんここで紹介した以外にも、ボロノイ図やファネル・チャートなど他にも多くの手法が存在しますので、その都度インプットしていきたいですね。

## 5. 参考
https://datavizcatalogue.com
