# PATACD for PC98FileSlot-IDE
@lpproj　さんが作成されたPATACD.SYSをPC98FileSlot-IDE用に改造したものです。


改造に当たって当方で気がついたATAPI規格上実装が不十分な箇所を修正を行っています。  
主にMMC5/6系で発生していた相性問題や起動できないソフトについて修正されていることを確認しています。  

## ■ 動作確認環境
#### PC-9821AP2＋PC98FileSlot-IDE 
SATAドライブについては、JM20330を使ったPATA->SATA変換ボード使って接続しています。  

## ■ PC98FileSlot-IDEついて
現在開発中の同人ハードウェアになります。  
PC-9801FA / PC-9821AP/2/3 に採用されていたファイルスロットにIDEを追加するボードです。  
PIO転送方式のATA(IDE)/ATAPI周辺機器を利用することができます。  
  
またドライブベイ金具にもなっており、  
3.5インチ１台とSlim TypeのCDROMをファイルスロット追加することが可能です。  

#### Hardware仕様
※後日詳細資料を作成

PIO方式 ATA/ATAPI 端子 x1  
[IO 0xCC0-0xCCE,0xDCC / 0xEC0-0xECE,FCCから選択、割り込みは使用しない]  
  
MMC準拠Audio入力端子  x1  
  
ステレオミニジャック  x1    

## ■ 動作確認
下記３つの確認しました。
1. MSCDEXの認識と各FunctionのTest  
   ・IOCTL input/output  
   ・Read Long  
   ・Play Audio  
   ・Stop Audio  
   ・Resume Audio  
   
2. 市販ゲームの動作確認   (KONAMI ポリスノーツ)
3. PC-FXGAを使ったゲームの起動と簡単な動作チェック   (HUDSON チームイノセント）

## ■ 動作確認済みドライブ

#### ●動作に問題が無かったドライブ  
##### PATAドライブ  
PIONNER    DVR-112D  
PLEXTOR    PX-760A  
PLEXTOR    PX-755A  
MITSUMI    CR-485GTE  
Lite-On    SHM-165H6S  
HITACHI    GMA-4020B  
RICOH      MP7200A  
PANASOIC   LF-D521  
PANASONIC  SW-9585-C  
MITSUMI    CRMC-FX240S  
NEC        AD-7173A  
MEDIATEK   IDE CD-ROM 3.2C  
BOSS-V     BOV-40B  

##### PATAドライブ (Slim)
HLDS       GCC-4243  
HLDS       CRN-8245B  
PIONNER    DVR-K16VAD  
NEC        CDR-2800A  
NEC        CD-2800D  
NEC        CD-2800E  
TEAC       CD-224E       ※CSELの極性が他社と逆です。  
TSST       TS-L462   
PHILIPS    SCB5265  

#### ●動作に問題は無いが、Audio出力が無いので音が出ないドライブ
##### PATAドライブ (Slim)
PHILIPS    SCB5265
##### SATAドライブ
Lite-On    DH-16D5S  
HLDS       GCC-H10N  
  
#### ●DATAの読み込みはOKだが、AudioCMD(Play Audio/Stop Audio)に非対応/エラーが出るドライブ  
##### PATAドライブ
NEC        AD-5200A  
##### PATAドライブ (Slim)
PANASONIC  UJ-845-B  (Slot-in Type)
##### SATAドライブ
LG      WH10LS30  
  
#### ●動作に問題があるドライブ  
##### PATAドライブ  
MEMOREX    CD-482E       ※Audio出力が他社より小さい+Play Audioが2秒ずれます
##### PATAドライブ (Slim)  
TSST        TS-L162 ※Play Audioで音が出る前にReadyを返します。そのため再生位置とずれが生じる場合があります。   
TSST        SN-124 ※Read10のデータが化ける場合があります。   
MATSUSHITA  UJA720 (IBM P/N 27L7359) ※IBM仕様？Read10がErrorになります。
HITACHI     CD-S200 (IBM P/N 27L4167) ※IBM仕様？Read10がErrorになります。
 
