# Graphical representation of causal effects

## 6.0 Introduction

* Causal inferenceには，因果パスについての専門知識と検証不可能な仮定が必要
  * これまでは，シンプルな設定におけるCausal effectを計算するための条件や方法に焦点をあててきた
* 興味のある因果構造についての専門知識や仮定を質的に表現するGraphical toolを導入する
* 知識や仮定を直感的にまとめることにより，Graphは研究者間のコミュニケーションを強化する

## 6.1 Causal representation of causal effects

* Graph \(causal diagram\)は因果的な概念を表す

![](.gitbook/assets/sukurnshotto-2020-06-05-113819png.png)

* Graphはnodeとedgesで構成される（Figure 6.1）
  * nodeは確率変数（L, A, Y）
  * edgeは矢印
  * 時間は左から右に流れる
    * LはAとYより時間的に先行
    * AはYより時間的に先行
  * Lは疾病の重症度，Aは心移植，Yは死亡を表す
* VからWへ矢印があることは，少なくとも一人において，direct causal effectがあることを示す
  * 他の変数で媒介（mediate）されていない
* VからWへ矢印がないことは，集団内で誰一人，direct causal effectがないことを示す
* causal diagramでは，矢印が不利益（害）であるか，利益（保護）であるかは区別できない
* Yの2つの原因であるAとLがどのように相互するかは表現していない
* Causal diagramsは，Directed acyclic graph: DAG
* Directed: 矢印は，影響の方向を意味する
* Acyclic: 巡回しない．変数は，直接または他の変数を介して，自身の原因にはならない
* DAG上のどの変数も，直接原因を条件づけた上で，原因でない他のどの変数からも独立している（Technical Point 6.1）
* Figure 6.1はConditionally randomized experiment
  * common causeはGraphに含める必要がある
* Figure 6.2はmarginal randomized experiment

![](.gitbook/assets/sukurnshotto-2020-06-05-132333png.png)

* Figure 6.1はobservational studyを表しているかもしれない
  * Aは原因としてLを持つ．Yの原因もL以外にない
  * もしあるならば，例え測定されていなかったとしても共通原因であるため図に含めるべき
* 6.2では，conditional exchangeabilityの仮定をどのように図式化するか説明する
* 多くの人にとって，graphical approachの方がcounterfactual approachより使いやすく直感的である
  * しかし，これらは密接にリンクしている（Technical Point 6.2）
  * conventional causal diagramはcounterfactual variableをグラフ上で含んでいない
  * Single World Intervention Graph \(SWING\)は，どちらも扱える
    * Chapter 7で説明
* Causal diagramは，問題の質的な因果構造についての専門知識や仮定をシンプルに表す方法
  * Causal diagramは，因果ネットワーク内の変数間の潜在的な関連も表す

## 6.2 Causal diagrams and marginal independence

* A: aspirin use -&gt; 心臓病Yのリスクを予防するcausal effectを持つ

$$
\Pr(Y^{a=1}=1) \neq \Pr(Y^{a=0}=1)
$$

![](.gitbook/assets/sukurnshotto-2020-06-05-140939png.png)

* Figure 6.2は，Aをランダムに，条件づけずに割り付けた状況をグラフに表している



* ライターの所持Aは，誰の肺がんYリスクのcausal effect（引き起こす or 予防）はない

$$
\Pr(Y^{a=1}=1) = \Pr(Y^{a=0}=1)
$$

* 喫煙Lは，AとY両方に対しcausal effectを持つ

![](.gitbook/assets/sukurnshotto-2020-06-05-141651png.png)

* Figure 6.2と6.3は，因果関係についての知識のみを用いて書かれたが，予測される変数間の関連性も表している
  * どちらの図でもAとYは関連する
* **Figure 6.2（randomized experiment）について考える**
  * AがYへのcausal effectを持つとき，AとYは関連あることが期待できる
  * unconditional exchangeabilityであるideal randomized experimentでは，causationはassociationを示す．逆も然りである．

$$
\Pr(Y^{a=1}=1) \neq \Pr(Y^{a=0}=1) \to \Pr(Y = 1| A=1) \neq \Pr(Y = 1| A=0) \\
\Pr(Y = 1| A=1) \neq \Pr(Y = 1| A=0) \to \Pr(Y^{a=1}=1) \neq \Pr(Y^{a=0}=1)
$$

* CausationでなくAssociationは，2つの変数の間の関係が対称である．因果関係の矢印の方向に関係なく，2つの変数の間には関連の流れがある．
  * Figure 6.2は，AからYへの関連の流れ，もしくはYからAへの関連の流れがある
* **Figure 6.3 \(Observational study\)について考える**
  * ライターの所持Aは，肺がんYのcausal effectは持たない
  * 今の疑問は，ライターAが肺がんYと関連するかどうか

$$
\Pr(Y^{a=1}=1) = \Pr(Y^{a=0}=1) \to \Pr(Y = 1| A=1) = \Pr(Y = 1| A=0) \>??
$$

* 世間知らずの研究者が，肺がんYのリスクへのライター所持Aのeffectがあるか研究することにしたと想像する
  * 彼は，多くの人に，ライターを所持しているかどうか記録し，向こう5年の間に彼らが肺がんと診断されたかどうか記録した
  * Heraは，ライターを所持している
  * もし，Heraがライターを所持しているならば，彼女はsmokerである可能性が高い，故に，肺がんになるリスクは高い
  * 直感的に，AとYには関連が期待される
    * A=1の集団での肺がんリスクとA=0の集団での肺がんリスクは異なるだろう

$$
\Pr(Y=1|A=1) \neq \Pr(Y=1 | A = 0)
$$





## 6.3 Causal diagrams and conditional independence

## 6.4 Positivity and consistency in causal diagrams

## 6.5 A structural classification of bias

## 6.6 The structure of effect modification

