# MOV, ADD, SUB 命令のサンプルコード

アセンブリ言語で MOV、ADD、SUB 命令を使って計算を行い、その結果を画面に表示するためには、システムコールを使用して標準出力に結果を出力する必要があります。ここでは、簡単な計算を行い、その結果を数値ではなく、結果の数値を示す文字列として画面に表示するサンプルコードを示します。この例では、x86-64 Linux システムを対象としています。

```asm
section .data
    msg db 'Result: ', 0   ; 結果を表示するためのメッセージプレフィックス
    msgLen equ $ - msg     ; メッセージプレフィックスの長さ
    resultTemplate db '0', 0xA, 0  ; 計算結果と改行を含むテンプレート
    resultTemplateLen equ $ - resultTemplate ; 計算結果文字列の長さ

section .text
    global _start

_start:
    ; 数値の準備
    mov rax, 5             ; RAXレジスタに5をセット
    mov rbx, 3             ; RBXレジスタに3をセット

    ; 計算: (5 + 3 - 2) = 6
    add rax, rbx           ; RAX += RBX (5 + 3)
    sub rax, 2             ; RAX -= 2 (8 - 2)

    ; 計算結果をASCII文字に変換してresultTemplateに格納
    add rax, '0'           ; 計算結果をASCIIに変換
    mov [resultTemplate], al  ; resultTemplateに格納

    ; 結果メッセージのプレフィックスを表示
    mov rax, 1             ; sys_write
    mov rdi, 1             ; 標準出力
    mov rsi, msg           ; メッセージプレフィックスのアドレス
    mov rdx, msgLen        ; メッセージプレフィックスの長さ
    syscall                ; システムコールを実行
    ; 計算結果を表示
    mov rax, 1             ; sys_write
    mov rdi, 1             ; 標準出力
    mov rsi, resultTemplate ; 計算結果のアドレス
    mov rdx, resultTemplateLen ; 計算結果文字列の長さ
    syscall                ; システムコールを実行

    ; プログラムを終了
    mov rax, 60            ; sys_exit
    xor rdi, rdi           ; 終了ステータス0
    syscall                ; システムコールを実行
```

このサンプルコードでは、5 と 3 を足し合わせた後に 2 を引くという単純な計算を行い、その結果（6）を画面に表示します。計算結果は num バッファに ASCII 文字として格納され、sys_write システムコールを使用して標準出力に表示されます。この例では、計算結果を直接数値として出力するのではなく、結果を ASCII 文字に変換しています。これは、アセンブリ言語において数値を直接テキストとして出力する機能がないためです。

- ASCII については https://wikipedia.org/wiki/ASCII を参照してください。

このコードは NASM でアセンブルし、ld でリンクすることができます。実行すると、画面に Result: 6 と表示されます。このサンプルは基本的な例であり、より複雑な数値や計算結果を扱う場合は、数値を文字列に変換するための追加のロジックが必要になります。

## 2 桁の数値の出力

2 桁の数値を出力するためには、数値を 10 で割って商と余りを得ることで、各桁を ASCII 文字に変換して表示する必要があります。具体的には、数値を 10 で割った商が十の位、余りが一の位になります。それぞれを'0'（ASCII コードで 48）に加えて ASCII の数字に変換し、その結果を出力用のバッファに格納してから表示します。

以下に示すのは、入力された数値が 2 桁であると仮定し、それを sys_write を用いて出力するための NASM のコード例です。ここでは計算結果が 2 桁であることを前提としていますが、実際の使用状況に応じて計算部分は適宜調整してください。

```asm
section .data
    msg db 'Result: ', 0     ; 結果を表示するためのメッセージプレフィックス
    msgLen equ $ - msg       ; メッセージプレフィックスの長さ
    resultTemplate db '00', 0xA, 0  ; 計算結果と改行を含むテンプレート、2桁対応
    resultTemplateLen equ $ - resultTemplate ; 計算結果文字列の長さ

section .text
    global _start

_start:
    ; 2桁の数値の準備（例として96を使用）
    mov rax, 96            ; RAXレジスタに96をセット

    ; 十の位を計算
    mov rdx, 0             ; RDXを0に初期化（DIV前に高位をクリア）
    mov rbx, 10            ; RBXレジスタに10をセット（除数）
    div rbx                 ; RAXをRBXで割り、商をRAXに、余りをRDXに格納

    ; 十の位をASCII文字に変換してresultTemplateに格納
    add al, '0'            ; 商（十の位）をASCIIに変換
    mov [resultTemplate], al  ; resultTemplateの十の位に格納

    ; 一の位（DIVの余りがRDXに格納されている）をASCII文字に変換して格納
    add dl, '0'            ; 余り（一の位）をASCIIに変換
    mov [resultTemplate+1], dl ; resultTemplateの一の位に格納

    ; 結果メッセージのプレフィックスを表示
    mov rax, 1             ; sys_write
    mov rdi, 1             ; 標準出力
    mov rsi, msg           ; メッセージプレフィックスのアドレス
    mov rdx, msgLen        ; メッセージプレフィックスの長さ
    syscall                ; システムコールを実行

    ; 計算結果を表示
    mov rax, 1             ; sys_write
    mov rdi, 1             ; 標準出力
    mov rsi, resultTemplate ; 計算結果のアドレス
    mov rdx, resultTemplateLen ; 計算結果文字列の長さ
    syscall                ; システムコールを実行

    ; プログラムを終了
    mov rax, 60            ; sys_exit
    xor rdi, rdi           ; 終了ステータス0
    syscall                ; システムコールを実行
```

### memo:

https://www.mycompiler.io/ja/new/asm-x86_64
ここでも実行できます。
