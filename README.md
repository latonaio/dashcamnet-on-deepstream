# dashcamnet-on-deepstream
dashcamnet-on-deepstream は、DeepStream 上で DashCamNet の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- DashCamNet
- Docker
- TensorRT Runtime

## DashCamNetについて
DashCamNet は、移動カメラから画像内の車、人、道路標識、および二輪車を検出し、カテゴリラベルを返すAIモデルです。
DashCamNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、DashCamNet の Dockerコンテナ を起動します。
```
docker-run: 
	docker-compose -f docker-compose.yaml up -d
```
### ストリーミングの開始
Makefile に記載された以下のコマンドにより、DeepStream 上の DashCamNet でストリーミングを開始します。  
```
stream-start:
	xhost +
	docker exec -it deepstream-dashcamnet deepstream-app -c /app/src/deepstream_app_source1_dashcamnet.txt
```
## 相互依存関係にあるマイクロサービス  
本マイクロサービスを実行するために DashCamNet の AIモデルを最適化する手順は、[dashcamnet-on-tao-toolkit](https://github.com/latonaio/dashcamnet-on-tao-toolkit)を参照してください。  


## engineファイルについて
engineファイルである dashcamnet.engine は、[dashcamnet-on-tao-toolkit](https://github.com/latonaio/dashcamnet-on-tao-toolkit)と共通のファイルであり、当該レポジトリで作成した engineファイルを、本リポジトリで使用しています。  

## 演算について
本レポジトリでは、ニューラルネットワークのモデルにおいて、演算スループット効率を高めるため、FP16(半精度浮動小数点)を使用しています。  