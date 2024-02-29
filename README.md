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
<summary>code_and_datasetフォルダ</summary>
<div>
  
研究で使用したコード、データセットを収録

- __メイン処理を行うファイル(main.ipynb)__
  - ベースラインモデル、提案手法モデルを訓練、学習済み重みの保存を行う
  - 学習済みモデルを使用して、推論結果を画像として保存する
  
- __収集した元データを編集するファイル(data_editing.ipynb)__
  - アノテーションで得られたデータおよび、yolov5で得られる検出データを使用して訓練する形に加工する
  - ラベル数削減や、アンダーサンプリングを行う

- __データ取集で使用するアノテーションソフトのファイル(data_collection_software.ipynb)__
  - tkinterで記述されたデータ取集で使用するアノテーションソフト

- __出力結果を表示するファイル(output_display.ipynb)__
  - 学習済みモデルを使用して評価値(f1, recall, precision)を出力する

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
    
<details>
<summary>datasetフォルダ</summary>
<div>

- __annotation_dataフォルダ__
  - すべてのアノテータのデータを収録

- __yolov5の出力結果を記録したファイル(datect.json)__
  - 各運転シーンで検出された物体の位置、クラスラベル、信頼度を記録している

- __データ収集で使用したマニュアルのファイル(manual.pdf)__
  
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
<summary>前処理</summary>
<div>

データ収集、訓練、推論を行う前の前処理(必須)

1. __./requirements/conda_requirements.txtを使用して環境を構築__

2. __./requirements/pip_requirements.txtを使用して環境を構築__

3. __DRAMAデータセットが格納された以下の写真のドライブを自PCに接続し、drama_data2/processed/trainというフォルダ内のpklデータをdatasetフォルダにコピーする__

     ![IMG_20240229_091833](https://github.com/naoki01maeda/2024-maeda/assets/98692841/4e6758dc-661c-415a-9e31-65f1a36c6538)

     コピー先のフォルダ名をpkl_dataにする必要あり

4. __DRAMAデータセットが格納された以下の写真のドライブを自PCに接続し、clip_generate.ipynbを実行して、DRAMAデータセットのcombinedフォルダに記録されたgifファイルで保存された運転シーンのデータをdrama_clipフォルダに保存する__

    ![IMG_20240229_091850](https://github.com/naoki01maeda/2024-maeda/assets/98692841/45f4dcbb-570c-4e61-bd6d-639204b1dc4d)

    実行するとdatasetフォルダ下に、以下のフォルダが作成される
     - drama_clip(運転シーンのクリップの各フレームが保存されたフォルダ)

5. __gif_to_mp4.ipynbを実行して、drama_clipフォルダに保存されたgifファイルをmp4ファイルに変換する__

6. __pkl_to_img.ipynbを実行して、DRAMAデータセットの運転シーンのデータが格納されたpklファイルを、jpgファイルに変換してdrama_imageフォルダに保存する__

    実行するとdatasetフォルダ下に、以下のフォルダ
     - drama_image(運転シーンの画像が保存されたフォルダ)
    
7. __data_editing.ipynbを実行して、訓練、推論をするためのデータを作成する__

    実行するとdatasetフォルダ下に、以下のフォルダ、ファイルが作成される
   
    - split_id_data(フォルダ内には分割パターンごとの訓練、検証、テストデータの画像IDが保存されたjsonファイルが格納されている)
    - split_data1(分割パターン1の訓練、検証、テストデータ)
    - split_data2(分割パターン2の訓練、検証、テストデータ)
    - split_data3(分割パターン3の訓練、検証、テストデータ)
    - split_data4(分割パターン4の訓練、検証、テストデータ)
    - split_data5(分割パターン5の訓練、検証、テストデータ)
    - all_dataset_dis(データセットを画像として可視化したjpgファイルが格納される)
    - all_dataset.json(訓練、検証、テストで使用するすべてのデータが記録されたjsonファイル)
  
   作業ディレクトリに、以下のフォルダが作成される

    - graph_img(データセットの様々な分布の画像が格納される)


</div>
</details>

<details>
<summary>データ収集</summary>
<div>
  
運転シーンのクリップを使用してデータ収集を実施

1. __前処理を行う__

2. __data_collection_software.ipynbを実行して、データ収集画面を表示させる__

   実行前に保存するjsonファイルの名前を指定する(コード参照)

4. __./dataset/manual.pdfのデータ収集マニュアルに従いデータを収集する__
  

</div>
</details>

<details>
<summary>訓練</summary>
<div>

訓練の実施

1. __前処理を行う__

2. __main.pyを実行して訓練を開始する__

   実行すると学習が開始され、以下のファイルが作業ディレクトリに作成される
     - log(学習済みの重みおよび、学習ごとの評価値の推移が記録される)

__自身のシード値設定ミスにより、再現不可なモデルあり__
<img width="621" alt="再現性表" src="https://github.com/naoki01maeda/2024-maeda/assets/98692841/f8291ea5-6dd5-4b12-a15a-2b876941e5cc">

</div>
</details>

<details>
<summary>推論</summary>
<div>

推論の実施

1. __前処理を行う__
  
2. __訓練を行う__

3. __output_display.ipynbを実行して、各手法の評価値を算出する__

    訓練によりlogフォルダに保存された各手法のデータを可視化する

4. __test_eval_summarize.ipynbを実行して、データ分割パターンごとの評価値の平均や標準偏差を出力する__

    output_display.ipynbによって得られた結果を記載し、分割パターンごとの評価値の平均や標準偏差を出力する

5. __main.pyの最後のセル(推定結果を画像として出力)を実行__

    推論結果を画像として保存する際、作業ディレクトリに以下のフォルダが作成される
   
      - output(推論結果を画像として保存される)
        - output_test_data(0.5を閾値とした結果を表示)
        - output_test_data_sig(予測値をそのまま表示)
        - output_test_data_att(提案手法で使用されるTransformerのMHAattentionmapを表示)
  
</div>
</details>

