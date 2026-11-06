<a id="toc"></a>
## 目次

- [int_testcase](#int_testcase): 整数のパース
  - [01.txt](#int_testcase-01): nb_drones の全角・`+`・`_`・先頭のゼロ
  - [02.txt](#int_testcase-02): nb_drones の 0・負・小数・余分な値
  - [03.txt](#int_testcase-03): 座標
  - [04.txt](#int_testcase-04): max_drones
  - [05.txt](#int_testcase-05): max_link_capacity
- [color_testcase](#color_testcase): 色の値
  - [01.txt](#color_testcase-01): 配られた地図にある名前、同じ形の名前
  - [02.txt](#color_testcase-02): 大文字・ASCII 以外・数字・アンダースコア
  - [03.txt](#color_testcase-03): ダッシュ・none・指定なし・`#`・空・2 語
  - [04.txt](#color_testcase-04): 接続に色
  - [05.txt](#color_testcase-05): ログに色の制御文字が混ざらないか
- [prove_priority](#prove_priority): priority の扱い
  - [01.txt](#prove_priority-01): 同点のときの priority、優先しすぎ
- [prove_restricted](#prove_restricted): restricted の規則
  - [01.txt](#prove_restricted-01): 接続の空き方、着く先が満杯、2 つ続く
  - [02.txt](#prove_restricted-02): PDF 9 ページの例の地図
- [prove_follow_through](#prove_follow_through): 出て行く分は同じターンで空く
  - [01.txt](#prove_follow_through-01): 一本道で、出る分が同じターンに空くか
- [prove_capacity](#prove_capacity): ゾーンと接続の容量
  - [01.txt](#prove_capacity-01): 容量の既定値、容量 2、start と end
- [prove_cost](#prove_cost): 移動のコストを考えた経路
  - [01.txt](#prove_cost-01): restricted の遠回り・近道、blocked の迂回
- [prove_unreachable](#prove_unreachable): start から end へ行けない地図
  - [01.txt](#prove_unreachable-01): 行けない地図、start や end が blocked
- [many_drones](#many_drones): ドローンが非常に多いとき
  - [01.txt](#many_drones-01): 100・1000・10000 台
  - [02.txt](#many_drones-02): 1 台と 10 億台
- [no_traceback](#no_traceback): ファイルそのものの異常
  - [01.txt](#no_traceback-01): 空のファイル
  - [02.txt](#no_traceback-02): コメントしか無い
  - [03.txt](#no_traceback-03): UTF-8 でない
  - [04.txt](#no_traceback-04): BOM
  - [05.txt](#no_traceback-05): CRLF
  - [06.txt](#no_traceback-06): バイナリ
  - [07.txt](#no_traceback-07): 読む権限が無い
  - [08.txt](#no_traceback-08): 最後に改行が無い
- [parse_format](#parse_format): 空白・記号・大文字などの書き方
  - [01.txt](#parse_format-01): nb_drones の行
  - [02.txt](#parse_format-02): メタデータ
  - [03.txt](#parse_format-03): 接続の行
  - [04.txt](#parse_format-04): 受理すべき書き方の全部入り
  - [05.txt](#parse_format-05): nb_drones が最初の行でない
- [undefined_by_pdf](#undefined_by_pdf): PDF に書かれていない場合
  - [01.txt](#undefined_by_pdf-01): キーの誤りと重複、同じ座標
  - [02.txt](#undefined_by_pdf-02): 自分自身への接続、逆向きの重複
  - [03.txt](#undefined_by_pdf-03): start と end の容量 0、restricted
  - [04.txt](#undefined_by_pdf-04): ゾーン名の記号・日本語・D1

<a id="int_testcase"></a>
## int_testcase

<a id="int_testcase-01"></a>
### [01.txt](int_testcase/01.txt)

| ケース | 期待 |
|---|---|
| nb_drones に全角の `５` | (自作。コメントに期待なし) |
| nb_drones に先頭の `+5` |  |
| nb_drones に `1_0` |  |
| nb_drones に先頭のゼロ `05` |  |

<a id="int_testcase-02"></a>
### [02.txt](int_testcase/02.txt)

| ケース | 期待 |
|---|---|
| nb_drones が `0` | 拒否(4 行目) |
| nb_drones が `-2` | 拒否(6 行目) |
| nb_drones が `2.0` | 拒否(8 行目) |
| nb_drones の後ろに余分な値 `5 5` | 拒否(10 行目) |

<a id="int_testcase-03"></a>
### [03.txt](int_testcase/03.txt)

| ケース | 期待 |
|---|---|
| 座標にアラビア・インド数字 `١`(U+0661) | 拒否(6 行目) |
| 座標が `+1` | 判断 |
| 座標が `-0` | 受理(0 として) |
| 座標が指数表記 `1e3` | 拒否(12 行目) |
| 座標が 10 の 30 乗。視覚表示で落ちないか | 受理 |

<a id="int_testcase-04"></a>
### [04.txt](int_testcase/04.txt)

| ケース | 期待 |
|---|---|
| max_drones が上付きの `²`(`isdigit()` は真、`int()` は例外) | 拒否(6 行目) |
| max_drones が 16 進数 `0x2` | 拒否(8 行目) |
| max_drones の値が空 | 拒否(10 行目) |
| max_drones が `+2` | 拒否(12 行目) |

<a id="int_testcase-05"></a>
### [05.txt](int_testcase/05.txt)

| ケース | 期待 |
|---|---|
| max_link_capacity が `-1` | 拒否(8 行目) |
| max_link_capacity が `0` | 拒否(10 行目) |
| max_link_capacity が `2.0` | 拒否(12 行目) |
| max_link_capacity が全角の `２` | 拒否(14 行目) |

[目次に戻る](#toc)

<a id="color_testcase"></a>
## color_testcase

<a id="color_testcase-01"></a>
### [01.txt](color_testcase/01.txt)

| ケース | 期待 |
|---|---|
| 8 色に無い名前 `rainbow` | 受理(配られた地図にある) |
| 8 色に無い名前 `orange` | 受理(配られた地図にある) |
| 8 色に無い名前 `gray` | 受理(配られた地図の名前と同じ形) |
| 2 語をつなげた名前 `darkblue` | 受理(配られた地図の名前と同じ形) |
| 8 色に無い名前 `purple` | 受理(配られた地図にある) |

<a id="color_testcase-02"></a>
### [02.txt](color_testcase/02.txt)

| ケース | 期待 |
|---|---|
| 大文字 `RED` | 実装依存 |
| 大文字と小文字の混在 `Blue` | 実装依存 |
| ASCII でない名前 `赤` | 実装依存 |
| 数字だけ `123` | 実装依存 |
| アンダースコア `dark_blue` | 実装依存 |

<a id="color_testcase-03"></a>
### [03.txt](color_testcase/03.txt)

| ケース | 期待 |
|---|---|
| ダッシュを含む `red-ish` | 実装依存 |
| `none` を明示(PDF の既定値) | 受理 |
| 色の指定なし | 受理 |
| 16 進の `#ff0000`(`#` はコメントの始まりでもある) | 判断 |
| 値が空 `color=` | 判断 |
| 2 語 `light blue`(1 語ではない) | 拒否が自然 |

<a id="color_testcase-04"></a>
### [04.txt](color_testcase/04.txt)

| ケース | 期待 |
|---|---|
| 接続に色 | 判断 |
| 接続に色と容量 | 判断 |

<a id="color_testcase-05"></a>
### [05.txt](color_testcase/05.txt)

| ケース | 期待 |
|---|---|
| PDF 9 ページの例の地図。ログに色の制御文字が混ざらないか | 受理。`cat -A` で `^[[` が出ない |

- PDF は色の値を「どんな valid な 1 語の文字列でもよい」とする。配られた地図には `rainbow`・`crimson`・`gold`・`maroon` などがあり、小文字の英単語を拒否すると、配られた地図が動かない。
- 「実装依存」は、valid の範囲(大文字・数字・記号・ASCII 以外)が PDF に無いもの。受理でも拒否でもよいが、落ちないこと。理由を聞く。
- どのケースでも、表示する色(何色で出すか、`RED` を `red` と同じにするか)は実装依存。

[目次に戻る](#toc)

<a id="prove_priority"></a>
## prove_priority

<a id="prove_priority-01"></a>
### [01.txt](prove_priority/01.txt)

地図ごと切り替えます。

| ケース | 期待 |
|---|---|
| 同じ 3 ターンの経路が 2 本。priority の経路を後に定義 | 3 ターン。p1, p2 を通る |
| 上の鏡。priority の経路(b1, b2)を先に定義 | 3 ターン。b1, b2 を通る |
| priority の経路のほうが 1 ターン長い | 2 ターン。a1 を通る |
| restricted の経路(2+1)と priority の経路が同点 | 3 ターン。p1, p2 を通る |
| 1 つ目の地図で 3 台 | 4 ターン。2 本とも使う(全員 priority だと 5) |

[目次に戻る](#toc)

<a id="prove_restricted"></a>
## prove_restricted

<a id="prove_restricted-01"></a>
### [01.txt](prove_restricted/01.txt)

| ケース | 期待 |
|---|---|
| PDF 13 ページの例(end が restricted、接続の容量 1) | 3 ターン(接続を 2 ターンとも数えると 4) |
| 同じ地図で、接続を `r-s` の向きで書く | 3 ターン。出力が `D1-r-s` か `D1-s-r` かを見る |
| `s - r - e`、3 台 | 5 ターン(2 ターンとも数えると 7) |
| 着く先が満杯なら出発しない | 4 ターン(3 なら r に 2 台で違反) |
| restricted が 2 つ続く | 6 ターン。r1 から r2 は `D<ID>-r1-r2` と出る |

<a id="prove_restricted-02"></a>
### [02.txt](prove_restricted/02.txt)

| ケース | 期待 |
|---|---|
| PDF 9 ページの例の地図 | 5 ターン(2 ターンとも数えると 6) |

[目次に戻る](#toc)

<a id="prove_follow_through"></a>
## prove_follow_through

<a id="prove_follow_through-01"></a>
### [01.txt](prove_follow_through/01.txt)

地図ごと切り替えます。

| ケース | 期待 |
|---|---|
| 出て行くドローンの分は、同じターンで空く | 3 ターン(空かないと 4) |
| 容量 1 のゾーンが 3 つ続く一本道に 3 台 | 6 ターン(4 + 3 − 1) |

[目次に戻る](#toc)

<a id="prove_capacity"></a>
## prove_capacity

<a id="prove_capacity-01"></a>
### [01.txt](prove_capacity/01.txt)

地図ごと切り替えます。

| ケース | 期待 |
|---|---|
| 接続の容量の既定値は 1(ゾーン a は 2 台入れる) | 3 ターン(無視すると 2) |
| ゾーンの容量の既定値は 1(接続は 2 台通せる) | 3 ターン(無視すると 2) |
| 接続の容量 2 で 4 台 | 3 ターン |
| start と end の容量は無制限 | 2 ターン(end に容量 1 を当てはめると 5) |

[目次に戻る](#toc)

<a id="prove_cost"></a>
## prove_cost

<a id="prove_cost-01"></a>
### [01.txt](prove_cost/01.txt)

地図ごと切り替えます。

| ケース | 期待 |
|---|---|
| ゾーンの数では短いが、restricted を 2 つ通るので遅い経路 | 4 ターン。a, b, c を通る(ホップ数の BFS だと 5) |
| restricted を通るほうが速い(3 対 4 ターン) | 3 ターン。r を通る |
| 最短の経路の途中が blocked | 3 ターン。a, b を通る(2 なら blocked の x に入っている) |

[目次に戻る](#toc)

<a id="prove_unreachable"></a>
## prove_unreachable

<a id="prove_unreachable-01"></a>
### [01.txt](prove_unreachable/01.txt)

地図ごと切り替えます。

| ケース | 期待 |
|---|---|
| end へつながる接続が無い | パースのエラーとは別の報告で止まる |
| 唯一の経路の途中が blocked | パースのエラーとは別の報告で止まる |
| start の周りに輪(s-a-b-s)があり、end は孤立。1000 台 | パースのエラーとは別の報告で止まる |
| end_hub 自体が blocked | 判断。受理なら「行けない」と報告する |
| start_hub 自体が blocked | 判断。受理なら 3 ターンか「行けない」 |

[目次に戻る](#toc)

<a id="many_drones"></a>
## many_drones

<a id="many_drones-01"></a>
### [01.txt](many_drones/01.txt)

| ケース | 期待 |
|---|---|
| easy/02_simple_fork の地図で 100 台 | 52 ターン |
| 同じ地図で 1000 台 | 502 ターン前後(推定)。時間が台数に比例して伸びるか |
| 同じ地図で 10000 台 | 5002 ターン前後(推定) |

<a id="many_drones-02"></a>
### [02.txt](many_drones/02.txt)

| ケース | 期待 |
|---|---|
| 1 台、start と end が直結 | 1 ターン(`D1-e`) |
| 10 億台 | Traceback や MemoryError で落ちない |

[目次に戻る](#toc)

<a id="no_traceback"></a>
## no_traceback

コメントアウトでは作れない異常なので、1 ファイルに 1 ケースです。

<a id="no_traceback-01"></a>
### [01.txt](no_traceback/01.txt)

| ケース | 期待 |
|---|---|
| 空のファイル | 拒否 |

<a id="no_traceback-02"></a>
### [02.txt](no_traceback/02.txt)

| ケース | 期待 |
|---|---|
| コメントしか無い | 拒否 |

<a id="no_traceback-03"></a>
### [03.txt](no_traceback/03.txt)

| ケース | 期待 |
|---|---|
| UTF-8 でない(ゾーン名に 0xE9 のバイト) | 拒否 |

<a id="no_traceback-04"></a>
### [04.txt](no_traceback/04.txt)

| ケース | 期待 |
|---|---|
| 先頭に UTF-8 の BOM | 判断 |

<a id="no_traceback-05"></a>
### [05.txt](no_traceback/05.txt)

| ケース | 期待 |
|---|---|
| 改行が CRLF。名前の末尾に `\r` が残らないか | 受理 |

<a id="no_traceback-06"></a>
### [06.txt](no_traceback/06.txt)

| ケース | 期待 |
|---|---|
| NUL を含むバイナリ | 拒否 |

<a id="no_traceback-07"></a>
### [07.txt](no_traceback/07.txt)

| ケース | 期待 |
|---|---|
| 読む権限が無いファイル(`chmod 000` してから渡す) | 拒否 |

<a id="no_traceback-08"></a>
### [08.txt](no_traceback/08.txt)

| ケース | 期待 |
|---|---|
| 最後の行に改行が無い | 受理 |

ここでの「拒否」は、メッセージと 0 以外の終了コードで終わり、Traceback が出ないことです。

[目次に戻る](#toc)

<a id="parse_format"></a>
## parse_format

<a id="parse_format-01"></a>
### [01.txt](parse_format/01.txt)

| ケース | 期待 |
|---|---|
| `nb_drones:2`(コロンの後に空白が無い) | 判断 |
| `NB_DRONES: 2`(大文字) | 判断 |
| コロンの後がタブ | 受理 |
| 行末のコメント | 受理 |

<a id="parse_format-02"></a>
### [02.txt](parse_format/02.txt)

| ケース | 期待 |
|---|---|
| `[zone = priority]`(`=` の前後に空白) | 判断 |
| メタデータの中の `#` | 判断 |
| 座標と `[` の間に空白が無い | 判断 |
| メタデータの後ろに余分な語 | 拒否(12 行目) |
| 空のメタデータ `[]` | 判断 |
| `[Zone=Priority]`(大文字のキーと値) | 判断 |

<a id="parse_format-03"></a>
### [03.txt](parse_format/03.txt)

| ケース | 期待 |
|---|---|
| `connection: a - e`(ダッシュの前後に空白) | 判断 |
| 名前の直後にコメント `a-e#x` | 受理 |
| コロンの後がタブ | 受理 |
| `Connection:`(大文字) | 判断 |

<a id="parse_format-04"></a>
### [04.txt](parse_format/04.txt)

| ケース | 期待 |
|---|---|
| タブ、空行、字下げしたコメント、行末のコメント、ゾーンと接続が交互(全部入り) | 受理 |

<a id="parse_format-05"></a>
### [05.txt](parse_format/05.txt)

| ケース | 期待 |
|---|---|
| nb_drones が最初の行でない | 拒否(2 行目か 3 行目) |

[目次に戻る](#toc)

<a id="undefined_by_pdf"></a>
## undefined_by_pdf

<a id="undefined_by_pdf-01"></a>
### [01.txt](undefined_by_pdf/01.txt)

| ケース | 期待 |
|---|---|
| 知らないキー(タイプミス `max_drone`)。無視すると容量 3 の意図が消える | 判断 |
| 同じキーが 2 回。受理なら、どちらの値を使うか | 判断 |
| 同じ座標のゾーンが 2 つ。視覚表示で落ちないか | 受理 |

<a id="undefined_by_pdf-02"></a>
### [02.txt](undefined_by_pdf/02.txt)

| ケース | 期待 |
|---|---|
| 自分自身への接続 `a-a` | 判断 |
| 同じ接続を逆向きで、メタデータを変えてもう一度 | 拒否(12 行目。PDF: `a-b` と `b-a` は重複) |

<a id="undefined_by_pdf-03"></a>
### [03.txt](undefined_by_pdf/03.txt)

| ケース | 期待 |
|---|---|
| start の `max_drones=0` | 受理(PDF: 無視され、エラーではない) |
| start_hub が restricted | 判断。受理なら 3 ターン |
| end の `max_drones=0` | 受理(PDF: 無視され、エラーではない) |
| end_hub が restricted | 受理。4 ターン |

03.txt には、start と end の 2 か所に切り替える場所があります。それぞれ `# default` の行が有効になっています。

<a id="undefined_by_pdf-04"></a>
### [04.txt](undefined_by_pdf/04.txt)

| ケース | 期待 |
|---|---|
| ゾーン名に `:`、`[`、`]` | 判断 |
| ASCII でないゾーン名(日本語) | 受理 |
| `D1` という名前のゾーン | 受理。出力は `D1-D1` |

[目次に戻る](#toc)
