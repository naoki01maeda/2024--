## 物体間の関係性を考慮した車載カメラ画像からのリスク要因推定

<img width="600" alt="モデル図" src="https://github.com/naoki01maeda/2024-maeda/assets/98692841/b0fcb92f-966a-401e-856d-091b31dd134a">
<img width="679" alt="出力例" src="https://github.com/naoki01maeda/2024-maeda/assets/98692841/a758c736-2ebe-4a16-8633-b56b48a91b62">


### ■フォルダやファイルの説明

<details>
<summary>paperフォルダ</summary>
<div>
  
論文執筆関連のファイルを収録

- __texファイル(main.tex)__
  - 論文の本文をtex言語で記述したテキストファイル
    
- __styファイル(mthesis.tex)__
  - texファイルから出力される文書のスタイルやレイアウトの設定を記述したファイル
  - main.texで呼び出される
    
- __bibファイル(refs.bib)__
  - 参考文献を一括管理するためのファイル
  - main.texで呼び出される

- __imageフォルダ__
  - 論文内に含まれる画像(pdf形式)を収録

- __pptxファイル(slide.pptx)__
  - 研究発表で使用したスライドファイル(アニメーションあり)

</div>
</details>


<details>
<summary>codeフォルダ</summary>
<div>
  
研究で使用したコード、データセットを収録

- __メイン処理を行うファイル(main.ipynb)__
  - ベースラインモデル、提案手法モデルを訓練、学習済み重みの保存を行う

- __収集した元データを編集するファイル(data_editing.ipynb)__
  - アノテーションで得られたデータおよび、yolov5で得られる検出データを使用して訓練する形に加工する
  - ラベル数削減や、アンダーサンプリングを行う

- __データ取集で使用するアノテーションソフトのファイル(data_collection_software.ipynb)__
  - tkinterで記述されたデータ取集で使用するアノテーションソフト

- __出力結果を表示するファイル(output_display.ipynb)__
  - 学習済みモデルを使用して評価値(f1, recall, precision)を出力する
  - 学習済みモデルを使用して、推論結果を画像として保存する

- __総合的な評価値を算出するファイル(test_eval_summarize.ipynb)__
  - output_display.ipynbにより算出された評価値をすべて記述し、データ分割パターンごとの評価値の平均や標準偏差を出力する

- __運転シーンのクリップを作成するファイル(clip_generate.ipynb)__
  - DRAMAデータセットから運転シーンのクリップ(gif)を取り出し、新たに保存する
  - 保存されたクリップはデータ収集で使用される(データ収集以外は使用されない)

- __gifからmp4に変換するファイル(gif_to_mp4.ipynb)__
  - clip_generate.ipynbにより保存された運転シーンのクリップgifファイルを、データ収集ソフトで使用するために、mp4に変換する

- __運転シーンの画像を作成するファイル(pkl_to_img.ipynb)__
  - 訓練で使用する運転シーンの画像を作成するためにDRAMAデータセットに収録されたpklファイルからimgファイルとして新たに保存する

- __アノテーションされたデータを表示するファイル(anno_img_display.ipynb)__
  - データ収集で記録されたデータを表示する(boxの位置やラベル)

- __カッパ係数を算出するファイル(kappa.ipynb)__
  - すべてのアノテータの組み合わせで一致度を算出する
    
<details>
<summary>datasetフォルダ</summary>
<div>

- __annotation_dataフォルダ__
  - すべてのアノテータのデータを収録

- __kappaフォルダ__
  - すべてのアノテータの一致度を算出するために使用した運転シーンやアノテーションデータを収録

</div>
</details>

<details>
<summary>requirementsフォルダ</summary>
<div>

- __condaコマンドでインストールしたライブラリを示したファイル(conda_requirements.txt)__


- __pipコマンドでインストールしたライブラリを示したファイル(pip_requirements.txt)__


</div>
</details>

</div>
</details>

### ■再現手順

<details>
<summary>訓練</summary>
<div>

</div>
</details>

<details>
<summary>推論</summary>
<div>

</div>
</details>

