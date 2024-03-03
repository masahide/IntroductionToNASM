# MOV命令の説明


MOV命令は、プログラミングにおける最も基本的かつ頻繁に使用される命令の一つです。この命令の役割は「データの転送」です。具体的には、あるデータをレジスタからメモリに、メモリからレジスタに、またはレジスタやメモリに即値（プログラムに直接記述された数値）をコピーします。しかし、メモリからメモリへ直接データを転送することはできません。この制限は、アドレスバスが同時に指定できるメモリアドレスを一つしか持てないためです。

MOV命令は、2つのオペランド（引数）を取ります。これらのオペランドは「転送元(SRC)」と「転送先(DEST)」です。命令の形式は以下の通りです：


```asm
mov dest, src
```
ここで、`dest`は転送先（レジスタまたはメモリ）、`src`は転送元（レジスタ、メモリ、または即値）です。ただし、転送元と転送先が共にメモリである場合は除きます。

例えば、レジスタ間でデータを転送するには：
```
mov eax, ebx
```
この命令は、`ebx`レジスタの内容を`eax`レジスタにコピーします。また、即値をレジスタに転送するには：

```
mov eax, 10
```

この命令は、数値`10`を`eax`レジスタにコピーします。

## 注意点：
- メモリからメモリへの直接転送はできません。
- 転送元と転送先は同じサイズ（バイト数）でなければなりません。例えば、32ビットのレジスタには32ビットのデータを、8ビットのレジスタには8ビットのデータを転送する必要があります。
- セグメントレジスタへの直接転送やセグメントレジスタ間での転送は特別な命令を使用する必要があります。

これらの基本を理解することで、NASMを使用したプログラミングの基礎を固めることができます。次のページでは、これらの命令の実際の使用法やさらなる注意事項について詳しく説明します。


## 例1: AHレジスタに「2」を代入する
LinuxのNASMでは、32ビットまたは64ビットレジスタを使用しますが、ここでは具体例として32ビットレジスタの操作を示します。8ビットのAHレジスタに直接値を代入する代わりに、32ビットのEAXレジスタの上位8ビットを操作する方法を紹介します。NASMでは次のように記述します：

```
mov al, 2
```

この命令は、EAXレジスタの下位8ビット（AL）に数値`2`を代入します。AHレジスタを直接操作する代わりに、AL（EAXの下位8ビット）を使用しています。これは、NASMでのプログラミングでは、主に32ビットまたは64ビットレジスタを使用するためです。

## 例2: CLレジスタにAHレジスタの内容をコピーする
同じく、NASMで32ビットレジスタを使用する場合の例を見てみましょう。AHレジスタからCLレジスタへの直接転送は、下位8ビットレジスタALとCLを使用して表現します。NASMでは次のように記述します：


```
mov cl, al
```

この命令は、EAXレジスタの下位8ビット（AL）の内容を、ECXレジスタの下位8ビット（CL）にコピーします。ここでも、直接AHを使用する代わりにALを使用している点に注意してください。これにより、NASMの文脈で正しいレジスタ操作を行うことができます。


# 2-2. コンパイル

Linuxの環境では、プログラムを終了してOSに制御を戻すための処理も含めて、プログラムを作成することが可能です。しかし、実際にプログラムを動かしてみる楽しみを味わうためには、いくつかの基本的な概念と手順を理解しておく必要があります。

Linuxでのプログラム実行形式は主に「.out」や「.elf」といった形式です。これらの形式は、様々なセグメントを持つことができ、データやプログラムコードを分けて管理することができます。バッチファイルやシンプルなバイナリファイルとは異なり、より複雑な構造を持つプログラムを作成することが可能です。

以下は、NASMを使用したシンプルなLinuxプログラムの例です。このプログラムは、画面に"A"と表示し、その後プログラムを終了します。

```asm
section .text
    global _start

_start:
    mov eax, 4          ; システムコール番号4（sys_write）
    mov ebx, 1          ; ファイル記述子1（標準出力）
    mov ecx, msg        ; メッセージのアドレス
    mov edx, len        ; メッセージの長さ
    int 0x80            ; システムコールを実行

    mov eax, 1          ; システムコール番号1（sys_exit）
    xor ebx, ebx        ; 終了ステータス0
    int 0x80            ; システムコールを実行

section .data
msg db 'A',0xA         ; メッセージ"A"と改行
len equ $ - msg        ; メッセージの長さを計算
```

このプログラムをコンパイルして実行可能な形式にするには、以下の手順を実行します。

1. プログラムをテキストエディタで書き、example.asmというファイル名で保存します。
2. NASMを使用してアセンブルします。
```bash
nasm -f elf example.asm
```
3. ldを使用してリンクします。
```bash
ld -m elf_i386 -s -o example example.o
```
4. 実行します。
```bash
./example
```
画面に"A"と表示されたら成功です。
このプロセスを通じて、初心者もLinux環境でアセンブリ言語プログラミングの基本を学び、自分のプログラムをコンパイルして実行する楽しみを味わうことができます。


# 2-3. 即値の転送

即値の転送は、定数をレジスタやメモリに転送する操作を指します。専門用語で「イミディエイトモード」と呼ばれることもありますが、名称はさておき、この概念はプログラミングにおいて非常に基本的です。

LinuxのNASMでプログラミングをする際、さまざまな数値表現を使うことができます。これには10進数、16進数、8進数、2進数、文字コード、メモリアドレスなどが含まれます。ここでは、NASMでこれらの表現をどのように扱うかを説明します。

```asm
; 10進数で即値をレジスタに転送
mov eax, 10 ; EAXレジスタに、10進数で10を代入します

; 16進数で即値をレジスタに転送
mov eax, 0x10 ; EAXレジスタに、16進数で10(10進数で16)を代入します

; 8進数表現はNASMでは直接サポートされていません

; 2進数で即値をレジスタに転送
; NASMでは直接2進数表記はサポートされていないため、16進数または10進数を使用

; 文字コードで即値をレジスタに転送
mov al, 'A' ; ALレジスタに、'A'の文字コード(10進数で65、16進数で41)を代入します

; メモリアドレスをレジスタに転送
; 例えば、データセクション内のラベルアドレスを転送する
mov eax, data_label ; EAXレジスタに、data_labelのアドレスを代入します
```
「mov ax, 'A'」のように記述した場合、NASMでは「'A'」は16進数の41に相当し、その値をAXレジスタに代入することになります。NASMでは、16ビットレジスタへの直接的な文字代入はサポートされていないため、この操作はmov ax, 0x41と等価であり、結果としてAXの下位バイト（AL）に41hが代入されます。

これらの例を通して、NASMでの即値の転送方法と、さまざまな数値表現の使用方法について理解を深めることができます。各操作でどのようなデータがレジスタに転送されるかを把握することは、効率的なアセンブリ言語プログラミングにおいて重要です。


# 2-4. メモリへの転送

メモリへの転送（またはメモリからの転送）には、「直接アドレス法」と「間接アドレス法」の2つの方法があります。

## 2-4-1. 直接アドレス法

直接アドレス法は、メモリの特定のアドレスにデータを転送する方法です。たとえば、変数`DATA`に`al`レジスタの内容を転送する場合、NASMでは次のように記述します。

```asm
mov [DATA], al
```
特定のアドレスにデータを書き込む場合は、アドレスを[]で囲みます。

```asm
mov [0x1000], al
```
メモリに即値を代入する場合、その値がバイト、ワード、ダブルワードのどれであるかを明示する必要があります。レジスタのサイズは既知ですが、メモリへの即値転送ではサイズを指定する必要があります。NASMでは以下のように記述します。

```asm
mov byte [DATA], 0
mov word [DATA], 0
```
## 2-4-2. 間接アドレス法
間接アドレス法は、レジスタを使用してメモリアドレスを指定する方法です。これはC言語の「ポインタ」に似ています。

```asm
mov ebx, DATA
mov byte [ebx], 0
```
NASMでは、さまざまなレジスタを使用してメモリアドレスを指定できます。これにはebx、esi、ediなどが含まれます。また、オフセット（disp）を使用してアドレスを計算することも可能です。

## 2-4-3. ワード以上の単位の場合の注意
ワードやダブルワードのような大きなサイズでメモリにデータを格納する場合、エンディアン性に注意する必要があります。x86系CPUでは、リトルエンディアン方式を採用しており、低位のバイトが低いアドレスに格納されます。

例えば、0x1000番地にワード値0x1234を格納する場合、実際には0x1000番地に0x34が、0x1001番地に0x12が格納されます。ダブルワードの場合も同様で、0x12345678を格納すると、0x1000番地から順に0x78、0x56、0x34、0x12が格納されます。

```asm
mov [0x1000], word 0x1234
```
このように、NASMを使用したアセンブリ言語プログラミングでは、メモリへの転送方法とデータのサイズ、エンディアン性に注意してコーディングする必要があります。


## 例
以下の例では、LinuxのNASMを使用して、「A」と表示するプログラムを直接アドレス法と間接アドレス法で書き換えたバージョンを示します。これらの例は、前に紹介したシンプルなプログラムと同様の動作をしますが、データの転送方法に注目してください。

### 直接アドレス法の例

```asm
section .data
DATA    db 'A', 0xA      ; 'A'と改行のデータ定義

section .text
    global _start

_start:
    mov eax, 4          ; システムコール番号4（sys_write）
    mov ebx, 1          ; ファイル記述子1（標準出力）
    lea ecx, [DATA]     ; DATAのアドレスをECXにロード
    mov edx, 2          ; データの長さ（'A' + 改行）
    int 0x80            ; システムコールを実行

    mov eax, 1          ; システムコール番号1（sys_exit）
    xor ebx, ebx        ; 終了ステータス0
    int 0x80            ; システムコールを実行
```

### 間接アドレス法の例
```asm
section .bss
buffer  resb 1          ; 1バイトのバッファを確保

section .data
DATA    db 'A', 0xA      ; 'A'と改行のデータ定義

section .text
    global _start

_start:
    mov al, [DATA]      ; DATAから1バイト読み込み
    mov [buffer], al    ; bufferにalの内容を書き込み

    mov eax, 4          ; システムコール番号4（sys_write）
    mov ebx, 1          ; ファイル記述子1（標準出力）
    lea ecx, [buffer]   ; bufferのアドレスをECXにロード
    mov edx, 2          ; データの長さ（'A' + 改行）
    int 0x80            ; システムコールを実行

    mov eax, 1          ; システムコール番号1（sys_exit）
    xor ebx, ebx        ; 終了ステータス0
    int 0x80            ; システムコールを実行
```
DATA byte 'A'は、変数DATAに初期値として'A'の文字コードを設定する命令です。NASMにおいて、ラベル（変数名など）はアルファベット、数字、一部の記号を含むことができますが、数字では始まらず、予約語やアセンブラの命令を使用することはできません。大文字と小文字は区別されないことが多いですが、これは使用するアセンブラに依存します。一般的に、アンダースコア以外の記号は特別な用途に使われることが多いため、避けることが推奨されます。



# 2-5. データ定義疑似命令

NASMでのプログラミングでは、疑似命令を使ってアセンブラに特定の指示を出すことがよくあります。疑似命令はCPUに対する命令ではなく、アセンブリ言語のソースコードをどのようにアセンブル（コンパイル）するかをアセンブラに指示するための命令です。たとえば、データセグメントの開始を宣言する`section .data`やCPUの種類を指定するディレクティブなどがこれにあたります。

データを定義するために、NASMでは以下のような疑似命令が利用されます：

- バイト型データの定義には`db`（Define Byte）を使用します。これは1バイト（8ビット）のデータを定義します。
```asm
  DATA    db 'A'            ; Aの文字コードを持つ1バイトのデータ
  MESSAGE db 'This is a pen!', 0  ; 文字列の終端にヌル文字を追加
  COUNT   db 5, 10, 30      ; 3つの数値を持つバイト型データ
```
ワード型（2バイト型）データの定義にはdw（Define Word）を使用します。

```asm
VALUE   dw 0x1234         ; 16ビット（2バイト）のデータ
```
ダブルワード型（4バイト型）データの定義にはdd（Define Double word）を使用します。

```asm
NUMBER  dd 0x12345678     ; 32ビット（4バイト）のデータ
```
クアッドワード型（8バイト型）データの定義にはdq（Define Quad word）を使用します。

```asm
BIG_NUM dq 0x123456789ABCDEF0  ; 64ビット（8バイト）のデータ
```
テンバイト型（10バイト型）データの定義にはdt（Define Ten bytes）を使用します。これは主に浮動小数点数を扱う際に使用されます。

大きなデータ領域を定義し、特定の値で初期化したい場合にはDUP（Duplicate）疑似命令を使用します。

```asm
DATA_AREA db 100 DUP(0)    ; 100バイトのデータ領域を0で初期化
```
不定値を持つデータ領域を定義するには?を使用します。これは特に初期化する値が決まっていない場合に便利です。

```asm
UNDEFINED db ?, ?, ?       ; 不定値で初期化された3バイトのデータ
```
これらの疑似命令を使用することで、アセンブリ言語プログラム内で必要なデータ領域を効率的に定義し、初期化することができます。NASMではこれらの疑似命令を用いて、バイトから大きなデータ構造まで、さまざまなサイズと形式のデータを柔軟に扱うことが可能です。



# 演習問題
DATA1の内容(ABCD)をDATA2にコピーして、DATA2を表示するプログラムを作りたい。下記の空欄を埋めよ。(ただし、DATA1とDATA2の後ろにある24hは気にしなくても良い)

```asm
section .data
DATA1   db 'ABCD', 0x24   ; 末尾の0x24は気にしなくても良い
DATA2   db '0000', 0x24   ; コピー先のデータ、同じく末尾は0x24

section .text
    global _start

_start:
    ; DATA1の内容をDATA2にコピー
                         ; ESIレジスタにDATA1のアドレスを設定
                         ; EDIレジスタにDATA2のアドレスを設定
                         ; コピーするデータのサイズ（4バイト）
                         ; バイト単位でデータをコピー

    ; DATA2を表示する
    mov eax, 4           ; システムコール番号4（sys_write）
    mov ebx, 1           ; ファイル記述子1（標準出力）
    mov ecx, DATA2       ; 表示するデータのアドレス
    mov edx, 4           ; 表示するデータのサイズ（4バイト）
    int 0x80             ; システムコールを実行

    ; プログラムを終了
    mov eax, 1           ; システムコール番号1（sys_exit）
    xor ebx, ebx         ; 終了ステータス0
    int 0x80             ; システムコールを実行
```
### 穴埋め部分のヒント:

- 最初の空欄は、DATA1のアドレスを指すレジスタの設定に関する命令です。
- 2番目の空欄は、DATA2のアドレスを指すレジスタの設定に関する命令です。
- 3番目の空欄は、コピーするデータのバイト数を指定する命令です。
- 4番目の空欄は、実際にデータをコピーする命令です。

これらの穴埋め問題を解くことで、学習者はメモリ間でのデータ転送方法についての理解を深めることができます。


