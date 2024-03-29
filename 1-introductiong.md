# x86-64 からは始めるアセンブラ入門

# アセンブリ言語とは？

アセンブリ言語は、コンピュータのプロセッサが直接理解できる機械語に非常に近い形で記述されたプログラミング言語です。プログラムを機械語に翻訳する作業は、アセンブラと呼ばれる特別なプログラムによって行われます。アセンブリ言語は、メモリの管理やプロセッサのレジスタ操作など、ハードウェアの細かい部分に直接アクセスし、制御することが可能です。これにより、プログラマーは高度な最適化を行うことができますが、その反面、プログラムを書く際には、そのコンピュータのアーキテクチャに関する深い知識が必要となります。

アセンブリ言語は、高レベル言語に比べて読み書きが困難であり、開発プロセスが複雑になることがあります。しかし、システムのパフォーマンスを最大限に引き出したい場合や、リアルタイムシステム、組み込みシステムなど、リソースが限られている環境での開発には欠かせない言語です。また、アセンブリ言語を学ぶことは、コンピュータの動作原理やプログラミングの基本を深く理解するのにも役立ちます。

個人的な意見としては、アセンブリ言語の学習は、コンピュータサイエンスにおける重要な一歩であり、全てのプログラマーが少なくとも基本的な概念を理解しているべきだと思います。それによって、より効率的なコードを書くための根底にある理解が深まります。ただし、初心者にはやや難解でアプローチが難しいかもしれませんので、基礎からしっかりと学ぶことが大切です。

# アーキテクチャとは？

コンピュータの「アーキテクチャ」とは、そのコンピュータシステムの基本的な設計や構造のことを指します。これには、コンピュータがどのようにデータを処理するか、データを一時的に保存するためのメモリはどのように構成されているか、そしてコンピュータの各部分がどのように連携して動作するかといったことが含まれます。簡単に言うと、アーキテクチャはコンピュータの「設計図」のようなものです。

# 高レベル言語とアセンブリ言語の比較

高レベル言語とアセンブリ言語は、コンピュータに命令を与えるためのプログラミング言語ですが、そのアプローチと目的に大きな違いがあります。

高レベル言語は、人間が理解しやすい抽象的な概念を用いてプログラムを記述します。例えば、Python や Java のような言語は、高度な抽象化を提供し、メモリ管理や複雑なデータ構造の操作を簡単に行えるように設計されています。これらの言語は、様々なタイプのプログラム開発に適しており、開発者がより迅速にプロジェクトを進めることができます。

一方で、アセンブリ言語は、コンピュータの CPU が直接実行可能な命令を、人間が読み書きしやすい形式で表したものです。アセンブリ言語は、特定のプロセッサアーキテクチャに密接に関連しており、メモリアドレスの操作やレジスタの使用など、ハードウェアに近いレベルでのプログラミングを可能にします。

アセンブリ言語を学ぶメリット
アセンブリ言語を学ぶことは、多くのプログラマーにとっては非常に特殊な経験ですが、以下のようなメリットがあります：

深い理解：

- アセンブリ言語を学ぶことで、コンピュータの動作原理やプロセッサがどのように命令を実行するかについて、深い理解を得ることができます。これは、高レベル言語だけを使用していると見逃してしまうような、コンピュータの基本的な仕組みを学ぶことになります。

性能の最適化：

- アセンブリ言語を使用することで、プログラムの性能を細かく調整し、最適化することが可能です。特に、実行速度やメモリ使用量が重要なアプリケーションでは、アセンブリ言語で書かれたコードが重要な役割を果たすことがあります。

低レベルアクセスとハードウェア制御：

- アセンブリ言語は、ハードウェアに直接アクセスし、制御する能力を提供します。これは、組み込みシステム、デバイスドライバ、または特定のハードウェア操作を必要とする他のアプリケーションで特に有用です。

プログラミングスキルの向上：

- アセンブリ言語の学習は、他のプログラミング言語を使う際の理解を深めることにも役立ちます。メモリ管理や CPU の動作原理などの基本的な概念を理解することで、より効率的なコードを書くことができるようになります。

セキュリティへの理解：

- アセンブリ言語を知ることは、ソフトウェアのセキュリティ面においてもメリットがあります。バッファオーバーフローやその他の低レベルの脆弱性を理解し、適切な対策を講じる能力が高まります。

個人的な意見としては、アセンブリ言語の学習は確かに挑戦的ですが、それを通じて得られるコンピュータの深い理解やプログラミング能力の向上は、多くの開発者にとって貴重な資産となります。初心者にとっては難解に感じるかもしれませんが、基礎的なコンセプトから徐々に学んでいくことで、プログラミングの世界における新たな視点を開くことができるでしょう。

# x86-64 アーキテクチャのアセンブラから始める理由

アセンブラを学ぶ際に x86-64 から始める利点はいくつかありますが、これは個人的な意見を交えた考察になります。まず、x86-64 は非常に広く使用されているアーキテクチャで、デスクトップ PC、ラップトップ、サーバーなど、多くのプラットフォームで見られます。これにより、x86-64 を学ぶことは実際のシステムやソフトウェア開発プロジェクトに直接応用しやすくなります。

また、x86-64 アーキテクチャは、過去数十年にわたる進化の結果、豊富な機能と複雑さを持つようになりました。これにより、低レベルプログラミングの様々な側面（メモリ管理、マルチタスキング、仮想化など）について深い理解を得ることができます。

さらに、x86-64 のドキュメントや学習リソースが豊富にあり、オンラインフォーラムやコミュニティでのサポートも手厚いです。これは学習過程で直面するかもしれない疑問や問題を解決する際に非常に役立ちます。

ただし、x86-64 アーキテクチャの複雑さは初学者にとって挑戦的である可能性があります。命令セットが非常に大きく、様々な命令形式が存在するため、学習の初期段階で圧倒されるかもしれません。ですが、これを乗り越えることができれば、他のよりシンプルなアーキテクチャを学ぶ際には容易に感じるかもしれませんし、深い理解が得られるでしょう。

最後に、プログラミング言語や開発ツールが x86-64 アーキテクチャをサポートしていることが多いため、学習成果を実践的なプロジェクトに活かしやすいという利点もあります。

これはあくまで個人的な見解ですが、x86-64 からアセンブリ言語の学習を始めることは、実用的かつ深い技術的理解を得るための良い選択と言えるでしょう。

# コンピュータアーキテクチャの基礎

## CPU

CPU については、以下のリンク先の記事で詳しく解説していますので、一旦そちらをご覧ください。終わったら、こちらに戻ってきてください。
https://elite-lane.com/central-processing-unit/

## メモリ管理

メモリ管理はコンピュータシステムにおいて非常に重要な役割を果たします。メモリ管理は、コンピュータの物理メモリ（主に RAM：ランダムアクセスメモリ）の使用を効率的に行い、プログラム実行時のデータと命令の格納場所を管理するプロセスです。このプロセスには、メモリの割り当て、保護、共有、メモリマッピング、およびキャッシングなどが含まれます。

### メモリ階層

コンピュータのメモリシステムは、速度とコストのバランスを取るために階層化されています。この階層の最上位には、CPU に最も近く、最も高速にアクセスできるレジスタがあります。その次にキャッシュメモリ、主メモリ（RAM）、そして最も遅く大容量の補助記憶装置（ハードディスクや SSD など）が位置づけられます。

### メモリ割り当て

メモリ割り当ては、プログラムやプロセスが使用するメモリ領域を確保するプロセスです。オペレーティングシステムは、プログラムが実行される際に必要なメモリ領域を割り当て、プログラムが終了した後はそのメモリを解放し、再利用可能にします。

### ページングとセグメンテーション

メモリ管理の技術にはページングとセグメンテーションがあります。ページングは、物理メモリを固定サイズのブロック（ページ）に分割し、仮想メモリアドレスを物理メモリアドレスにマッピングする技術です。セグメンテーションは、メモリを異なるサイズのセグメントに分割する方法で、プログラムの論理的な構造に基づいています。

### メモリ保護

メモリ保護は、プロセスが他のプロセスのメモリ領域に不正にアクセスするのを防ぐためのメカニズムです。これにより、システムの安定性とセキュリティが保たれます。

### 仮想メモリ

仮想メモリは、物理メモリの容量を超えるプログラムを実行できるようにする技術です。このシステムでは、物理メモリがフルになると、一部のデータを補助記憶装置に一時的に移動させ、必要なときに再び物理メモリに戻します。これにより、プログラムはより多くのメモリを使用しているかのように振る舞うことができます。

メモリ管理は、プログラムのパフォーマンスと効率に直接影響を与えるため、コンピュータシステムの設計と運用において中心的な役割を担います。プログラマやシステム設計者は、これらの基本的なメモリ管理の概念を理解し、適切に利用することが重要です。

## レジスタとは

レジスタは、コンピュータの CPU 内に存在する非常に高速な記憶領域で、プロセッサが直接アクセスして読み書きを行うことができる小さなデータホルダーです。プログラムの実行中に頻繁に使用されるデータや命令の一時的な保持、計算結果の一時格納、プログラムの実行状態の管理など、さまざまな目的で使用されます。レジスタの高速アクセス性は、コンピュータの性能に直接影響を与える重要な要素です。

### x86-64 アーキテクチャのレジスタ

「x86-64 アーキテクチャ」とは、特に Intel と AMD という二つの大手半導体製造会社によって開発された、コンピュータの CPU（中央処理装置）のアーキテクチャの一種です。このアーキテクチャは、もともとは「x86」と呼ばれる 32 ビットアーキテクチャを基にしていますが、それを 64 ビットに拡張したものです。64 ビットアーキテクチャへの拡張により、コンピュータはより多くのデータを同時に処理できるようになり、またより大きなメモリアドレス空間にアクセスできるようになりました。

簡単に言うと、x86-64 アーキテクチャは、コンピュータがより高速に、より多くの作業を一度に処理できるようにするための「進化版設計図」のようなものです。

x86 アーキテクチャでは、32 ビットと 64 ビットのプロセッサで利用可能なレジスタの種類が異なります。32 ビットアーキテクチャでは、主に以下の種類のレジスタがあります：

汎用レジスタ：データ操作（算術演算、データ転送など）に使用されるレジスタ。EAX、EBX、ECX、EDX、ESI、EDI、EBP、ESP などがあります。
セグメントレジスタ：メモリセグメントのアドレス指定に使用されるレジスタ。CS（コードセグメント）、DS（データセグメント）、ES、FS、GS、SS（スタックセグメント）などがあります。
フラグレジスタ（EFLAGS）：プロセッサの状態や算術演算の結果を示すフラグビットの集まりです。
命令ポインタレジスタ（EIP）：次に実行される命令のアドレスを保持します。
64 ビットアーキテクチャ（x86-64 または AMD64）では、これらのレジスタに加えて、以下の拡張が行われています：

拡張汎用レジスタ：32 ビットレジスタが 64 ビットに拡張され、RAX、RBX、RCX、RDX、RSI、RDI、RBP、RSP などとして使用されます。
追加の汎用レジスタ：R8 から R15 までの新しいレジスタが追加され、より多くのデータを同時に保持できるようになりました。
RIP レジスタ：64 ビットの命令ポインタレジスタで、次に実行される命令のアドレスを保持します。

# 8、16、32、64 ビットのレジスタとその関係

以下は、8 ビット、16 ビット、32 ビット、64 ビットのレジスタとその関係を、Intel x86 アーキテクチャ（特に x86-64 アーキテクチャを含む）においてマークダウン形式で説明したものです。

| レジスタのサイズ | レジスタの種類                                                       | 説明                                                                                                                                |
| ---------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 64 ビット        | `RAX`, `RBX`, `RCX`, `RDX`, `RSI`, `RDI`, `RBP`, `RSP`, `R8` - `R15` | x86-64 アーキテクチャで導入された拡張レジスタです。32 ビット、16 ビット、8 ビットのデータ操作もサポートしています。                 |
| 32 ビット        | `EAX`, `EBX`, `ECX`, `EDX`, `ESI`, `EDI`, `EBP`, `ESP`               | 32 ビットのデータ操作に使用されます。64 ビットレジスタの下位 32 ビットとしても機能します。                                          |
| 16 ビット        | `AX`, `BX`, `CX`, `DX`, `SI`, `DI`, `BP`, `SP`                       | 古い 16 ビットのデータ操作に使用されます。32 ビットおよび 64 ビットレジスタの下位 16 ビットとして機能します。                       |
| 8 ビット         | `AL`, `BL`, `CL`, `DL`, `AH`, `BH`, `CH`, `DH`                       | 16 ビットレジスタの下位または上位 8 ビットにアクセスします。`AH`は`AX`の上位 8 ビットを表しますなど。                               |
| 8 ビット         | `SIL`, `DIL`, `BPL`, `SPL`, `R8B` - `R15B`                           | x86-64 アーキテクチャで導入された、新しい 8 ビットレジスタです。それぞれ対応する 64 ビットレジスタの下位 8 ビットにアクセスします。 |

この表は、各レジスタの関係性と使用目的を簡潔に示しています。8 ビットおよび 16 ビットレジスタは、主に互換性のため、または特定の用途で小さなデータサイズが必要な場合に使用されます。32 ビットレジスタは、IA-32（32 ビット Intel Architecture）で広く使用され、64 ビットレジスタは x86-64 アーキテクチャにおいて標準的なデータサイズとなります。各レジスタは、特定のデータサイズの操作に最適化されていることを示しており、プログラミングする際にはこれらの特性を考慮する必要があります。

### x86-64 アーキテクチャで導入された、新しい 8 ビットレジスタの補足

x86-64 アーキテクチャ（AMD64 または Intel 64）では、既存のレジスタに加えて新しいレジスタが導入されました。これには、R8 から R15 までの追加の汎用レジスタが含まれます。これらの新しいレジスタは、64 ビット、32 ビット、16 ビット、そして 8 ビットの各バージョンを提供します。8 ビットのバージョンは R8B から R15B としてアクセスされ、それぞれの 64 ビットレジスタの下位 8 ビットに対応します。

また、SIL、DIL、BPL、SPL は、それぞれ RSI、RDI、RBP、RSP の下位 8 ビットを指します。これらは、x86 アーキテクチャの SI、DI、BP、SP レジスタの 8 ビットバージョンで、x86-64 アーキテクチャで新たに導入されました。以前の x86 アーキテクチャでは、SI、DI、BP、SP レジスタの下位 8 ビットに直接アクセスする方法はありませんでした。

したがって、正確には、SIL、DIL、BPL、SPL も x86-64 アーキテクチャで導入された新しい 8 ビットレジスタであり、既存の 16 ビットレジスタの拡張として機能し、それぞれの下位 8 ビットにアクセスするために使用されます。

## 32/64 ビットの NASM

32 ビットおよび 64 ビットの OS 環境で、16 ビットや 8 ビットのレジスタを使用することが可能です。実際、x86 アーキテクチャは下位互換性を保持しているため、新しいアーキテクチャ（例えば、64 ビットの x86-64）でも、古いアーキテクチャ（例えば、16 ビットの x86）で使用されていたレジスタや命令セットにアクセスできます。

### 32 ビットアーキテクチャにおけるレジスタ使用

32 ビットモード（IA-32）では、16 ビットおよび 8 ビットレジスタが利用可能です。例えば、32 ビットレジスタ EAX の下位 16 ビットは AX として、さらにその下位 8 ビットを AL（下位バイト）と AH（上位バイト）として扱うことができます。このようにして、同じ物理レジスタの異なるビット幅の部分にアクセスすることが可能です。

### 64 ビットアーキテクチャにおけるレジスタ使用

64 ビットモード（x86-64 または AMD64）でも、同様に 16 ビットおよび 8 ビットのレジスタを使用できます。64 ビットレジスタ（例えば、RAX）の下位 32 ビットは EAX、その下位 16 ビットは AX、そして AX の下位 8 ビットを AL としてアクセスできます。また、RAX の 8 ビット上位バイトに直接アクセスする方法は用意されていませんが、新たに R8 から R15 までのレジスタが追加され、これらのレジスタも 8 ビットおよび 16 ビット部分へのアクセスが可能です（例：R8B、R8W）。

### 使用上の注意

ただし、64 ビットモードで 16 ビットレジスタを使用する際にはいくつか注意点があります。特に、一部の命令ではデフォルトのオペレーションサイズが 64 ビットまたは 32 ビットになるため、16 ビットオペレーションを行いたい場合は明示的にオペランドサイズを指定する必要がある場合があります。また、16 ビットレジスタを使用することで性能に影響を与える可能性もあるため、最適化を目指す場合はこれらの点を考慮する必要があります。

総じて、32 ビットおよび 64 ビットの NASM では、下位互換性を活かして 8 ビットや 16 ビットのレジスタを使用することができますが、アーキテクチャの特性を理解し、適切に使用することが重要です。

## 64 ビットモードや 32 ビットモードとは？

64 ビットモードと 32 ビットモードは、コンピュータの CPU がプログラムを実行する際の動作モードを指します。これらのモードは、主に CPU が扱うデータのサイズやアドレス空間の大きさに影響を与えます。以下、それぞれのモードについて簡単に説明します。

### 64 ビットモード

64 ビットモード（x86-64 または AMD64 とも呼ばれる）は、64 ビットのデータ幅と拡張されたアドレス空間を特徴としています。このモードでは、CPU は 64 ビットのレジスタを使用してデータを処理し、理論上 2^64 バイト（約 18.4 エクサバイト）のメモリアドレス空間にアクセスできます。これにより、より大きなメモリ容量の利用や、より高速なデータ処理が可能になります。

64 ビットモードでは、新たに追加されたレジスタ（R8〜R15 など）を使用できるほか、従来の 32 ビットレジスタ（EAX、EBX など）や、更に古い 16 ビットおよび 8 ビットのレジスタも引き続き使用可能です。このモードは、現代の多くのオペレーティングシステムやアプリケーションで標準的に使用されています。

### 32 ビットモード

32 ビットモード（IA-32 とも呼ばれる）は、32 ビットのデータ幅を持ち、最大 4GB（2^32 バイト）のメモリアドレス空間にアクセスできます。このモードでは、32 ビットのレジスタ（EAX、EBX など）を使用して演算を行います。16 ビットおよび 8 ビットのレジスタも利用可能ですが、64 ビット専用のレジスタは使用できません。

32 ビットモードは、64 ビットアーキテクチャが普及する以前のシステムや、互換性を保つための環境でよく使用されていました。現在では、新しいシステムやソフトウェアでは 64 ビットモードが主流ですが、32 ビットモードをサポートすることで古いアプリケーションの動作を保証したり、メモリ要件が比較的小さいアプリケーションで利用されたりすることがあります。

### モードの選択

オペレーティングシステムやアプリケーションをインストールする際には、使用する CPU と互換性のあるモードを選択する必要があります。64 ビット OS を実行するには、64 ビット対応の CPU が必要ですが、多くの 64 ビット CPU は 32 ビットモードでも動作するため、古いソフトウェアとの互換性を保持しています。しかし、64 ビットモードでのみ利用できる機能や性能のメリットを活かすためには、64 ビット OS とアプリケーションの使用が推奨されます。

### レジスタの利用

アセンブリ言語プログラミングでは、これらのレジスタを直接操作してプログラムの振る舞いを制御します。例えば、算術演算の結果をレジスタに格納したり、関数呼び出しの引数としてレジスタの値を使用したりします。レジスタの利用方法は、プログラムの性能や効率に大きく影響するため、効果的なレジスタ利用はアセンブリ言語プログラミングの鍵となります。

NASM を利用した Intel x86 アセンブリ言語プログラミングでは、これらのレジスタに対する深い理解が必要です。レジスタの使い方を学ぶことは、効率的な低レベルプログラミングの基礎を築く上で不可欠です。

## 命令セットの概要

命令セット（Instruction Set）は、コンピュータの CPU が理解し実行できる命令の集合です。これらの命令は、プログラムを形成する基本的な操作であり、データの移動、算術演算、論理演算、プログラムの制御フローの管理（例えば、条件分岐やループ）、およびシステムコールなどの機能を実行するために使用されます。命令セットの設計は、そのプロセッサアーキテクチャの核心部分を形成し、プロセッサの性能、効率、およびプログラミングの柔軟性に直接影響を与えます。

### Intel x86 命令セットの特徴

Intel x86 アーキテクチャは、CISC（Complex Instruction Set Computing）アーキテクチャの一例であり、豊富な命令セットを特徴としています。この命令セットは、複雑な操作を単一の命令で実行できるように設計されており、以下のような特徴を持っています：
| 命令の種類 | 命令例 | 説明 |
|------------------|---------|----------------------------------------------------------------------------------|
| データ転送命令 | `MOV` | データをレジスタ間、レジスタとメモリ間で転送します。 |
| 算術命令 | `ADD` | 二つの値を加算します。 |
| | `SUB` | 一つの値から別の値を減算します。 |
| 論理命令 | `AND` | 二つの値のビット単位の AND を実行します。 |
| | `OR` | 二つの値のビット単位の OR を実行します。 |
| シフトおよびローテーション命令 | `SHL` | ビット列を左にシフトします。 |
| | `SHR` | ビット列を右にシフトします。 |
| 制御フロー命令 | `JMP` | 無条件で指定されたアドレスにジャンプします。 |
| | `JE` | 二つの値が等しい場合に指定されたアドレスにジャンプします。 |
| 文字列操作命令 | `MOVSB` | バイト単位で文字列をメモリの一つの場所から別の場所へ移動します。 |
| フローティングポイント演算 | `FADD` | 浮動小数点数の加算を行います。 |
| システム命令 | `CLI` | 割り込みを無効にします。 |
| | `STI` | 割り込みを有効にします。 |

### 命令セットの意義

命令セットは、プログラマやコンパイラが利用できるプロセッサの機能と能力を定義します。効率的なソフトウェア開発と最適化されたプログラムの実行には、使用される CPU の命令セットに対する理解が不可欠です。特にアセンブリ言語のプログラミングでは、これらの命令を直接扱うため、命令セットの詳細な知識が重要となります。

Intel x86 アーキテクチャの命令セットは、その豊富さと柔軟性から、幅広いアプリケーションに適用可能です。NASM を使用することで、これらの命令を直接制御し、特定のプログラミングタスクに対して高度に最適化されたコードを生成することができます。
