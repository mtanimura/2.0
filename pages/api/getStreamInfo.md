---
title: getStreamInfo
keywords: api
sidebar: api_sidebar
permalink: getStreamInfo.html
folder: api
toc: false
---

ストリームに関して詳細情報を返します





## API パラメータ

| パラメータ名  |  タイプ | 必須かどうか | デフォルト値 | 説明 |
| :----------------: | :-----: | :-------: | :------------------: | ---------------------------------------- |
|         id         | 整数値 |   true    |        *null*        | ストリームの**configID** 通常`listStreamsIDs`の返り値 このパラメータは必須ではなく、本パラメータ若しくは`localStreamName`のどちらかがストリーム特定のために必要です |
|  localStreamName   | 文字列  |   true    | *zero length string* | ストリーム名。このパラメータは必須ではなく、本パラメータ若しくは`id`のどちらかがストリーム特定のために必要です |





## API Call テンプレート

```
getStreamInfo id=<configId>
```

または

```
getStreamInfo localStreamName=<localStreamName>
```



### サンプル API Call

```
getStreamInfo localStreamName=testpullStream
```



### JSONのSuccess Response

```
{
"data":{
"appName":"evostreamms",
"audio":{
"aveAudioBitRate":116810.8571,
"bytesCount":483506,
"codec":"AAAC",
"codecNumeric":4702111241970122752,
"currAudioBitRate":106814.8571,
"droppedBytesCount":0,
"droppedPacketsCount":0,
"packetsCount":1483
},
"bandwidth":0,
"connectionType":1,
"creationTimestamp":1508501495963.5352,
"farIp":"204.246.165.114",
"farPort":1935,
"ip":"192.168.2.123",
"name":"testpullStream",
"nearIp":"192.168.2.123",
"nearPort":48754,
"outStreamsUniqueIds":null,
"pageUrl":"",
"port":48754,
"processId":58043,
"processType":"origin",
"pullSettings":{
"_callback":null,
"audioCodecBytes":"",
"configId":1,
"emulateUserAgent":"EvoStream Media Server (www.evostream.com) player",
"forceTcp":false,
"httpProxy":"",
"httpStreamType":"ts",
"isAudio":true,
"keepAlive":true,
"localStreamName":"testpullStream",
"operationType":1,
"pageUrl":"",
"ppsBytes":"",
"rangeEnd":-1,
"rangeStart":-2,
"rtcpDetectionInterval":10,
"saveToConfig":true,
"sendDummyPayload":false,
"sendRenewStream":false,
"spsBytes":"",
"ssmIp":"",
"swfUrl":"",
"tcUrl":"",
"tos":256,
"ttl":256,
"uri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
"videoSourceIndex":"high"
},
"queryTimestamp":1508501526607.2568,
"serverAgent":"FMS\/3,5,7,7009",
"swfUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
"tcUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
"type":"INR",
"typeNumeric":5282249572905648128,
"uniqueId":28,
"upTime":30643.7217,
"video":{
"aveFrameRate":24.9643,
"aveKeyFramesPerSec":0.4643,
"aveVideoBitRate":925772.8571,
"bytesCount":4081575,
"codec":"VH264",
"codecNumeric":6217274493967007744,
"currFrameRate":23.0000,
"currKeyFramesPerSec":0.4286,
"currVideoBitRate":1096873.1429,
"droppedBytesCount":0,
"droppedPacketsCount":0,
"height":306,
"level":30,
"packetsCount":827,
"profile":66,
"width":720
}
},
"description":"Stream information",
"status":"SUCCESS"
}
```



#### JSON Response

JSON responseは以下を含みます:

- data – パースすべきデータ
  - appName - serviceを利用するアプリケーション名
  - audio – ストリームのオーディオ部分の統計情報
    - aveAudioBitRate - ストリームの先頭からのオーディオフレームの平均ビットレート
    - bytesCount - 受信したオーディオデータ総量
    - codec - オーディオcodec名
    - codecNumeric - 内部使用コード
    - currAudioBitRate - コマンドコール時点で最後のオーディオフレームのビットレート
    - droppedBytesCount - ロストしたビデオバイト数
    - droppedPacketsCount – ロストオーディオパケット数
    - packetsCount – 受信オーディオパケット総数
  - bandwidth – ストリームの現在の使用帯域
  - connectionType - 1=pull, 2=push, 3=HLS, 4=HDS, 5=MSS, 6=DASH, 7=record, 8=launchprocess, 9=webrtc, 10=metadata, 0=standard
  - creationTimestamp – ストリーム生成時点のUNIXタイムスタンプ。UNIXタイムはUNIXエポック(1970年1月1日)からの秒数です
  - farIp - far側のIPアドレス
  - farPort - far側の使用ポート
  - ip - ソースストリームホストのIPアドレス
  - name – ストリームの`localStreamName`
  - nearIp - ローカルコンピューターで使用されるIPアドレス
  - nearPort - ローカルコンピューターで使用されるポート
  - outStreamsUniqueIDs – *プルしたストリーム* inストリームに関連するoutストリームIDの配列
  - pageUrl - リクエスト元のページへのリンク
  - port - serviceにバインドされたポート
  - processID - APIコマンドを処理するEMSインスタンスのプロセスID
  - processType - APIコマンドを処理するEMSインスタンスにより、Origin または edge
  - pullSettings/pushSettings – 外部プレーヤー／クライエントによりリクエストされたストリームには無い。`pullStream` または `pushStream`コマンドで使用されたパラメータ
    - _callback -lazy pullでは必須。内部使用のみ
    - audioCodecBytes - オーディオの場合のRTPストリームのオーディオcodec設定
    - configId – pullPushConfig.xmlエントリでのid
  - emulateUserAgent – EMSが他のサーバーと自身を区別するために使用する文字列。EMSが自身をFlash Media Serverと指定する等に使用可能です
    - forceTcp – TCPを強制するかどうか
    - httpProxy - IP:Portの組み合わせまたはself
    - isAudio - 現在プルされているストリームがオーディオソースかどうかを示す
    - keepAlive – trueの場合、接続が切断した際ストリームは再接続を試みます
    - localStreamName – ストリームの`localStreamName`
    - operationType – オペレーションタイプ
    - pageUrl – リクエスト元のページへのリンク
    - ppsBytes - ビデオの場合RTPストリームのvideo PPSバイト
    - rangeEnd - 再生する長さ(秒)
    - rangeStart - 再生開始点（秒）
    - rtcpDetectionInterval – RTSPで使用され、RTSP/RTPストリームのためのRTCP接続ができるかどうか判定するEMSの待ち時間(RTSPはオーディオとビデオの同期に使用されます)
    - sendRenewStream - 1の場合、新規クライエント接続時にサーバーはSET_PARAMETERでRenewSTreamを送ります
    - spsBytes - ビデオの場合RTPストリームのビデオSPSバイト
    - swfUrl – ストリームを生成するFlashクライエントの場所
    - tcUrl – RTMPパラメータの一種、実質的にはURIのコピー
    - tos – Type of Serviceネットワークフラグ
    - ttl – Time To Liveネットワークフラグ
    - uri – ソースストリームURIのパースされた値
  - queryTimestamp – リクエストによる情報が投入された時間のタイムスタンプ(UNIX時間)
  - serverAgent - 使用されたサーバーエージェント
  - swfUrl - ストリームを生成するFlashクライエントのロケーション
  - tcUrl - RTMPパラメータの一種、実質的にはURIのコピー
  - type – ストリームタイプ。重要な情報は最初の２文字:
    - char 1 = インバウンドはI、アウトバウンドは O
    - char 2 = ネットワークはN、 ファイルはF
    - char 3+ = ストリームに関する詳細情報
    - 例: INR = Inbound Network Stream (ネットワークからEMSに入ってくるストリーム)
  - typeNumeric - ストリームタイプ文字に0で埋めて8バイトにした配列から得られる数値
  - uniqueId – ストリームのuniqueID(整数値)
  - upTime – ストリームがaliveかつ実行中の期間(秒数)
  - video – ストリームのビデオ部分の統計情報
    - aveFrameRate- ストリーム開始からの平均フレームレート
    - aveKeyFramesPerSec - ストリーム開始からの平均毎秒キーフレーム
    - aveVideoBitRate -  ストリーム開始からのビデオフレームの平均ビットレート
    - bytesCount - 受信ビデオデータ総量
    - codec - ビデオcodec名
    - codecNumeric - 内部使用コード
    - currFrameRate - 秒あたりで処理されているビデオフレーム数
    - currKeyFramesPerSec - 秒あたりで処理されるビデオキーフレーム数
    - currVideoBitRate - コマンドコール時点の最後のビデオフレームのビットレート
    - droppedBytesCount – ロストしたビデオバイト数
    - droppedPacketsCount – ロストしたビデオパケット数
    - height - ビデオストリームの縦ピクセル数
    - level - H264レベル
    - packetsCount – ビデオパケット受信総数
    - profile - H264プロファイル
    - width - ビデオストリームの横ピクセル数

- description– コマンドのパース・実行結果
- status – コマンドがパースされ正常実行された場合は**SUCCESS** そうでなければ**FAIL**

------

## 関連リンク

- [getStreamsCount](getStreamsCount.html)