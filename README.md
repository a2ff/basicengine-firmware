## 豊四季タイニーBASIC for Arduino STM32 V0.8(2017/04/29)
※V0.8はまだテスト不十分です。下記より以前のバージョンV0.7を使って下さい。  
https://github.com/Tamakichi/ttbasic_arduino/releases  

![サンプル画像](./image/03.jpg)

NTSC・PS/2キーボード対応ブランチ版  
(ドキュメント修正中）  

本プログラムは、下記オリジナル版をArduino STM32向けに移植・機能版です.  
STM32F103C8T6搭載のBlue Pillボード、Black Pillボードでの動作を確認しています.  
※機能の大幅追加のため、Arduino MEGEは非対応となりました.  
※NTSCビデオ出力対応のため、ターミナル画面制御は非対応にしました(2017/04/13)  

- オリジナル版配布サイト  
 https://github.com/vintagechips/ttbasic_arduino  
 関連情報 [電脳伝説 Vintagechips - 豊四季タイニーBASIC確定版](https://vintagechips.wordpress.com/2015/12/06/%E8%B1%8A%E5%9B%9B%E5%AD%A3%E3%82%BF%E3%82%A4%E3%83%8B%E3%83%BCbasic%E7%A2%BA%E5%AE%9A%E7%89%88/)

**「豊四季タイニーBASIC」**の著作権は開発者**のTetsuya Suzuki**氏にあります.  
プログラム利用については、オリジナル版の著作権者の配布条件に従うものとします.  
著作権者の同意なしに経済的な利益を得てはいけません.  
この条件のもとで、利用、複写、改編、再配布を認めます.  

Blue Pillボード利用構成図  
![構成図](./image/02.png)

- **利用可能市販パーツ**  
  - PS/2キーボード用コネクタ  
  aitendo PS/2モジュール [ML-PS2-4P] http://www.aitendo.com/product/11377  
  秋月電子 USBコネクタDIP化キット(Aメス) http://akizukidenshi.com/catalog/g/gK-07429/  
  - NTSC用 RCAコネクタ  
  aitendo TVOUTモジュールキット [K-TVOUT2R] http://www.aitendo.com/product/11740  
  aitendo RCAモジュールキット [brebo.jam.rca] http://www.aitendo.com/product/12125  
  秋月電子 RCAジャックDIP化キット(黄) http://akizukidenshi.com/catalog/g/gK-06522/  
  ※aitendo製品は付属抵抗を使うと若干出力電圧が上がりますが、許容範囲です。そのまま利用できます。  


![ピン割り付け](./image/03_1.png)

**修正内容**
- ラインエディタ部の差し換え  
 オリジナルのラインエディタ部分をフルスリーンテキストエディタに差し換えました.  
 昔のBASICっぽい編集操作を出来るようにしました.  

- コマンドの追加  
  - **RENUM** ：行番号再割り当て  
  - **CLS** ：画面クリア  
  - **LOCATE**：カーソル移動    
  - **WAIT**：時間待ち  
  - **VPEEK**：スクリーン位置の文字コード参照  
  - **CHR$()**、**HEX$()**、**BIN$()**、**ASC()**、**INKEY()** 関数の追加  
  - **TICK()** 関数、**RESETTIK**の追加  
  - **?**：**PRINT**文の省略系を追加  
  - **GPIO**、**OUT**、**IN**、**ANA**、**POUT**,**SHIFTOUT**、**SHIFTIN** 、**PWM**：GPIO利用コマンドの追加  
  - **I2CW**、**I2CR**：I2C利用コマンドの追加  
  - **POKE**、**PEEK**：メモリ領域参照コマンドの追加  
  - **DATE**、**SETDATE**、**GETTIME**: 内蔵RTC利用コマンド追加  
  - **SAVE**、**LOAD**： 内部フラッシュメモリへのプログラム保存機能の追加  
  - **EEPFORMAT**,**EEPWRITE**,**EEPREAD**コマンドの追加(仮想EEPROM機能)  
  - **AND**、**OR**、!、~、!の追加  
  - **PSET**,**LINE**,**RECT**,**CIRCLE**,**GPRINT**のグラフィック描画コマンド追加  
  - **SMODE**,**SOPEN**,**SCLOSE**,**SERITE**,**SREAD**,**SREADY**,**SPRINT**のシリアル通信コマンドの追加  
  - **BITMAP**,**CSCROLL**,**GSCROLL**,コマンドの追加  
  - **DELETE**,**EXPORT**,**CONFIG**,**SAVECONFIG**,**LRUN**の追加  
  - **MAP()**,**DMP$()**の追加
- 文法の変更  
  - 定数の16進数表記対応(例 $1234,$AB)  
  - 命令文区切りを';'から':'に変更  
  - **PRINT**文の行継続を';'でも可能に変更  
  - **PRINT**文の数値桁指定#nのnにマイナス値指定時、空白ではなく0埋め出来るように追加  
  - **IF**文の不一致判定を"!="でも可能に変更、ELSE文対応    
  - 演算子 剰余計算'%'、シフト演算子 '>>'、'<<'を追加  
  - AND・OR・NOT、ビットOR'|'、ビットAND'&'ビット反転~、XOR'^'を追加  
  - **STOP**命令を**END**に変更    
  - **SIZE**を**FREE**に変更  
  - 文字列囲みにシングルクォーテーションを利用出来ないように変更  
  - コメントをシングルクォーテーション(')での記述出来るように修正  
  - 配列の連続値設定を可能した(例: @(0)=1,2,3,4,5)    
  - GOTO,GOSUBをラベル対応(例: GOTO "ラベル" ダブルクォーテーション囲み)  
  - INPUT文の入力改善、オーバーフローエラー回避対策追加    
- 編集機能の変更  
  - 実行中プログラムの中断を**[ESC]**を2回押し、**[CTRL-C]**に変更  
- その他  
  - プログラム領域を4096バイトに拡大  
  - プログラム保存数を10個に拡大  
  - 配列サイズを32から100に拡大  
  - エラーメッセージ**Illegal value**の追加  
  - エラーメッセージ**Out of range value**の追加  
  - エラーメッセージ**Program not found**の追加  
  - 定数:HIGH、LOW、PA00、PA01、..、PC15のピン名の追加  

**※本スケッチの利用には別途、下記のライブラリが必要です.**  
 - Arduino STM32 内部フラッシュメモリ書き込みライブラリ  
   https://github.com/Tamakichi/ArduinoSTM32_TFlash  
 - Arduino STM32 NTSCビデオ出力ラブラリ(最新版)  
   https://github.com/Tamakichi/ArduinoSTM32_TNTSC  
 - Arduino STM32 TVoutライブラリ(最新版)  
   https://github.com/Tamakichi/ArduinoSTM32_TVout    
 - Arduino STM32用 PS/2 キーボードライブラリ(最新版)  
   https://github.com/Tamakichi/ArduinoSTM32_PS2Keyboard      

## フルスリーンテキストエディタの機能
※利用にはNTSC対応のTVモニターデスプレイが必要です.  

※現状、利用しているNTSC対応のモニターデスプレイとの相性問題が発生しています.  
　TNTSCビデオ出力ライブラリの下記の設定を調整することで改善できる場合があります.  
　TNTSC/src/TNTSC.cpp の57行近辺の下記の設定を変更して下さい.  

  `#define NTSC_LINE (262+2)  // 画面構成走査線数(一部のモニタ対応用に2本に追加)`  
　を  
  `#define NTSC_LINE (262+0)`  
  `#define NTSC_LINE (262+1)`  
  `#define NTSC_LINE (262+2)`  
  の何れかにして修正して映りが改善する設定にする.  

**スクリーンサイス**  
224ｘ216ドット  
6x8ドットフォント利用時 37x27文字  
8x8ドットフォント利用時 28x27文字  

**利用可能キー**  
- [←][→][↑][↓] ： カーソル移動 カーソルキー  
- [Delete]、[CTRL-X] ：カーソル位置の文字削除  
- [BackSpace]：カーソル前の文字削除と前に移動  
- [PageUP]、[PageDown]：カーソルを画面の上端、下端に移動  
- [F5]、[CTRL-R]：画面の再表示  
- [HOME]、[END]：行内でカーソルを左端、右端に移動  
- [INS]：挿入・上書きのトグル切り替え  
- [Enter]：行入力確定  
- [ESC]、[CTRL-C]：実行プログラムの中断
- [F1]、[CTRL-L]：画面のクリア

## 追加・修正コマンドの説明
[リファレンスマニュアル(nmanual.pdf)](./manual.pdf)に記載しています(ただし追加・修正中)  
(リンクを直接クリックして閲覧すると表示が遅いです。ダウンロードして閲覧して下さい)  

## サンプルプログラム
### ボード上のLEDの点滅  
```
10 P=PC13
20 GPIO P,OUTPUT
30 OUT P,HIGH
40 FOR I=1 TO 10
50 OUT P,LOW
60 WAIT 300
70 OUT P,HIGH
80 WAIT 300
90 NEXT I
```

### アナログ値表示
```
10 CLS
20 GPIO PB01,ANALOG
30 A=ANA(PB01)
40 LOCATE 5,5: ? A; "     "
50 GOTO 30
```
### 配列の連続設定
```
10 @(1)=1,2,3,4,5,6,7,8
20 FOR I=1 TO 8
30 ? "@(";I;")=";@(I)
40 NEXT I
```

### シフト演算
```
10 A=1
20 FOR I=0 TO 16
30 ? HEX$(A<<I,4)
40 NEXT I
```

### ラベルの利用
```
100 GOSUB "SUB01"
110 GOSUB "SUB02"
120 N=0
130 "LOOP"
140 PRINT "N=";N
150 N=N+1:IF N<5 GOTO "LOOP"
160 END
170 "SUB01"
180 PRINT "SUB01"
190 RETURN
200 "SUB02"
210 PRINT "SUB02"
220 RETURN
```

## 以降はオリジナルのドキュメントです



TOYOSHIKI Tiny BASIC for Arduino

The code tested in Arduino Uno R3.<br>
Use UART terminal, or temporarily use Arduino IDE serial monitor.

Operation example

&gt; list<br>
10 FOR I=2 TO -2 STEP -1; GOSUB 100; NEXT I<br>
20 STOP<br>
100 REM Subroutine<br>
110 PRINT ABS(I); RETURN

OK<br>
&gt;run<br>
2<br>
1<br>
0<br>
1<br>
2

OK<br>
&gt;

The grammar is the same as<br>
PALO ALTO TinyBASIC by Li-Chen Wang<br>
Except 3 point to show below.

(1)The contracted form of the description is invalid.

(2)Force abort key<br>
PALO ALTO TinyBASIC -> [Ctrl]+[C]<br>
TOYOSHIKI TinyBASIC -> [ESC]<br>
NOTE: Probably, there is no input means in serial monitor.

(3)Other some beyond my expectations.

(C)2012 Tetsuya Suzuki<br>
GNU General Public License
