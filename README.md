# MakeDataset_IXI
IXI Datasetをpi2pixやCycleGANで利用できる形に変換するツール

## データDL先
🔗[IXI dataset - Brain Development](https://brain-development.org/ixi-dataset/)

上記リンクより600例のMRIのデータセットがDLできる。今回はその中からT2とPDをDL後、Google Driveに解凍せずアップロードする。

## 処理内容
### データの展開
Google DriveにアップローダされたデータをGoogle Colab上に展開する。展開したデータのうち、データセットに含める例をさらに展開する。

### pix2pix用の処理
<a href="https://www.kaggle.com/vikramtiwari/pix2pix-dataset">
  <img src="https://i.gyazo.com/27b4dcff32749be36a1cd5c6972ddc41.png" width="320" />
</a>

バークレー校が配布している[pix2pix/dataset](https://people.eecs.berkeley.edu/~tinghuiz/projects/pix2pix/datasets/)のデータセットは、変換前の画像と変換後の画像が、1枚の画像の左右でペアになっている。このようになるようにT2画像とPD画像をconcatenateし、ペア画像を作成する。

<img src="https://i.gyazo.com/f26a7426587f906f55d33c7371057f7c.png" width="320" />

### 画像の保存
16bit の.tiffファイルとして、読み込んだMRIの画像データを保存する。
#### pix2pixでのディレクトリ構成
``` 
T2PD_pix2pix/
        ├ test/
        │  └ 136files
        └ train/
            └ 358files
```

#### CycleGANでのディレクトリ構成
```
T2PD_cyclegan/
    ├ trainA/
    │    └ T2 image 358files
    ├ testA/
    │    └ T2 image 136files
    ├ trainB/
    │    └ PD image 358files
    └ testB/
         └ PD image 136files
```
