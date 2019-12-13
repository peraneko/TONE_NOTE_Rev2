# TONEビルドガイド
## 組み立て手順
組立の前に、必ず同梱品の確認をおこなってください。  
また、組立にはキットに同梱されていないパーツや工具を使用します。  
かならず下記のページを読んでおいてください。  
[README.md](https://github.com/peraneko/TONE/blob/master/README.md)


### PCBの選択
本製品には、TONE（左手用）とNOTE（右手用）のPCBが１枚ずつ封入されています。
どちらか１枚を上、もう１枚を下（ボトムプレート）として使用します。
このビルドガイドでは、TONE（左手用）を上にした場合を想定して説明していきます。
※写真が旧Reｖです。随時差し替えますが、旧バージョンと配置はほぼ変わらないので、作業に支障はないと思います。

### PCBの観察
組み立て前にPCBをよく観察しましょう。  
表面　ロータリーエンコーダの丸と□の枠と、位置で把握してください。  
![表面](https://user-images.githubusercontent.com/5952961/70760444-f7e79e00-1d8c-11ea-9192-e38eabcd4244.jpg)

### ProMicroの組み立て
コンスルーとピンヘッダの識別を行います。
今回は、キーの裏にProMicroを実装するため、ピンヘッダは使用しません。  
また、コンスルーを使用することで、万一ProMicroが破損した場合でも交換可能になります。  

![ProMicro1](https://user-images.githubusercontent.com/5952961/59026138-aec00a00-8890-11e9-8fba-5ff7336ee15c.jpg)
上下に並んだパーツのうち、上がピンヘッダになります。こちらは今回使用しません。  
下側のパーツがコンスルーです。ピンの部分が金色で、細い針金を折ったものが使われています。  
今回は前述のような理由で、コンスルーを使用します。  

![ProMicro1](https://user-images.githubusercontent.com/5952961/59015614-5b42c180-887a-11e9-92bd-fa32baa3fef1.JPG)
ProMicroの部品が実装されている面にコンスルーを差し込みます。  
コンスルーの小さな小窓がProMicroに近い側であること、手前奥ともに小窓が見えていることを確認したらひっくり返します。  
![ProMicro2](https://user-images.githubusercontent.com/5952961/59015616-5da51b80-887a-11e9-8408-a7d9d0e1b51e.JPG)
ProMicroとコンスルーをはんだ付けします。コテ先が差込やすいように、ProMicroを少し斜めに置くとやりやすいでしょう。  
![ProMicro3](https://user-images.githubusercontent.com/5952961/59015626-63026600-887a-11e9-8832-33c9d1f8476a.JPG)

### キースイッチの取り付け
PCB表面からキースイッチを差し込んでいきます。
![キースイッチ取り付け](https://user-images.githubusercontent.com/5952961/59015641-6ac20a80-887a-11e9-9752-d6244277618a.JPG)
8キーすべて差し込んだら、裏返します。   
![キースイッチ取り付け](https://user-images.githubusercontent.com/5952961/59015653-70b7eb80-887a-11e9-9d5d-cd56120fc6c0.JPG)
裏返したら、ProMicroと干渉するピンを切り取ります。  
干渉するのはこの五ヶ所です。
![キースイッチ取り付け](https://user-images.githubusercontent.com/5952961/59020329-b8dc0b80-8884-11e9-8480-6e56f675e81a.JPG)
切り取る長さはこのくらいです。  
  
切り取ったらはんだ付けします。  
こちらはハンダ付けが終わった状態。
![キースイッチ取り付け](https://user-images.githubusercontent.com/5952961/59020654-65b68880-8885-11e9-8d23-21b04b8de230.JPG)

### ロータリーエンコーダの取り付け
ロータリーエンコーダも表面から差し込んで、裏面でハンダ付けします。  
3本縦に並んでいる表側から見て右のピンが信号用です。のこりの上下2本の爪は固定用です。  
固定用の爪には、少し多めにハンダを送ることになるでしょう。
ハンダ付けが終わった状態はこんな感じです。  
![ロータリエンコーダ取り付け](https://user-images.githubusercontent.com/5952961/59020673-723ae100-8885-11e9-8aa4-36966ac36e32.JPG)

### リセットスイッチの取り付け
裏面からリセットスイッチをとりつけます。  
![リセットスイッチ](https://user-images.githubusercontent.com/5952961/59015608-5716a400-887a-11e9-9d98-709e4c4d751c.JPG)
   
表面側からハンダ付けします。
![リセットスイッチ表](https://user-images.githubusercontent.com/5952961/59015611-58e06780-887a-11e9-8a01-9fee2a655bb4.JPG)
リセットスイッチの足がくの字になっていますが、根本と穴がハンダ付けできていれば大丈夫です。
  
![リセットスイッチ表](https://user-images.githubusercontent.com/5952961/59017786-62b89980-887f-11e9-8f38-b8d8dbdde931.JPG)
完成後の写真ですがこうなってればOK  

### ProMicroの取り付け
ProMicroとTONEのPCBははんだ付けせずに取り付けをおこないます。
![ProMicro取り付け](https://user-images.githubusercontent.com/5952961/59020707-81219380-8885-11e9-8cc4-b973c33fbd1f.JPG)
根本まで確実に差し込んでください。  
※ここでハンダ付けをしないのは、ProMicroが破損した場合に交換を容易にするためです。  
　悲しい先例を見たい場合は、mogeMicroで検索してみてください。

### 状況の確認
これで青基板に取り付けるスイッチやProMicroは全て取り付けられているはずです。
![表側確認](https://user-images.githubusercontent.com/5952961/59021803-8384ed00-8887-11e9-8c29-98c3eab786f6.JPG)
![裏側確認](https://user-images.githubusercontent.com/5952961/59021802-82ec5680-8887-11e9-87a6-f2d4aa6b91b1.JPG)


### ボトムプレートの取り付け
ボトムプレート（今回は黒基板）にスペーサーを裏側からねじで固定します。  
固定する位置は写真を参照してください。
![ボトムプレート](https://user-images.githubusercontent.com/5952961/59021917-b6c77c00-8887-11e9-950d-73b358a59654.JPG)
その後、裏返してゴム足をよろしい感じに貼り付けてください。
![ボトムプレート](https://user-images.githubusercontent.com/5952961/59021806-841d8380-8887-11e9-89a5-42de7fa717fd.JPG)
もう一度うらがえしたら、PERANEKO FACTORYのロゴを上下であわせて、ネジ止めします。
![ボトムプレート](https://user-images.githubusercontent.com/5952961/59022694-373aac80-8889-11e9-851d-57cdd7346c10.JPG)

### キーキャップとロータリーエンコーダノブの取り付け
好みのものを取り付けてください。  
キーキャップ（特にDSA)は取り付け時に向きを確認する必要があります。  
![艤装](https://user-images.githubusercontent.com/5952961/59022693-373aac80-8889-11e9-88bb-a40b8aa7cdff.JPG)
ロータリーエンコーダのノブについては、マイナスドライバーでしめつけることになります。
今回使用しているロータリーエンコーダは軸に平たい面がありますので、そこにねじが垂直に当たるように締めると、収まりが良くなります。

## おつかれさまでした
これにて、物理的にはTONEが完成です。  
さあ、次のステップ、ファームウエアの書き込みに進みましょう。  
  
[ファームウエアの書き込み](TONE_QMK_firmware.md)
