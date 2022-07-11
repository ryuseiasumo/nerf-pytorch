# nerf-pytorch with singularity

Pytorchで作成されたNeRF __[nerf-pytorch](https://github.com/krrish94/nerf-pytorch)__ をSingularity環境で実行するために、自分用に作成しました。
コードの内容自体は __[nerf-pytorch](https://github.com/krrish94/nerf-pytorch)__ をそのまま利用していますので、そちらを参考にしてください。

# Requirement
* CUDA v11.x
* singularity-ce version 3.9.0

# Quickstart
```bash
# singularityイメージの作成
$ git clone https://github.com/ryuseiasumo/nerf-pytorch
$ cd nerf-pytorch/
$ singularity build --fakeroot pytorch.sif ./def_files/pytorch.def
```


```bash
# データのダウンロードと展開 
## nerf-pytorch/ 以下で、下記を実行
$ mkdir cache
$ cd cache/
$ wget http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/ECCV20/nerf/nerf_example_data.zip
$ unzip nerf_example_data.zip
$ cd ../
```



```bash
# 実行
## nerf-pytorch/ 以下で、下記を実行
$ singularity shell --nv pytorch.sif


## 学習を行う場合
$ python train_nerf.py --config config/lego.yml

## チェックポイントからの学習を行う場合
$ python train_nerf.py --config config/lego.yml --load-checkpoint path/to/checkpoint.ckpt

## 事前学習済みモデル(pretraind model)を用いて、シーンのレンダリングをする場合
$ python eval_nerf.py --config pretrained/lego-lowres/config.yml --checkpoint pretrained/lego-lowres/checkpoint199999.ckpt --savedir cache/rendered/lego-lowres
```


[Imagemagick](https://imagemagick.org/)を用いた`gif`への変換.
```bash
$ convert cache/rendered/lego-lowres/*.png cache/rendered/lego-lowres.gif
```

This should give you a gif like this.

<p align="center">
    <img src="assets/lego-lowres.gif">
</p>





# Note
* singularityが利用できない場合は、requirements.txtを参考にして環境構築をしてみてください。

* __[nerf-pytorch](https://github.com/krrish94/nerf-pytorch)__ のrequirementsから、openvの部分だけ変更しています(condaに変更)。

* singularityイメージのビルドの際に、imagemagickの部分で居住地などを選択が必要になります。



# Sample results from the repo
### On synthetic data

<p align="center"> 
    <img src="assets/blender-lowres.gif">
</p>

### On real data

<p align="center"> 
    <img src="assets/fern-lowres.gif">
</p>




# LICENSE

`nerf-pytorch` is available under the [MIT License](https://opensource.org/licenses/MIT). For more details see: [LICENSE](LICENSE) and [ACKNOWLEDGEMENTS](ACKNOWLEDGEMENTS).
