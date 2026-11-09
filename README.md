# pycell_display_df 0.2.0

VS CodeのJupyter notebookでpandas／Polars DataFrameを、固定見出し・全行filter・元DataFrameの編集ができる表として表示する拡張です。

## 導入

1. Releasesから `pycell_display_df-0.2.0.vsix` をdownloadします。
2. VS CodeのExtensions画面の「…」→「Install from VSIX...」でinstallします。
3. Jupyter拡張を用意し、Python kernelを選んでcellを一度実行します。
4. Command Paletteで `pycell_display_df: 有効化` を実行します。Jupyterからkernelへのアクセス許可を求められたら、この拡張へ許可します。
5. 次のcellを実行します。

```python
import pandas as pd

df = pd.DataFrame({"name": ["A", "B"], "value": [10, 20]})
pycell_display(df)
```

pandas／Polarsは利用するkernelに必要です。拡張用の追加pip installは不要です。VS Code 1.100以上、Python 3.10以上を対象としています。今回の自動検証環境と未確認範囲は `VALIDATION.md` を参照してください。

## 主な機能

- 固定見出し、pandas MultiIndex、Polars固定列、全行filter／sort、page移動。
- 値・列名・列順・一列全体の削除とUndo／Redo。
- `pycell_display(df.head())` から元dfへの反映、同じdfの複数出力の同期。
- `pycell.display(df)`、`pycell_display(df)`、`pycell_print(df)` による明示表示。
- 標準の `print()`、`display()`、末尾式は変更しません。

操作例は `editable_display.ipynb` をVS Codeで開いて実行してください。Polarsの例も含みます。

## 編集と更新時の注意

表の編集はmemory内の元dfを直接更新します。head表示でも列の削除・列名・列順の変更は元df全体に反映します。重要なdataではcopyを作ってから使用してください。fileへは自動保存しません。Undo／Redoはkernelの再起動を越えて保持されません。

更新後はVS CodeのwindowとPython kernelを再起動し、再度有効化して出力cellを実行してください。無効化はCommand Paletteの `pycell_display_df: 無効化` を使います。

## 配布fileの照合

downloadしたfilesと同じfolderで次を実行できます。

```sh
shasum -a 256 -c SHA256SUMS.txt
```

このrepositoryはReleasesによる配布用です。GitHubの自動生成するSource code ZIP／tar.gzにはVSIXを含みません。Assetsの `.vsix` をdownloadしてください。

## ライセンス

拡張のmanifestは `UNLICENSED` のままです。オープンソースライセンスは付与していません。VSIXに含むLucide等の第三者のnoticeとlicenseは、同梱の `THIRD_PARTY_NOTICES.md` と `dist/LUCIDE_LICENSE` を参照してください。
