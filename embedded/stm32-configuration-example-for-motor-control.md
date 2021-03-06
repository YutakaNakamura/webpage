---
title: "PMSM制御のための設定例(STM32)"
metaTitle: "embedded"
metaDescription: "This is the meta description motor page"
---

# 概要
PMSMの制御を行う為には、相電流を検出する必要がある。電流検出の際には、PWMリプル除去性能や、回路トポロジーによる検出可能領域の観点から、PWMに同期したサンプリングが多く利用されている。

ここでは以下の条件のもと、電流検出の為のTIM及びADC設定例を紹介する。

## 動作条件
### 環境
- MotorDriverBoard : X-NUCLEO-IHM08M1 (3シャント電流検出)
- MCU : STM32G431 (NUCLEO-G431RB)
- Code Generator : CubeMX Version:5.4.0

### 仕様
- PWMキャリア周期 : 20kHz
- TIMカウントアップ周期 : 170MHz
- TIM周期 : 65535 Count/Rev

### ピン配置仕様
- PWM u相出力 : PA8
- PWM u相相補出力 : PA7
- PWM v相出力 : PA9
- PWM v相相補出力 : PB0
- PWM w相出力 : PA10
- PWM w相相補出力 : PB1
- PWM ADCトリガ出力 : PA11 
- ADC u相入力 : PA0
- ADC v相入力 : PC1
- ADC w相入力 : PC0 
- ADC DCLink入力 : PA1

# PWMとADCトリガタイミング
今回の構成例の概略図を次に示す。

![SystemOverview](picture/CurrentDetection3Shunt.svg)

この構成では、下アームがONの時に相電流がシャント抵抗を通過する。

この事を考慮し、電流検出可能領域は次のようになる。

![ADCtiming](picture/ADCTiming.svg)

また、これを電圧ベクトルとして表示したものが次の図である。

![Voltage](picture/NotDetectableArea.svg)

一辺の長さがDCLink電圧である$V_{dc}$の正六角形(出力可能範囲)に対して、内接する円は半径が $\frac{\sqrt{3}}{2} V_{dc}$ である。

空間ベクトル変調を利用し、過変調領域を使用しない場合には、この内接円にて電圧を制限する。
この制限により、電圧検出可能領域内に出力となるPWMは侵入せず、必ず下アームが導通した状態となる。

換言すれば、3シャント電流検出では、過変調領域を除いた領域で電流検出が可能である。

この電流検出可能領域で3相全てのアナログ値をサンプリングすることが重要であり、本説での目標となる。

# 供給クロックの確認

# TIM設定
次のように設定する。

<!-- 必要に応じてCubeMXの画像を追加する。 -->
<!-- ![TIMSetting](picture/timConfig1.png) -->

## TIM1 Mode and Configuration - Mode
- Channel1 : PWM Generation CH1 CH1N
- Channel2 : PWM Generation CH2 CH2N
- Channel3 : PWM Generation CH3 CH3N
- Channel4 : PWM Generation CH4

この設定により、CH1～CH3の出力ピンより相補PWMが出力される。
TIM4の設定は、ADCの動作トリガに利用する。

## TIM1 Mode and Configuration – Configuration – Parameter Setting
### Counter Setting
タイマの周期等を決定する、カウンタに関する設定項目である。
- Prescaler : 0
- Counter Period : "TODO"
- Counter Mode : Center Aligned mode 1
- Repetition Counter : 1

Prescalerはカウンタレジスタの値が足りない時に設定する。今回は0とする。

Counter PeriodはPWMの周期を設定する。(Counter Modeの設定により周期が変化する事に注意する。)今回は20kHzとするため、8499に設定する。このとき値の計算は、$\frac{20 \mathrm{k} \mathrm{[Hz]}}{170 \mathrm{M} \mathrm{[Hz]}} - 1$で求める。

Counter ModeはPWMキャリアの波形を設定する。のこぎり波又は三角波から設定できる。
Center Aligned mode 1の場合には、三角波となる。

Repetition Counterでは、Duty等のPWM設定を更新するタイミングを設定する。今回はPWMキャリアの山でのみDutyの更新をしたいため、1とする。
<!-- 必要に応じて、説明画像を追加する。 -->

### Trigger Output(TRGO) Parameters
外部へ出力するトリガ信号の設定項目の項目である。ここでは2つのトリガを設定する。
- Trigger Event Selection TRGO : Update Event
- Trigger Event Selection TRGO2 : Output Compare(OC4REF)

Trigger Event Selection TRGOではUpdate Eventを選択する。  
Trigger Event Selection TRGO2ではOutput Compare(OC4REF)を選択する。今回はこれをADCのトリガとして利用する。

### Break And Dead Time management - Output Configuration
- Dead Time : n

必要に応じてデッドタイムの設定をする。

### PWM Generation Channel 1 and 1N
- Mode : PWM mode 1

### PWM Generation Channel 2 and 2N
- Mode : PWM mode 1

### PWM Generation Channel 3 and 3N
- Mode : PWM mode 1

### PWM Generation Channel 4
- Mode : PWM mode 2

PWM modeによりPWMの極性を反転できる。普通はPWM mode 1を使用する。 
Channel 4では、ADCへのトリガ出力のために、反転出力のPWM mode 2を設定する。


# ADC設定
<!-- 必要に応じて、CubeMXの画像を追加する。 -->
<!-- ![ADCSetting](picture/noimage.svg) -->

## ADC1 Mode and Configuration - Mode
対応したピンのADCを有効化する。
- IN1 : IN1 Single-ended
- IN7 : IN7 Single-ended
- IN6 : IN6 Single-ended  
これらが電流検出に関するADCピンである。
- IN2 : IN2 Single-ended  
これはDCLink電圧の測定に関するADCピンである。

## ADC1 Mode and Configuration - Configuration - Parameter Settings

### ADC_Injected_ConversionMode
ここでは外部割り込みに対する設定をする。
- Enable Injected Conversions : Enable
- Number Of Conversions : 4
- External Trigger Source : Timer1 Trigger Out event 2
- External Trigger Conversion Edge : Trigger detection on the rising edge
- Rank 1 Channel : Channel 1
- Rank 1 Sampling Time : 12.5 Cycles
- Rank 2 Channel : Channel 7
- Rank 2 Sampling Time : 12.5 Cycles
- Rank 3 Channel : Channel 6
- Rank 3 Sampling Time : 12.5 Cycles
- Rank 4 Channel : Channel 2
- Rank 4 Sampling Time : 12.5 Cycles

Number Of Conversionsは、外部トリガにより駆動するチャンネル数を設定する。  
今回の設定"4"では、トリガ信号を検出した後に  
Rank1 -> Rank2 -> Rank3 -> Rank4  
と逐次的にAD変換する。

External Trigger Sourceは、外部トリガを選択する。  
今回はTIM1のTrigger Event Selection TRGO2をトリガとしたいため、Timer1 Trigger Out event 2とする。

Sampling Timeには、ADCの変換時間を設定する。今回は12.5Cyclesとした。  
ここはMCUやドライバ側の出力インピーダンスに依存して最低時間が変動する。  
そのため、MCUのデータシートにある制約を守りつつ、実験的に決定するのが良い。

## ADC1 Mode and Configuration - Configuration - NVIC Settings
ここではADCの変換完了時の割り込みについて設定する。
- ADC1 and ADC2 global interrupt : enable (チェック)  
この設定により、AD変換の完了時に割り込みを生成する。


## Links

