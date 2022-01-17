---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Parallel WaveGAN: GPUを利用した高速かつ高品質な音声合成 / Parallel WaveGAN: Fast and High-Quality GPU Text-to-Speech @ LINE DEV DAY 2020"
event: LINE DEVELOPER DAY 2020
event_url: "https://linedevday.linecorp.com/2020/en/sessions/8721"
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: " "
abstract: Text-to-speech is a technology that synthesizes human voice from a text by computer. For services that require real-time interaction with users, such as LINE CLOVA smart speakers, text-to-speech systems are required to have high synthesis quality and generate speech at high speed. In this session, we will present the results of our research on GPU-based speech synthesis, which we developed jointly with NAVER and LINE. Typical conventional methods suffer from the slow generation or long training time. This session covers how we addressed these issues, based on a paper accepted for ICASSP 2020, a top conference on speech signal processing, with recent developments in related fields.

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-11-25T14:20:00+09:00
date_end: 2020-11-25T14:50:00+09:00
all_day: false

# Schedule page publish date (NOT event date).
publishDate: 2020-11-25T14:20:00+09:00

authors: ["admin"]
tags:
- Presentation
- TTS
- Deep Learning

# Is this a featured event? (true/false)
featured: false

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

# Optional filename of your slides within your event's folder or a URL.
url_slides: https://speakerdeck.com/line_devday2020/parallel-wavegan-fast-and-high-quality-gpu-text-to-speech

url_code:
url_pdf:
url_video: https://www.youtube.com/watch?v=knzT7M6qsl0

# Markdown Slides (optional).
#   Associate this event with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: ["pwg"]
---

### Abstract (ja)

コンピュータによってテキストから人間の声を合成する技術は、テキスト音声合成と呼ばれます。LINE CLOVAのスマートスピーカーを初めとするユーザとのリアルタイムのインタラクションが必要なサービスでは、音声合成システムには合成品質が高いことだけでなく、高速に音声を生成できることが求められます。本セッションでは、高速かつ高品質な音声合成を実現するために、NAVERとLINEで共同で開発したGPUベースの音声合成の研究成果について発表します。従来の方法では、品質が良くても合成速度が遅い、合成速度は速い一方でモデルの学習に多大な時間がかかるなどの問題がありました。我々はそのような問題に対してどのようにアプローチしたのか、音声信号処理のトップカンファレンスICASSP 2020に採択された論文の内容を元に、近年の関連分野の発展を交えて紹介します。