# arm-ml-env
arm環境に機械学習系packageを一通り導入するminiforge用設定ファイル。  
pythonの学習環境を作るときにはまることが多かったため、ハマらないために作った。
2022年4月版。  

**前提**
- M1 Mac
- miniforge (conda 4.10.1)

**含まれるpackage**
- scikit-learn
- pandas
- jupyterlab
- pytorch
- numpy
- opencv
- cython
- matplotlib
- and more...

**この設定ファイルを使うと嬉しいポイント**

1. armでの機械学習環境構築をハマらずにサクッと行えます。
2. 仮想環境の作成をyamlファイルで行うため、環境の再現や依存性の管理ができます。
3. 仮想環境を利用でき、依存性が仮想環境内部で完結します。
4. 機能をシンプルに保っているため、トラブルに遭遇する可能性が低いです。

**工夫ポイント**
- miniforgeの機能だけで完結させることで、機能性を犠牲にしてでもハマりポイントを最小化しています。（欲を出してpackage managerを使ったりしない）

## 使い方

### インストール

```zsh
% conda env create -f arm_ml_env_base.yml
```

※仮想環境名を変更して利用するときは、ymlファイルの`name`の仮想環境名をreplaceして使ってください。


### スクリプトを実行
まず仮想環境を`activate`します。

```zsh
% conda activate arm_ml_env_base
```

仮想環境をactivateするとコンソールの文頭に`(仮想環境名)`が付きます。この状態になっていれば仮想環境の依存性を利用することができます。  
デモコードを実行して確認してみましょう。

```zsh
% pyhton -V
# 3.10.4
% python demo/numpy_demo.py
# [1 2 3 4 5 6]
# <class 'numpy.ndarray'>
```

### packageを追加

```zsh
% conda install numpy
% conda env export | grep -v "^prefix: " > arm_ml_env_base.yml
```

## conda (Miniforge) チートシート

独断と偏見でまとめたよく使う操作。

| ユースケース | コマンド |
| --- | --- |
| 仮想環境一覧を表示 | `conda info -e` |
| 仮想環境をactivate | `conda activate machine_learning` |
| インストールされたパッケージを確認 | `conda list` |
| 仮想環境を作成 | `conda create -n machine_learning python=3.10;` |
| activateした仮想環境に依存性をインストール(リポジトリ指定) | `conda install -c conda-forge scikit-learn -y` |
| activateした仮想環境に依存性をインストール | `conda install numpy |
| 仮想環境削除 | `conda remove -n arm_ml_env_base --all` |
| yamlファイルから仮想環境を作成 | `conda env create -f arm_ml_env_base.yml` |
| 仮想環境をymlファイルにexport(`prefix`を消去, 推奨) | `conda env export | grep -v "^prefix: " > arm_ml_env_base.yml` |
| 仮想環境をymlファイルにexport | `conda env export` |

**`conda install`のオプション引数について**

| 引数 | 詳細 |
| --- | --- |
| `-c` | 省略可. リポジトリ(`channel`)を指定. ex. `conda-forge`, `pytorch`, etc... <br>arm用のpackageは`-c conda-forge`から手に入れやすい.<br>miniforgeはarm対応を謳っているリポジトリであるため. |
| `-y` | 省略可. 途中でいろいろ聞かれる系の質問に全てyesで答える |

## 環境構築手順の記録

### condaでの環境構築〜yamlファイルとして仮想環境をエクスポート

```zsh
# 仮想環境を作成
% conda create -n arm_ml_env_base python=3.10;

# 機械学習系packageをインストール
% conda install -c conda-forge scikit-learn -y
% conda install -c conda-forge pandas -y
% conda install -c conda-forge jupyterlab -y
% conda install -c pytorch pytorch torchvision -y
% conda install numpy decorator attrs cython
% conda install llvmdev
% conda install cmake
% conda install tornado psutil xgboost cloudpickle pytest
% conda install -c conda-forge librosa -y
% conda install -c conda-forge opencv
% conda install -c conda-forge matplotlib 

# yamlに環境設定をexport
% conda env export | grep -v "^prefix: " > arm_ml_env_base.yml
```

## その他
m１ Macでのpython学習開始時に環境構築で詰まることが多かったので作成しました。

## 参考
- https://qiita.com/kujirahand/items/9bf1a1e7bd34bdb87da5
- https://qiita.com/junkor-1011/items/cd7c0e626aedc335011d
