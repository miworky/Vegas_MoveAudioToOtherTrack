# Vegas_MoveAudioToOtherTrack
# ●概要

このプログラムは、Vegas Pro のスクリプトです。
このスクリプトを使用すると、タイムラインに配置してある特定のトラックのオーディオファイルのうち、パターンにマッチするオーディオファイルを別のトラックに移動できます。

iPhoneのオーディオファイルだけ別のトラックに移したいときに使えます。


# ●背景

みてねから画像や動画をダウンロードして動画を作成したり、ブルーレイに焼いたりする際に、いくつか課題があります。
課題の一つに、撮影したカメラによって動画の音量が大きく違うことがあります。例えば、iPhoneで撮影した動画は（手持ちのどの）デジカメで撮影した動画に比べて音量が小さいです。
このため、iPhoneで撮影した動画だけ音量が小さくて聞きづらくなります。

そこで、本プラグインを使用してiPhoneで撮影した動画だけ別のトラックに移します。

その上で、iPhoneで撮影した動画のボリュームやコンプレッサの設定などを変更して、音量を上げます。




# ●動画作成手順

1)みてねからファイルをダウンロードする

  https://github.com/miworky/miteneDownloader

を使用してダウンロードしてください。
  ダウンロードしたファイルは、「YYYY-MM-DDThhmmss_みてねの1つめのコメント」というファイル名になります。
  
2)ダウンロードしたファイルを Vegas Pro のメディアプールに取り込み、タイムラインに貼り付けます。

　ダウンロードしたファイル名に日付が含まれているので、これだけでみてねからダウンロードしたファイルを撮影日時順にタイムラインに配置できます。
 　画像・動画は Track 2 に追加してください。
  
3)撮影日とコメントからテロップを作成します

　https://github.com/miworky/Vegas_AddTextEventFromFilename

を使用すると自動でテロップを追加できます。テロップは Track 1 に作成されます。

4)オリジナルの高解像度のファイルに差し替えます

       https://github.com/miworky/Vegas_ReplaceMediaFiles

を使用すると、自動でオリジナルの高解像度のファイルに差し替えできます。

5)お好きな BGM を貼り付けます

   https://github.com/miworky/Vegas_AddMusic
   
   を使用すると画像の部分に自動で BGM を追加できます。

6)iPhone で撮影した動画のオーディオを別のトラックに移します（本プログラムを使用します）

  iPhone で撮影した動画の音量は小さいので、いい感じに補正します。

7)iPhone で撮影した動画のオーディオの後ろを削除します

   https://github.com/miworky/Vegas_RemoveEndOfAudio
   
   を使用すると動画のオーディオの後ろを削除できます。

8)動画として書き出したり、ブルーレイに焼いたりします。

9)テロップの時刻と内容をテキストファイルに書き出します

  https://github.com/miworky/Vegas_ExportTextEvent

　を使用すると自動でテロップの時刻と内容をテキストファイルに書き出せます。


# ●デプロイ方法

C:\ProgramData\VEGAS Pro\Script Menu

に以下のファイルをコピーします：

MoveAudioToOtherTrack.cs


# ●実行方法

1)Vegas Pro から本スクリプトを実行します

  スクリプトなので Vegas Pro のバージョンによらずに動作するはず・・・（Vegas Pro 21.0 で動作確認しました）

2)ダイアログが表示されるので以下を入力します：

Video Track No(1-base): オーディオを移動したい動画のあるトラック番号（オーディオファイルのトラックではなく動画ファイルのトラックを指定します）

MovePattern:     移動するファイルを正規表現で指定します。

                 iPhoneで撮影した動画のみ移動したいのであれば「IMG.*」でOK。

Destination Track No(1-base)：移動先のトラック番号


3)ファイル選択ダイアログが開くので、作成するログのファイル名を指定します

4)しばらく時間が経った後に、「終了しました」というポップアップが開けば終了です



# ●参考（備忘録）
こちらでは以下のような設定にしています。


デジカメのオーディオトラック

トラックコンプレッサ

- 入力ゲイン 0dB
- 出力ゲイン 0dB
- Threshold -20.3dB
- ratio：  4.1 : 1
- Attack: 15ms
- Release: 250ms
- 自動ゲイン補正： On
- スムーズサチュレーション： Off

eFX_Limiter(VST2, 64 Bit)

- IN: 0dB
- OUT: -0.1dB
- threshold: 0dB
- release 10ms
- clip gain: 0dB



iPhoneのオーディオトラック

トラックコンプレッサ

- 入力ゲイン 2dB
- 出力ゲイン 3dB
- Threshold -39.4dB
- ratio：  4.2 : 1
- Attack: 15ms
- Release: 250ms
- 自動ゲイン補正： On
- スムーズサチュレーション： Off

eFX_Limiter(VST2, 64 Bit)

- IN: 0dB
- OUT: -0.1dB
- threshold: 0dB
- release 10ms
- clip gain: 0dB





