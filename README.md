# Structural Sharpening and Functional Dependence: Reproducibility Repository

## Japanese

### Overview
このリポジトリは、以下の論文の再現用コードをまとめたものです。

**Structural sharpening and functional dependence: a long-run interregional input-output analysis of Shikoku as a peripheral case in Japan**

四国地域を対象に、1985年、1990年、1995年、2005年の経済産業省公表の地域間産業連関表を用いて、長期的な産業構造変化、地域内価値保持、域外依存、空間的可視化を分析します。再現の中心は、論文で用いた3段階の Notebook ワークフローです。

本リポジトリで再現する主な内容は次のとおりです。

- 部門統合を含む前処理
- スカイライン分析
- 長期推移分析
- 漏出分解と関東依存の把握
- 本四架橋や地域区分図を含む論文用地図の作成

論文本文では、四国の一部産業で選択的な競争力強化が生じる一方で、地域全体の価値保持や機能的自立が改善したとは言い切れないという`structural sharpening`(著者が命名)を主要な論点として扱っています。本リポジトリは、その主要な定量分析と図表生成を再実行できるよう整理したものです。

### Related Research
関連する研究として、同じく四国の長期的な構造変化を地域間産業連関表で分析しつつ、APLや階層ベイズ、GISによる可視化に重点を置いた別プロジェクトがあります。

- [shikoku-economic-analysis](https://github.com/Naaao9999/shikoku-economic-analysis)

こちらは共通の問題意識を持ちながら、要因分解や動的な可視化に重心を置いています。

### Research Focus
本研究は、交通の統合、グローバル化、人口減少の初期進行が重なった1985年から2005年の四国を対象に、周辺地域がどう再編されたのかを見ています。特定の産業で競争力や自給率が上がっても、それが地域全体の需要や価値の蓄積に結びつくとは限らない、という点を実証的に捉えるのが狙いです。

論文の主要な問いは三つに整理できます。

- 四国では、どの産業で自給率や競争力の改善がみられたのか
- そうした改善は、地域全体の需要基盤や価値保持の拡大を伴っていたのか
- 地域内循環の弱まりや域外依存の強まりは、どのような形で進んだのか

### Methods and Main Perspective
分析では、地域間産業連関表を35部門にまとめ、スカイライン分析、自給率と需要構成比の比較、漏出分解、関東依存の把握、空間可視化を組み合わせます。ここでいう structural sharpening は、同じ部門の中で自給率が上がる一方、需要に占める比率が縮むような動きを捉えるための概念です。

この枠組みによって、生産額や表面的な競争力の上昇だけでは見えにくい変化が浮かび上がります。

- 選択的な部門強化と地域全体の基盤縮小の併存
- 地域内保持の弱まりと域外漏出の拡大
- 生産は残っても高次機能やサービス依存が外部に集中する構造

### Workflow
3つの Notebook を順番に実行することで再現作業を行うことができる構成です。Notebook 冒頭の説明もこの順序を前提に書かれています。

#### `notebooks/01_data_preprocessing.ipynb`
論文再現の第1部です。生の地域間産業連関表を、分析で用いる統一部門分類に合わせて前処理・統合します。

- 入力元: `../data/raw/intermunicipal_io_tables/`
- 対応表: `../data/mapping/産業分類統一対応表_S60_H2_H7_H17.xlsx`
- 主な出力先: `../output/tables/`
- 生成される統合済みファイル: `S60_integrated.xlsx`, `H2_integrated.xlsx`, `H7_integrated.xlsx`, `H17_integrated.xlsx`

#### `notebooks/02_main_analysis.ipynb`
論文再現の第2部です。前処理済みの統合表を読み込み、論文の主要な実証分析を実行します。Notebook 冒頭では、`../output/tables/` から統合済み表を読み込み、Skyline analysis、structural X-ray analysis、leakage decomposition、long-run comparisons などを再現すると明記されています。

Notebook 内の主なセクションは次のとおりです。

- `スカイライン・X-ray`
- `長期推移分析`
- `支店経済化分析`
- `架橋分析`

分析結果、中間集計、図表用データは `../output/` 配下に保存されます。

#### `notebooks/03_visualization.ipynb`
論文再現の第3部です。論文で使用した地図図表を作成します。

- 入力元: `../data/raw/municipality_shapefile/`
- 主な用途: 研究対象地域の地図、全国地域区分地図、本四架橋ネットワーク図の作成
- 出力先: `../output/`

Notebook 冒頭では、少なくとも「本四架橋ネットワークと研究対象地域の地図」と「地域間産業連関分析で用いる全国地域区分地図」を出力すると説明されています。

### Repository Structure

```text
.
├─ README.md
├─ requirements.txt
├─ presentations/
│  └─ 2026-03_ICES2026_presentation_inoda.pdf
├─ notebooks/
│  ├─ 01_data_preprocessing.ipynb
│  ├─ 02_main_analysis.ipynb
│  └─ 03_visualization.ipynb
├─ data/
│  ├─ raw/
│  │  ├─ intermunicipal_io_tables/
│  │  └─ municipality_shapefile/
│  └─ mapping/
│     └─ 産業分類統一対応表_S60_H2_H7_H17.xlsx
└─ output/
   ├─ figures/
   └─ tables/
```

### Presentation Material
ICES 2026 学会での発表資料を以下のファイル名で収録しています。

- `presentations/2026-03_ICES2026_presentation_inoda.pdf`

この資料は、投稿中論文に関連する学会発表資料として位置づけています。論文本文と完全に同一ではなく、学会発表時点の構成や表現を含む可能性があります。

### Required Data
論文再現には、少なくとも次のデータが必要です。

- 経済産業省の地域間産業連関表
- 行政区域の GIS データ
- 部門統合用の対応表

このうち、地域間産業連関表と GIS データは、再配布制約を考慮して、公開版では利用者自身が取得して配置する前提で案内するのが適切です。README もその前提で記載しています。

#### 1. 地域間産業連関表
対象年次は 1985年、1990年、1995年、2005年です。`01_data_preprocessing.ipynb` の冒頭説明に合わせると、想定入力ファイル名は「2026年4月時点の経産省HPから取得した元ファイル名」または短い整理名です。

| Year | Preferred filename | Supported original filename |
| :--- | :--- | :--- |
| 1985 | `S60.xlsx` | `h2rio85a.xlsx` |
| 1990 | `H2.xlsx` | `h2rio90a.xlsx` |
| 1995 | `H7.xlsx` | `h2rio95c.xlsx` |
| 2005 | `H17.xlsx` | `H17年地域間産業連関表(53部門).xlsx` |

配置先:

```text
data/raw/intermunicipal_io_tables/
```

入手先:

- 経済産業省「地域間産業連関表」
  <https://www.meti.go.jp/statistics/tyo/tiikiio/index.html>

#### 2. GIS データ
`03_visualization.ipynb` は `../data/raw/municipality_shapefile/` から市区町村シェープファイルを読み込む前提です。公開版では、利用者が行政区域データを取得して、少なくとも次の構成で配置することを想定しています。

- `region.shp`
- `region.shx`
- `region.dbf`
- `region.prj`

配置先:

```text
data/raw/municipality_shapefile/
```

参考:

- 国土交通省 国土数値情報
  <https://nlftp.mlit.go.jp/ksj/>

#### 3. 部門統合対応表
前処理には次のファイルを使用します。

- `data/mapping/産業分類統一対応表_S60_H2_H7_H17.xlsx`

この対応表は、利用者が別途取得する前提ではなく、すでに本リポジトリ内に含まれています。

### How To Run
再現手順は次のとおりです。

1. このリポジトリを取得します。
2. Python 環境を用意し、依存パッケージをインストールします。
3. 地域間産業連関表を `data/raw/intermunicipal_io_tables/` に配置します。
4. GIS データを `data/raw/municipality_shapefile/` に配置します。
5. `notebooks/01_data_preprocessing.ipynb` を実行します。
6. `notebooks/02_main_analysis.ipynb` を実行します。
7. `notebooks/03_visualization.ipynb` を実行します。

Notebook は順番依存なので、原則としてこの順に実行してください。

### Python Environment
`requirements.txt` に含まれているパッケージは次のとおりです。

- `pandas`
- `numpy`
- `matplotlib`
- `geopandas`
- `scipy`
- `pymc`
- `arviz`
- `openpyxl`

Notebook の import を確認すると、環境によっては追加で次のパッケージも必要です。

- `pillow`
- `seaborn`
- `japanize-matplotlib`
- `adjustText`
- `shapely`

また、`01_data_preprocessing.ipynb` には `google.colab` 由来の import が含まれています。ローカル Jupyter で実行する場合は、その部分を環境に応じて読み替えてください。

### Expected Outputs
実行後、`output/` 配下には少なくとも次の成果物が生成される想定です。

- 統合済みの地域間産業連関表
- 中間集計表
- 論文図表作成用データ
- GIS ベースの可視化図

論文投稿版の紙面そのものを直接組版するリポジトリではありませんが、論文の主要分析と図表生成プロセスの再現を目的としています。

### Notes
- 本リポジトリは研究再現用です。
- 再配布制約のある生データは、公開版では利用者自身が取得する前提で扱ってください。
- データ利用条件は各提供元の規約に従ってください。
- 公開前には、Notebook 内の絶対パスや個人用ストレージ依存が残っていないか確認することを推奨します。

### Citation
本リポジトリを参照する場合は、対応する論文またはその公開版を引用してください。

Suggested citation:

Inoda, N., and Ishiro, T. *Structural sharpening and functional dependence: a long-run interregional input--output analysis of Shikoku as a peripheral case in Japan.*

---

## English

### Overview
This repository contains the reproducibility code for the following paper:

**Structural sharpening and functional dependence: a long-run interregional input--output analysis of Shikoku as a peripheral case in Japan**

The repository analyzes long-run structural change, regional value retention, extra-regional dependence, and spatial visualization for the Shikoku region using interregional input-output tables for 1985, 1990, 1995, and 2005. The core reproducibility workflow consists of the same three notebooks used for the paper.

The main components reproduced in this repository include:

- preprocessing and sector harmonization
- Skyline analysis
- long-run comparative analysis
- leakage decomposition and Kanto dependence analysis
- production of paper-ready maps, including the Honshu-Shikoku bridge network and regional classification maps

In the paper, a central argument is that selective strengthening in some sectors in Shikoku did not necessarily lead to improved regional value retention or stronger functional autonomy for the region as a whole. This repository is organized so that the main quantitative analyses and figure-generation workflow can be rerun in a reproducible manner.

### Related Research
A related project connected to this repository is:

- [shikoku-economic-analysis](https://github.com/Naaao9999/shikoku-economic-analysis)

That repository shares a common interest in long-run structural change in the Shikoku region and places greater emphasis on APL (Average Propagation Length), hierarchical Bayesian decomposition, and GIS-based visualization. 

### Research Focus
The main point of the paper is "Structural Sharpening" (a term coined by the authors), which argues that while selective competitiveness has been strengthened in some industries in Shikoku, it cannot be said that the overall value preservation or functional independence of the region has improved. This repository is organized to allow for the re-execution of the main quantitative analysis and the generation of figures and tables.

The main research questions can be summarized as follows:

- In which sectors did Shikoku experience gains in self-sufficiency or competitiveness?
- Did those gains also expand the broader regional demand base and value-retention capacity?
- How did weakening intraregional circulation and stronger extra-regional dependence unfold over time?

### Methods and Main Perspective
The analysis combines harmonized interregional input-output tables at the 35-sector level with Skyline analysis, long-run comparison of self-sufficiency and demand-share width, leakage decomposition, analysis of dependence on Kanto, and spatial visualization. In the paper, `structural sharpening` refers to a pattern in which a sector's self-sufficiency rises while its demand-share width contracts.

This perspective is used to capture structural changes that are difficult to see through production levels or competitiveness measures alone, including:

- the coexistence of selective sectoral strengthening and shrinkage of the broader regional base
- weakening intraregional retention and expansion of extra-regional leakage
- a structure in which production remains locally present while higher-order functions and service dependence become more externally concentrated

### Workflow
The reproducibility workflow is organized as three notebooks executed in sequence. The introductory text at the beginning of each notebook is also written with this order in mind.

#### `notebooks/01_data_preprocessing.ipynb`
This is the first part of the paper reproduction workflow. It preprocesses and harmonizes the raw interregional input-output tables into the unified sector classification used in the analysis.

- Input directory: `../data/raw/intermunicipal_io_tables/`
- Concordance file: `../data/mapping/産業分類統一対応表_S60_H2_H7_H17.xlsx`
- Main output directory: `../output/tables/`
- Integrated output files: `S60_integrated.xlsx`, `H2_integrated.xlsx`, `H7_integrated.xlsx`, `H17_integrated.xlsx`

#### `notebooks/02_main_analysis.ipynb`
This is the second part of the paper reproduction workflow. It reads the harmonized tables produced in the preprocessing step and runs the main empirical analyses reported in the paper. As stated in the notebook introduction, it reads the integrated tables from `../output/tables/` and reproduces analyses such as Skyline analysis, structural X-ray analysis, leakage decomposition, and long-run comparisons.

The main sections inside the notebook include:

- `スカイライン・X-ray`
- `長期推移分析`
- `支店経済化分析`
- `架橋分析`

Analysis outputs, intermediate summaries, and figure-ready data are saved under `../output/`.

#### `notebooks/03_visualization.ipynb`
This is the third part of the paper reproduction workflow. It generates the map figures used in the paper.

- Input directory: `../data/raw/municipality_shapefile/`
- Main use: maps of the study area, Japan's regional classification, and the Honshu-Shikoku bridge network
- Output directory: `../output/`

The notebook introduction explains that it produces at least two types of outputs: a map of the Honshu-Shikoku bridge network and study area, and a map of Japan's regional classification used in the interregional input-output analysis.

### Repository Structure

```text
.
├─ README.md
├─ requirements.txt
├─ presentations/
│  └─ 2026-03_ICES2026_presentation_inoda.pdf
├─ notebooks/
│  ├─ 01_data_preprocessing.ipynb
│  ├─ 02_main_analysis.ipynb
│  └─ 03_visualization.ipynb
├─ data/
│  ├─ raw/
│  │  ├─ intermunicipal_io_tables/
│  │  └─ municipality_shapefile/
│  └─ mapping/
│     └─ 産業分類統一対応表_S60_H2_H7_H17.xlsx
└─ output/
   ├─ figures/
   └─ tables/
```

### Presentation Material
If related conference materials are included in the repository, they are placed under `presentations/`. At present, the ICES 2026 presentation slides are included as:

- `presentations/2026-03_ICES2026_presentation_inoda.pdf`

This file is included as conference presentation material related to the manuscript currently under review. It is not necessarily identical to the submitted paper and may reflect the structure and wording used at the time of the conference presentation.

### Required Data
At minimum, the following data are required to reproduce the paper:

- METI interregional input-output tables
- GIS boundary data
- the sector concordance file used for harmonization

Among these, the interregional input-output tables and GIS data should be obtained and placed locally by each user when this repository is distributed publicly, because redistribution restrictions need to be respected. This README is written on that basis.

#### 1. Interregional input-output tables
The analysis covers four benchmark years: 1985, 1990, 1995, and 2005. Consistent with the introductory note in `01_data_preprocessing.ipynb`, the expected input filenames are either the original filenames downloaded from the METI website as of April 2026 or the shorter normalized filenames.

| Year | Preferred filename | Supported original filename |
| :--- | :--- | :--- |
| 1985 | `S60.xlsx` | `h2rio85a.xlsx` |
| 1990 | `H2.xlsx` | `h2rio90a.xlsx` |
| 1995 | `H7.xlsx` | `h2rio95c.xlsx` |
| 2005 | `H17.xlsx` | `H17年地域間産業連関表(53部門).xlsx` |

Placement:

```text
data/raw/intermunicipal_io_tables/
```

Source:

- METI Interregional Input-Output Tables
  <https://www.meti.go.jp/statistics/tyo/tiikiio/index.html>

#### 2. GIS data
`03_visualization.ipynb` assumes that municipality shapefiles are read from `../data/raw/municipality_shapefile/`. In a public reproducibility setting, users are expected to obtain administrative boundary data themselves and place at least the following files there:

- `region.shp`
- `region.shx`
- `region.dbf`
- `region.prj`

Placement:

```text
data/raw/municipality_shapefile/
```

Reference:

- MLIT National Land Numerical Information
  <https://nlftp.mlit.go.jp/ksj/>

#### 3. Sector concordance file
The preprocessing step uses the following file:

- `data/mapping/産業分類統一対応表_S60_H2_H7_H17.xlsx`

This concordance file is already included in the repository and does not need to be obtained separately by the user.

### How To Run
The basic reproduction procedure is as follows:

1. Obtain this repository.
2. Prepare a Python environment and install the required packages.
3. Place the interregional input-output tables under `data/raw/intermunicipal_io_tables/`.
4. Place the GIS boundary data under `data/raw/municipality_shapefile/`.
5. Run `notebooks/01_data_preprocessing.ipynb`.
6. Run `notebooks/02_main_analysis.ipynb`.
7. Run `notebooks/03_visualization.ipynb`.

Because the notebooks have sequential dependencies, they should be executed in this order.

### Python Environment
The following packages are listed in `requirements.txt`:

- `pandas`
- `numpy`
- `matplotlib`
- `geopandas`
- `scipy`
- `pymc`
- `arviz`
- `openpyxl`

Based on the notebook imports, some environments may additionally require:

- `pillow`
- `seaborn`
- `japanize-matplotlib`
- `adjustText`
- `shapely`

In addition, `01_data_preprocessing.ipynb` contains an import related to `google.colab`. If you run the notebook locally in Jupyter, that part may need to be adapted to your environment.

### Expected Outputs
After execution, `output/` is expected to contain at least the following types of artifacts:

- harmonized interregional input-output tables
- intermediate summary tables
- figure-ready data used in the paper
- GIS-based visualizations

This repository is not intended to reproduce the final journal layout itself, but rather the main analytical and figure-generation process behind the paper.

### Notes
- This repository is intended for research reproducibility.
- Redistribution-restricted raw data should be obtained directly by each user in the public version of the repository.
- Data use must follow the terms and conditions of the original providers.
- Before public release, it is advisable to confirm that no notebook still depends on absolute local paths or personal storage locations.

### Citation
If you refer to this repository, please cite the corresponding paper or its public version.

Suggested citation:

Inoda, N., and Ishiro, T. *Structural sharpening and functional dependence: a long-run interregional input--output analysis of Shikoku as a peripheral case in Japan.*
