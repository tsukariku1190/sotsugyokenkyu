# 研究計画書

**学籍番号：AF24099**

**氏名：塚原陸斗**

## 研究テーマ

昼間の街路画像による夜間照度と交通環境の推定に基づく夜間ランニング練習場所推薦

AF24099
昼間の街路画像による夜間照度と交通環境の推定に基づく夜間ランニング練習場所推薦

## 1. 研究背景

根拠となる情報(論文を含む)を用いて社会的課題(実現すべき理想)を提示し，それを解決するためにどのような技術が必要かを述べる．課題と問題を理解していない人が多いので注意すること． / Using supporting information (including academic papers), present the social issue (the ideal state to be achieved) and explain what kind of technology is needed to solve it. Be careful, as many people do not clearly distinguish between an issue and a problem.
社会的課題：夜に走るランナーが初めての場所でも「明るく、車の危険が少ない」練習場所を事前に選べるようにすること。
ジョギング、ランニングは日本で758万人（2024年、年1回以上）が行う運動である。[1]。仕事や学校の後に走る人は、日没後に行う。北米の大規模なランニング記録（20,446件）の分析では、日没後の走行は男性で約13%、女性で約9〜11%であった[2]。また、ランナーは走る場所を環境で選んでいる。ロンドンの40,290地点の分析では、歩道が広く街灯が多い道ほど走る人が多いという結果であった[9]。
しかし、夜の屋外は2つの点で危険が大きくなる。
- 1.交通の危険：日本では、交通死亡事故は17時台から19時台に多く発生している。車と歩行者の死亡事故は、1時間あたりで見ると日没前後1時間が昼間の約4倍であった（2014〜2018年）。
- 2.暗さによる不安：他人を怖いと感じる人が女性26.7%・男性6.8%で、「暗さ」も主な不安の一つだった。[3]。北米の分析では、照明の少ない公園を昼は女性が多く走っていたのに、夜は男性の走行しか記録されていなかった[2]。日本の歩行者の研究でも、夜間の不安と最も強く関係するのは主観的な明るさであった[4]。
こうした危険を避けるには、「どの道が夜に明るいか」「どの道が車と分かれているか」を知る必要がある。しかし、街灯の照度を測るには手間とコストがかかり、自治体などの街灯マップは網羅性に欠けている[5]。衛星から測った夜間光のデータもありますが、解像度は130mと粗く、走る人の多さとの有意な関係は見られなかった[9]。
そこで広い範囲で夜間の明るさを知り、夜間の明るさと交通の危険を分けて評価し、ランナーの判断に合う安全度を出す。そこから練習に使える場所やコースを推薦する技術が必要となる。

## 2. 研究目的

技術的な成果として何が達成されるのかを述べる． / Describe what will be achieved as a technical outcome.
昼間の街路画像だけから、夜間の明るさと交通環境を分けて推定し、夜に走るランナーの判断に合った練習場所を推薦できるようにする

## 3. 関連研究

技術的課題を解決する先行研究に関する論文を提示し，提案技術およびPros & Consを述べる．続いて，Consのまとめから，研究目的を達成するための技術的要求条件を述べる． / Present papers on prior studies that address the technical issue, and describe the proposed technologies and their pros and cons. Then, based on a summary of the cons, describe the technical requirements needed to achieve the research objective.
### 画像から安全の印象を推定する研究
- Dubeyら[6]
56都市のストリートビュー画像約11万枚に、「どちらが安全そうか」の一対比較を117万件集め、Siamese型CNNで学習した。「安全」の正解率は73.5%です。
**Pros：**大規模・多様なデータ。一対比較で主観的な正解を効率よく作る方法を確立
**Cons：**「安全」の中身が定義されておらず、「美しい」との相関が高い
昼の画像のみで交通は評価軸にない
- 小川ら[7]
世田谷区の車載カメラ画像約61万枚と880万回答で、「安全」を含む22項目の印象を1つのモデルで推定
**Pros：**日本の街で実証。同じデータでDubeyらの方式を全項目で上回った。計算が軽い
**Cons：**画像は晴天の日中のもので、夜間の安全は慎重に評価すべきと著者が明記
「安全」は「快適」「美しい」と同じグループになり、好ましさと区別できない。
- 原田・沖[8]
小川らと同じグループが、自転車で昼・夕方・夜の街路を撮影し、印象の違いを分析した。
「安全だ」「不安だ」に最も強く効いたのは「夜かどうか」でした。
**Pros：**夜が安全の印象を大きく変えることを、同じ地点の比較で示した。
自転車とカメラで安く撮影できる
**Cons：**「夜」を一律に扱い、どの道が夜に明るいかは説明できない。夜に撮影した道しか評価できない。夜間画像は明るく補正してから評価しており、実際の照度とは結びついていない
- Jiangら[15]
ロンドン中心部の40,290地点で、Stravaのヒートマップから取った「走る人の多さ」と、Googleストリートビュー画像の画像分割（PSPNet）で測った街並みの特徴を、空間回帰モデルで分析し、歩道の広さ、街灯の多さ、樹木、空の開け具合が、走る人の多さと正の関係にあった。
**Pros：**街路画像の画像分割とランニングを大規模に結びつけた
**Cons：**目的変数は「走る人の多さ（人気）」で、安全ではない
街灯は昼の画像に写った画素の割合で、夜の明るさではない
### 夜間の明るさを測る研究
- 松田ら[5]
多くの人のスマホ照度センサのデータから、街灯の位置と照度を推定した。明石市の約1kmで、街灯の再現率89.2%、照度の誤差率31.9%であった。
**Pros：**防犯灯照度基準で安全を客観的に定義し、夜の実測値で評価した
**Cons：**夜に誰かが歩いた道しか測れない。実験は1経路のみ。LED街灯では誤差率43.1%。街灯以外の光（自販機・店）は「外乱」として除外。交通は扱わない
### 問題
昼の画像で印象を推定しており、夜間の明るさは分からない
夜の状態を知るには、夜に現地で測るか撮影する必要がある
「安全」が見た目の好ましさと混ざり、交通の危険が分かれていない
### 要求される技術
夜間の明るさを、実測照度にもとづくクラスで推定できること
夜に測定・撮影していない道にも、昼間の画像から推定を広げられること
安全を「照明」と「交通」に分けて推定し、根拠を説明できること
区間ごとの安全度から練習場所を推薦できること

## 4. 提案内容

先行研究のConsを解決し，本研究目的を達成するための技術的提案とその新規性について述べる．その際，科学的根拠に基づいて仮説を立て，提案の有効性を担保する． / Describe the technical proposal and its novelty for overcoming the cons of prior work and achieving the objective of this research. In doing so, formulate a hypothesis based on scientific evidence to support the effectiveness of the proposal.
提案：昼間の街路画像に写る「光源」と「道の形」から、夜間の照度クラスを推定する。また、別に交通環境も推定し、2つを組み合わせて推薦する
仮説：夜間の照度は、昼間の画像に写る固定された光源（街灯・店舗・自販機など）と道の形（道幅・街路樹）から、クラス単位で推定できる。
- 根拠：照度は光源からの距離の2乗に反比例し、入射角で減衰する。光源の位置と間隔が分かれば、照度はある程度決まる。
- 街路の画像分割モデルは、「街灯」「看板」「歩道」「車」などを画素単位で分けられる。
Mapillary Vistasで学習したモデルで街路の構成要素を抽出している。[8]
仮説：安全を「照明」と「交通」に分けて推定すると、「安全そうか」の印象を1つの値で推定するよりも、夜に走るランナーの判断に近づく。
- 根拠：既存の「安全」の印象は、「美しい」との相関が高い。つまり、見た目の好みが混ざっている。
一方、ランナーの不安は車（61.0%）と人・暗さ[3]。夜間の不安には明るさが最も強く関係している。
新規性：昼間の画像から夜間の照度を推定すること
照明と交通を分けた安全度で、夜間ランナー向けに推薦すること

## 5. 評価方法

提案の妥当性を検証するためにどのような定量的評価を行うのか，その評価方法について述べる． / Describe what kind of quantitative evaluation will be conducted to verify the validity of the proposal, and explain the evaluation method.
先行研究に対する提案手法の優位性を検証するために，どのような定量的比較評価を行うのか，比較する研究論文を提示し，その評価方法について述べる． / To verify the superiority of the proposed method over prior work, present the research papers used for comparison and describe what kind of quantitative comparative evaluation will be conducted and how it will be performed.

## 6. 研究スケジュール

ガントチャートを用いて提示する(卒業するまでのスケジュール)．研究倫理審査が必要な場合は，その書類作成および審査にかかる期間もスケジュールに組み込む． / Present the schedule up to graduation using a Gantt chart. If research ethics review is required, include the time needed for document preparation and the review process in the schedule.

## 参考文献

- [1] 笹川スポーツ財団, “スポーツライフ・データ2024 プレスリリース,” October 2025
- [2] Grant McKenzie, Daniel Romm, Clara Féré, Maria Laura Guerrero Balarezo, “Gender differences in urban recreational running: A data-driven approach,” Journal of Transport Geography, Vol. 124, 104171, 2025.
- [3] Nadine Schuurman, Leah Rosenkrantz, Scott A. Lear, “Environmental Preferences and Concerns of Recreational Road Runners,” International Journal of Environmental Research and Public Health, Vol. 18, No. 12, 6268, 2021.
- [4] 樋野公宏, 石井儀光, 藤井さやか, “周辺環境が夜間歩行時の犯罪不安に与える影響とその構造,” 日本建築学会計画系論文集, Vol. 79, No. 696, 2014, pp. 445-450
- [5] 松田裕貴, 新井イスマイル, “スマートフォン搭載照度センサの集合知による網羅的な街灯情報収集システムの開発,” 情報処理学会論文誌, Vol. 55, No. 2, 2014, pp. 750-760
- [6] Abhimanyu Dubey, Nikhil Naik, Devi Parikh, Ramesh Raskar, César A. Hidalgo, “Deep Learning the City: Quantifying Urban Perception at a Global Scale,” Proceedings of the European Conference on Computer Vision (ECCV 2016), Amsterdam, The Netherlands, October 2016, pp. 196-212
- [7] Yoshiki Ogawa, Takuya Oki, Chenbo Zhao, Yoshihide Sekimoto, Chihiro Shimizu, “Evaluating the subjective perceptions of streetscapes using street-view images,” Landscape and Urban Planning, Vol. 247, 105073, 2024.
- [8] 原田慶紀, 沖拓弥, “天候や時間帯の違いが人々の街路印象評価に及ぼす影響のモデル分析,” 第37回人工知能学会全国大会論文集, 3F5-GS-10-04, 2023
- [9] Hongchao Jiang, Lin Dong, Bing Qiu, “How Are Macro-Scale and Micro-Scale Built Environments Associated with Running Activity? The Application of Strava Data and Deep Learning in Inner London,” ISPRS International Journal of Geo-Information, Vol. 11, No. 10, 504, 2022
