# NP_TagEX

http://japan.nucleuscms.org/wiki/plugins:tagex

http://japan.nucleuscms.org/forum/viewtopic.php?id=2473

記事にタグをつける機能を追加するプラグイン。
タグによるフィルタリング表示をするためには [NP_ShowBlogs](https://github.com/NucleusCMS/NP_ShowBlogs) v.2.04以上が必要。

作者: nakahara21, shizuki, Tucker, Cacher

フォーラム参照先 http://japan.nucleuscms.org/bb/viewtopic.php?p=15433


## インストール方法
  - Zipファイルを展開して、中身をサーバーのプラグインディレクトリにアップロードする
  - 管理画面からプラグインをインストールする







## このプラグインの使い方
記事の新規投稿または編集画面の「追加プラグインオプション」にてタグを入力します。
{{:plugins:taginput.gif |タグの入力画面 }}
  * テキストエリアにタグを入力します。
  * すでに登録済みのタグが右側に表示されています。クリックすると自動入力します。
  * テキストエリア上の「reset」を押すと編集前の状態にリセットされます。
  * 複数のタグを指定する場合は、半角カンマ「,」もしくは改行で区切ってください。
  * 先頭と末尾の半角スペースは削除されます。それ以外のスペースはタグとして利用できます。


## スキン/テンプレートへの記述

  * タグによるフィルタリングを行っているページにてその指定タグをガイドする機能
  * 登録済みタグのリストをリンク付きで表示する機能
  * たくさん指定した記事があるタグほど大きいフォントでリスト表示するウェイト付け機能(タグクラウド／TagCloud)
があります。

### スキン変数

  - <code file><%TagEX(tag)%></code>選択されているタグをリンクつきで表示
    * 表示形式:Tag for TAG-A + TAG-B or TAG-C
  - <code file><%TagEX(list20/2/1/1/4)%></code>登録済みのタグのリストをリンクつきで表示
    * パラメータの解説
       - 第1パラメータ：モード・数指定(ist20：タグを20個リスト表示)
       - 第2パラメータ：カテゴリ追従モードの指定
         * 0 -> ブログ・カテゴリ問わず全てのタグを表示
         * 1 -> 表示中のブログに属するタグのみ表示
         * 2 -> 表示中のカテゴリに属するタグのみ表示
       - 第3パラメータ：タグの並び順指定
         * 1 -> そのタグが打ってあるアイテムの多い順
         * 2 -> そのタグが打ってあるアイテムの少ない順
         * 3 -> タグあいうえお・アルファベット順
         * 4 -> ランダム
       - 第4パラメータ：リスト中の文字の最小サイズ
       - 第5パラメータ：リスト中の文字の最大サイズ
  - <code file><%TagEX(meta20/2/1)%></code>登録済みのタグのリストを<meta keyword="" />に出力
    * パラメータは list と同じ
  - <code file><%TagEX(meta2/ad)%></code>タグを AWS 用に変換して出力
  - <code file><%TagEX(title)%></code>選択中のタグを表示(<title></title>用)
    * 表示形式:Tag for TAG-A|TAG-B|TAG-C

### テンプレート変数
  - <code file><%TagEX()%></code>アイテムに付与されているタグのリストをリンクつきで表示

  - 「テンプレートの説明」に
    - <highlightTagsAll> と記述する事で、タグに指定してある全ての文字列を
    - <highlightTags> と記述する事で、選択中のタグと同じ文字列を
ハイライト表示させます

## オプション
  * Erase data on uninstall.\\ プラグインをアンインストールする時にデータテーブルを削除するか
  * editform tag order\\ アイテムの追加・編集画面でのタグの並び順
    * amount(desc)
    * amount(asc)
    * TAG order
    * random
  * show tags only current blog\\ アイテムの追加・編集画面で表示するタグをカレントのブログに所属するもののみにするか
  * colorful highlight mode ?\\ CSS ファイルを使用してタグのハイライトをカラフルに表示(最大10色)
  * template for normal highlightmode\\ カラフル表示しない場合のタグハイライト用テンプレート

  * template for 'and'\\ タグリスト中の '&' リンク用テンプレート
  * template for 'or'\\ タグリスト中の 'or' リンク用テンプレート
  * template for 'tagIndex'\\ タグリスト中のタグ表示用テンプレート
  * template for 'tagItemHeader'\\ タグリスト中のタグが指定されているアイテムのリストのヘッダ用テンプレート
  * template for 'tagItem'\\ タグリスト中のタグが指定されているアイテムのリスト用テンプレート
  * template for 'tagItemSeparator'\\ タグリスト中のタグが指定されているアイテムのセパレータ用テンプレート
  * template for 'tagItemFooter'\\ タグリスト中のタグが指定されているアイテムのリストのフッタ用テンプレート
  * template for 'tagIndexSeparator'\\ タグリスト中のタグのセパレータ用テンプレート

#### タグリストテンプレート内変数

```
<%andurl%>\\ '&' リンクの URL
<%orurl%>\\ 'or' リンクの URL
<%fontlevel%>\\ スキン変数で指定した最大/最小フォントサイズと該当タグを指定してあるアイテムの数から導き出されたフォントサイズ
<%tagamount%>\\ 該当タグを指定してあるアイテムの数
<%taglinkurl%>\\ タグのリンク
<%tag%>\\ タグ自身
<%itemid%>\\ 該当タグを指定してあるアイテムのID
<%itemtitle%>\\ 該当タグを指定してあるアイテムのタイトル(10バイトに短縮)
<%and%>\\ [ template for 'and' ] の内容
<%or%>\\ [ template for 'or' ] の内容
<%tagitems%>\\ [ template for 'tagItemHeader' ]+[ template for 'tagItem' ]+[ template for 'tagItemSeparator' ]+[ template for 'tagItemFooter' ] の内容
```


## Tipsと裏技
admin.cssに次のように追記すると、タグをインラインで表示できます。タグの数が多い場合は見やすくなります。

<code>
div.tagex li {display:inline;}
div.tagex li a:hover {background-color:#d9dce6;}
</code>

## 希望事項
  * <del>タグ入力支援の登録済みタグリストの表示カスタマイズ。v0.4ではたくさん使われている順に並列表示のみ。</del>\\ 0.42 で並び順をプラグインオプションから指定可能に
  * <del>タグ入力支援の登録済みタグリストを、編集中のblogに属する記事で指定したタグのみとする機能。\\ [[http://blog.uribou.net/item395.html|uridev - NP_TagEXをちょっと改造]]参照。</del>\\ 0.42 でプラグインオプションから指定可能に
  * <del>タグの並び順に｢タグ順｣｢ランダム｣を追加\\ [[http://blog.uribou.net/item395.html|uridev - NP_TagEXをちょっと改造]]参照。</del>\\ 0.42 でマージ。対応済み
  * タグラベルの階層化。考え中。

## バグ

## 開発履歴
  * version 0.4 [2005-11-14]
    * バグ修正(タグ削除時の動作)。
    * 半角数字のみのタグに対応。


  * version 0.2 [2005-10-30]
    * 2つ以上のタグのand/orフィルタリングに対応。


  * version 0.1 [2005-10-21]
    * 初回リリース
