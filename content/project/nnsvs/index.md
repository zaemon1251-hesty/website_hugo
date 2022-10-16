---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "NNSVS: Neural Network Based Singing Voice Synthesis Toolkit"
summary: "Submitted to [ICASSP 2023](https://2023.ieeeicassp.org/)"
authors:
- admin
- Reo Yoneyama
- Tomoki Toda
tags:
- SVS
- Python
- Deep Learning
- Open-Source
categories: []
date: 2022-10-18T22:17:44+09:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

Submitted to [ICASSP 2023](https://2023.ieeeicassp.org/).


- [Authors](#authors)
- [Abstract](#abstract)
- [Systems](#systems)
- [Samples](#samples)
  - [SVS](#svs)
  - [A/S](#as)
- [Appendix](#appendix)
  - [Note pitch distribution](#note-pitch-distribution)
- [References](#references)

## Authors

- Ryuichi Yamamoto (LINE Corp., Nagoya University)
- Reo Yoneyama (Nagoya University)
- Tomoki Toda (Nagoya University)

## Abstract

This paper describes the design of NNSVS, open-source software for neural network-based singing voice synthesis research.
NNSVS is inspired by Sinsy, one of the open-source pioneers in singing voice synthesis research, and provides many new features such as multi-stream autoregressive models, autoregressive fundamental frequency models, and neural vocoders.
Furthermore, NNSVS provides extensive documentation and scripts to build complete singing voice synthesis systems.
Experimental results demonstrate that our best system significantly outperforms our reproduction of Sinsy and other baseline systems.
The toolkit is available at https://github.com/nnsvs/nnsvs.

## Systems

The following table summarizes the systems used in our experiments. All the models were trained on Namine Ritsu's database [1].

| System                      | Acoustic Features  | Multi-stream Architecture | Autoregressive streams | Vocoder     |
|-----------------------------|--------------------|---------------------------|------------------------|-------------|
| Sinsy [2]                   | MGC, LF0, VUV, BAP | No                        | -                      | hn-uSFGAN  [5]   |
| Sinsy (w/ pitch correction) | MGC, LF0, VUV, BAP | No                        | -                      | hn-uSFGAN   |
| Sinsy (w/ vibrato modeling) | MGC, LF0, VUV, BAP | No                        | -                      | hn-uSFGAN   |
| Muskits RNN [3]             | MEL                | No                        | -                      | HiFi-GAN [6]   |
| DiffSinger [4]              | MEL, LF0, VUV      | Yes                       | -                      | hn-HiFi-GAN |
| NNSVS-Mel v1                | MEL, LF0, VUV      | Yes                       | -                      | hn-uSFGAN   |
| NNSVS-Mel v2                | MEL, LF0, VUV      | Yes                       | LF0                    | hn-uSFGAN   |
| NNSVS-Mel v3                | MEL, LF0, VUV      | Yes                       | MEL, LF0               | hn-uSFGAN   |
| NNSVS-WORLD v0 [1]          | MGC, LF0, VUV, BAP | No                        | -                      | WORLD       |
| NNSVS-WORLD v1              | MGC, LF0, VUV, BAP | Yes                       | -                      | hn-uSFGAN   |
| NNSVS-WORLD v2              | MGC, LF0, VUV, BAP | Yes                       | LF0                    | hn-uSFGAN   |
| NNSVS-WORLD v3              | MGC, LF0, VUV, BAP | Yes                       | MGC, LF0               | hn-uSFGAN   |
| NNSVS-WORLD v4              | MGC, LF0, VUV, BAP | Yes                       | MGC, LF0, BAP          | hn-uSFGAN   |
| hn-HiFI-GAN (A/S)           | MEL, LF0, VUV      | -                         | -                      | hn-HiFi-GAN |
| hn-uSFGAN-Mel (A/S)         | MEL, LF0, VUV      | -                         | -                      | hn-uSFGAN   |
| hn-uSFGAN-WORLD (A/S)       | MGC, LF0, VUV, BAP | -                         | -                      | hn-uSFGAN   |

Notes on baselines

- Muskits and DiffSinger baseline systems were trained with thier offical code ([Muskits](https://github.com/SJTMusicTeam/Muskits/tree/1f1855d914d2077f33ad9675866f474005cd8034/egs/namine_ritsu_utagoe_db/svs1) and [DiffSinger](https://github.com/MoonInTheRiver/DiffSinger)).
- hn-HiFi-GAN is the vocoder used by DiffSinger. The detail of its implementation can be found [here](https://github.com/nnsvs/ParallelWaveGAN/blob/5a1e0e0c6972cfa0efcbd17d4b42c453e611234d/parallel_wavegan/models/hnhifigan.py#L173).
- Sinsy systems are based on NNSVS's implementation.
- NNSVS-WORLD v0 uses the model trained with the earlier version of NNSVS (as of Nov. 2021) [1]. See [here](https://www.youtube.com/watch?v=pKeo9IE_L1I) for details.


## Samples

### SVS

Samples generated from musical score.

<p>Sample 1: 1st color</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 2: ARROW</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 3: BC</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 4: Close to you</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 5: ERROR</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table>

### A/S

Samples generated from extracted features (i.e., analysis-by-synthesis).

<p>Sample 1: 1st color</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 2: ARROW</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 3: BC</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 4: Close to you</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 5: ERROR</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table>

## Appendix

### Note pitch distribution

We selected test songs to cover wide ranges of pitch, which distributions are shown in the following figure.
Pitch is presented as MIDI note number, where A4 (69) corresponds to 440 Hz.
The lowerest and highest notes of the test songs were D#4 (155.6 Hz) and A5 (880 Hz).

<div align="center"><img src="/images/ritsu_pitch_dist.png" width="100%" /></div>

## References

- [1] Canon, [NamineRitsu] Blue (YOASOBI) [ENUNU model Ver.2, Singing DBVer.2 release], https://www.youtube.com/watch?v=pKeo9IE_L1I, Accessed: 2022.10.06.
- [2] Y. Hono, K. Hashimoto, K. Oura, et al., “Sinsy: A deep neural network-based singing voice synthesis system,” IEEE/ACM Trans. on Audio, Speech, and Language Processing, vol. 29, pp. 2803.
- [3] J. Shi, S. Guo, T. Qian, et al., “Muskits: an End-to-end Music Processing Toolkit for Singing Voice Synthesis,” in Proc. Interspeech, 2022, pp. 4277–4281.
- [4] J. Liu, C. Li, Y. Ren, et al., “DiffSinger: Singing Voice Synthesis via Shallow Diffusion Mechanism”, AAAI, vol. 36, no. 10, pp. 11020-11028, Jun. 2022.
- [5] R. Yoneyama, Y.-C. Wu, and T. Toda, “Unified Source-Filter GAN with Harmonic-plus-Noise Source Excitation Generation,” in Proc. Interspeech, 2022, pp. 848–852.
- [6] J. Kong, J. Kim, and J. Bae, “HiFi-GAN: Generative adversarial networks for efficient and high fidelity speech synthesis,” NeurIPS, vol. 33, pp. 17 022–17 033, 2020.
