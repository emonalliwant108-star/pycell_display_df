# pycell_display_df 0.2.0 検証結果

確認日: 2026-11-09 JST。

## 自動検証

- Python 3.11.13、pandas 3.0.2、Polars 1.27.1、IPython 9.3.0でPythonテスト49件PASS。
- Nodeのテスト17件PASS。送信元notebookの照合、JSON入力境界、kernel応答、同梱Pythonのmemory読込を含む。
- Nodeのうち11件はbuild済みrendererをDOM実装へmountし、実Python backendと接続する。値・列名・列順・列削除、Undo／Redo、複数出力と画面外出力の同期、filter、Polars固定列、HTML文字列をtextとして表示することを確認。
- Pythonでは元objectとdtypeの保持、headの元df対応、重複index／列名、nanosecond／timezone、不正入力・外部更新の拒否、失敗時のrollbackを確認。

## 配布物の確認

公開用コピーをbuild・packageしたVSIXについて、同梱runtime・文書・例Notebookをコピー側sourceとbyte照合する。VSIXを別folderへ展開し、その同梱Pythonからmemory bootstrap、pandas／Polarsの編集、Undo／Redo、複数出力同期と例Notebookの実行を検証する。

公開前にVSIX内の全fileと公開用文書を走査し、認証情報・個人の絶対path・不要な設定やcacheの混入を確認する。この確認は完全な不在を保証するものではない。

## 未確認の範囲

0.2.0の実VS Code画面、狭いwindowでの配置、実mouseによるdrag、remote kernel、Windows／Linuxでの動作は今回未確認。DOMテストは実browserのlayoutを検査しない。過去versionのGUI検証結果を0.2.0の保証として扱わない。

表の編集はmemory内の元DataFrameを更新する。fileへの自動保存はなく、Undo／Redoはkernel再起動を越えて保存されない。更新後はVS CodeのwindowとPython kernelを再起動し、再度有効化して出力cellを実行する。
