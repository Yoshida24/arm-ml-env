# arm-ml-env
arm環境での機械学習環境。2022年4月版。  

**前提**
- conda 4.10.1 (from Miniforge)

**含まれるpackage**
- scikit-learn
- pandas
- jupyterlab
- pytorch
- numpy
- opencv
- cython
- and more...

## インストール

```zsh
% conda env create -f arm_ml_env_base.yml
% conda activate arm_ml_env_base
```

デモコードを実行

```zsh
% pyhton -V
# 3.10.4
% python demo/numpy_demo.py
```

## packageを追加

```zsh
% conda install numpy
% conda env export | grep -v "^prefix: " > arm_ml_env_base.yml
```

## conda (Miniforge) チートシート

仮想環境一覧を表示

```zsh
% conda info -e  
```

仮想環境をactivate

```zsh
% conda activate machine_learning
```

インストールされたパッケージを確認

```zsh
% conda list
```

仮想環境作成

```zsh
% conda create -n machine_learning python=3.10;
```

activateした仮想環境に依存性をインストール（複数）

```zsh
% conda install numpy decorator attrs cython
% conda install -c conda-forge scikit-learn -y
```

- `-c`: 省略可. リポジトリ(`channel`)を指定. ex. `conda-forge`, `pytorch`, etc...

仮想環境削除

```zsh
% conda remove -n arm_ml_env_base --all
```

yamlファイルから仮想環境を作成

```zsh
% conda env create -f arm_ml_env_base.yml
```

仮想環境の依存packageをymlとしてexport

```zsh
# 推奨コマンド.（不要なローカルのファイルパスを消去する）
% conda env export | grep -v "^prefix: " > arm_ml_env_base.yml

# 単にexport
% conda env export
```

## 環境構築手順の記録

### condaでの環境構築〜yamlファイルとして仮想環境をエクスポート

```zsh
# 仮想環境を作成
% conda create -n machine_learning python=3.10;

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

# yamlに環境設定をexport
% conda env export | grep -v "^prefix: " > arm_ml_env_base.yml
```

## 参考
- https://qiita.com/kujirahand/items/9bf1a1e7bd34bdb87da5
- https://qiita.com/junkor-1011/items/cd7c0e626aedc335011d
