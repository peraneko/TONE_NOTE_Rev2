
# ファームウエアの書き込み
### ファームウエアとはなにか
TONEでは、キー入力をPCに渡すために、QMKファームウエアを利用しています。  
QMKファームウエアは、先程とりつけたProMicroにこれから書き込まれ、キーの入力をPCで認識できる入力形式に変換して、PCに送る動作を行います。    

### TONEの動作確認をする
まずは物理的にキーが動作しているか確認するためのファームウエアで、ハンダ付けがうまく行っているかを確認しましょう。  

テスト用のファームウエアはこちらに用意してあります。  
[tone_test.hex](https://github.com/peraneko/TONE/blob/master/TONE_HEX/tone_test.hex)  
tone_test.hexをダウンロードして、わかりやすい場所に置いておきます。  

ファームウエアの書き込みについては、QMK Toolboxを利用します。
[QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)  のダウンロード画面で、自分の使っているOSにあわせてダウンロードするファイルを選んでください。  
MAC OS/Windowsともに用意されています。  

QMK Toolboxを無事にダウンロードできたら、インストールして実行してください。  
このような画面が表示されます。この画面はWindows版のためMACを利用している方は、適宜読み替えてください。    

![QMKToolbox実行画面](https://user-images.githubusercontent.com/5952961/59032589-a45a3c00-88a1-11e9-94c2-eec1b0bca2c6.png)  
この画面の右上、MicroControllerのプルダウンがatmega32u4になっているか確認してください。  
問題がなければ、そのすぐ下にあるAuto-Flashのチェックボックスをクリックして、チェックを入れてください。  

左側のlocal fileを選択します。これは、書き込みたいファイルを指定するための動作です。
local fileの右側にあるOPENをクリックして、先程ダウンロードしておいた、TONE_test.hexを選択してください。  

選択したら、TONEのリセットスイッチを押します。
すると、自動的に書き込みが進んでいきます。  
書き込みが終わるとavrdude.exe done.  Thank you.と表示されます。

TONE_test.hexのキーマップは下記の通りです。  
~~~C
#include QMK_KEYBOARD_H

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    [0] = LAYOUT( 
        KC_A,       KC_B,      KC_C,     KC_D,
        KC_E,       KC_F,      KC_G,     KC_H
    )
};

/* Rotary encoder settings */
void encoder_update_user(uint16_t index, bool clockwise) {
   if (clockwise) {
        tap_code(KC_0);    //Rotary encoder clockwise
    } else {
        tap_code(KC_1);    //Rotary encoder Reverse clockwise
    }
}

~~~

上段の４キーが左からABCD  
下段の４キーが左からEFGH  
ロータリーエンコーダ時計回りが0  
反時計回りが1です。    

|-|左１|左２|左３|左４|  
|---|---|---|---|---|  
|上段|a|b|c|d|  
|下段|e|f|g|h| 
|ロータリーエンコーダ|時計回り|反時計回り|||  
|ロータリーエンコーダ|0|1|||  


すべてのキーとロータリーエンコーダは正常に動いていましたか？  
もし反応しないキーがあれば、ハンダ付けが正確に行われているか確認してください。  

それでは、実際にキーマップを変更して、マクロパッドとして使ってみましょう。  
このキーマップは、Adobe photoshop Lightroom Classicで快適に操作できるように設計されています。  

~~~C
#include QMK_KEYBOARD_H

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    [0] = LAYOUT( 
        C(S(KC_E)), S(KC_TAB),  KC_TAB,      KC_0,
        KC_LSFT,    C(KC_LEFT), C(KC_RIGHT), C(KC_Z)
    )
};

/* Rotary encoder settings */
void encoder_update_user(uint16_t index, bool clockwise) {
   if (clockwise) {
        tap_code(KC_UP);    //Rotary encoder clockwise
    } else {
        tap_code(KC_DOWN);  //Rotary encoder Reverse clockwise
    }
}

~~~
[tone_ALR.hex](https://github.com/peraneko/TONE/blob/master/TONE_HEX/tone_ALR.hex)  
tone_ALR.hexをダウンロードして、わかりやすい場所に置き、先程の手順でProMicroに書き込んでみましょう。

上段の４キーが左からCtrl+SHIFT+E（書き出し）　SHIFT+TAB　TAB　0    
下段の４キーが左からSHIFT　CTRL+←（前の画像）　CTRL＋→（次の画像） CTRL+Z（UNDO)  
ロータリーエンコーダ時計回りが↑
反時計回りが↓です。

わけわからないですね、表にします。  

|-|左１|左２|左３|左４|  
|---|---|---|---|---|  
|上段|Ctrl+SHIFT+E(書き出し)|SHIFT+TAB|TAB|0|  
|下段|SHIFT|CTRL+←(前の画像)|CTRL＋→(次の画像)|CTRL+Z(UNDO)| 
|ロータリーエンコーダ|時計回り|反時計回り|||  
|ロータリーエンコーダ|↑|↓|||  

ここまではできあいの設定ファイルを使って来ました。  
近い将来、あなたは自分でTONEの設定ファイルを作りたくなると思います。  

### キーの割当をカスタマイズする
この製品はQMKファームウエアによってキー役割を定義しています。  
そのため、QMKファームウエアの設定を変更することで、キーの割当を思い通りに設定できます。

実際の手順はこんな感じになります。  
下記ページよりQMKファームウェアを入手します。  
zipedのファイルをダウンロードする場合は、別途「lufa」というライブラリを必要とします。
そのため、git cloneを行うことを推奨します。

https://github.com/qmk/qmk_firmware/

QMKファームウエアのディレクトリは用意できたでしょうか。
Cドライブ直下に置いたことにして、説明を続けます。  
※gitに慣れている方はクローンの方が良いでしょう。

#### ビルド環境を作る
##### macOS
homebrewを使う手順を説明します。  

ターミナルを起動します。  
homebrewを使っていなかったらインストールしておきます。  
次に下記のコマンドをそれぞれ実行します  
- brew tap osx-cross/avr
- brew tap PX4/homebrew-px4
- brew update
- brew install avr-gcc@7
- brew install dfu-programmer
- brew install gcc-arm-none-eabi
- brew install avrdude

##### Windows
msys2を使う手順を説明します。  

[msys2](https://www.msys2.org/)のサイトから、自分が使っているWindowsに合わせたインストーラをダウンロード＆インストールします。   
32bit OSの時 : msys2-i686-xxxxxxx.exe   
64bit OSの時 : msys2-x86_64-xxxxxxxx.exe  
msys2を起動します  

ダウンロードしておいたQMKファームウェアのフォルダに移動します。  
qmk_firmwareのフォルダは、先程Cドライブ直下に置きました。  

cd /c/qmk_firmware/util/msys2_install.sh と入力して、実行します。  
インストールするパッケージを聞かれますので答えていきます。不明な質問であれば、全てYとしてください。  
終わったらmsys2を再起動します    

#### 設定ファイルのダウンロード   
QMKファームウエアのリポジトリには、まだTONEが取り込まれていません。  
そのため、わたしのGitHubからファイルを取得して、qmk_firmware-master\keyboardsに置く必要があります。  

ダウンロードするフォルダ  
https://github.com/peraneko/TONE_NOTE_Rev2/tree/master/tone_rev2  

ダウンロードしたファイルを置く場所  
qmk_firmware-master\keyboards

#### 設定ファイルのビルド
qmk_firmwareの第一階層で以下のようにします。  

make tone:default   
しばらく時間がかかるかもしれませんが、tone_default.hexというファイルが生成されます。
このファイルをQMK ToolBoxでProMicroに書き込めば、使用できます。

### キーマップのカスタマイズ
既存のキーマップをカスタマイズする際は、現在のキーマップをバックアップしましょう。  
どこか別のフォルダにいれて、keymap_org.cなどとリネームしておけば良いでしょう。  

qmk_firmwareの第一階層で`./util/new_keymap.sh` を使うと、下記の様に<keyboard>のdefaultキーマップをベースに指定の<user_name>で複製することができます。  
```:shell
./util/new_keymap.sh <keyboard> <user_name>
```
<keyboard>にはtoneが入ります。  
<user_name>には、バージョン名やどういう使い方を意図しているのかを入力すると便利です。    
![コマンドライン](https://user-images.githubusercontent.com/5952961/59074284-b5d52f80-8905-11e9-9fa1-2dc9dc96dfee.png)  
./util/new_keymap.shとtoneの間、toneとFPSの間には半角スペースを忘れずに入れてください。  

上記の操作でできたフォルダは、以後、<あなたのkeymap名>と呼びます。
<あなたのkeymap名>フォルダ内のkeymap.cを好みに合わせて編集してください。  

編集後のビルドコマンドは以下のようになります。  
make tone:<あなたのkeymap名>  

#### 注意　
ロータリーエンコーダを時計回り方向に回した場合に入力したいキーコードは、if（clockwise）内のtap_code()に書き込みます。
ロータリーエンコーダを反時計回りに回した場合に入力したいキーコードは、else句の下の行のtap_code()に書き込みます。
~~~C
const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    [0] = LAYOUT( 
        C(S(KC_E)), S(KC_TAB),  KC_TAB,      KC_0,
        KC_LSFT,    C(KC_LEFT), C(KC_RIGHT), C(KC_Z)
    )
};

/* Rotary encoder settings */
void encoder_update_user(uint16_t index, bool clockwise) {
   if (clockwise) {
        tap_code(KC_UP);    //Rotary encoder clockwise
    } else {
        tap_code(KC_DOWN);  //Rotary encoder Reverse clockwise
    }
}
~~~

ここまでの説明で、あなたの好みのキー配置（キーマップ）が設定できたかと思います。  
ハードウェアからミドルウエア（ファームウエア）まで、簡単なものばかりとはいえ網羅的にたどってこないと、ここまでたどり着けません。  
自作キーボードを作ることは、あなたがPCを使いこなせているかどうかの身近な試金石です。  

長旅お疲れ様でした。ぜひTONEをご愛用いただけますよう、お願い申し上げます。  

### 余談 QMKファームウエアについて詳しく知りたくなったら
[公式のリファレンス](https://docs.qmk.fm/#/)を読みましょう。  
とくにお世話になるのが、次のページです。  

[keycode](https://docs.qmk.fm/#/keycodes)    
設定したいキーのコードを調べるのに有用です。  

一部日本語特化したい場合は、keymap_jp.hをincludeするとはかどります。  
<あなたのkeymap名>フォルダ内のkeymap.cの17行目あたり。#include QMK_KEYBOARD_Hと書かれているつぎの行に、下記を追加してください。  
`#include "keymap_jp.h"`

[keymap_jp.h](https://github.com/qmk/qmk_firmware/blob/master/quantum/keymap_extras/keymap_jp.h)  
[【QMK】JPキーコードでキーマップを定義する](https://skyhigh-works.hatenablog.com/entry/2018/11/14/033242)  
