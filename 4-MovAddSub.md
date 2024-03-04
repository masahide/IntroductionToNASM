# MOV, ADD, SUB命令のサンプルコード

アセンブリ言語でMOV、ADD、SUB命令を使って計算を行い、その結果を画面に表示するためには、システムコールを使用して標準出力に結果を出力する必要があります。ここでは、簡単な計算を行い、その結果を数値ではなく、結果の数値を示す文字列として画面に表示するサンプルコードを示します。この例では、x86-64 Linuxシステムを対象としています。
```asm
section .data
    msg db 'Result: ', 0   ; 結果を表示するためのメッセージプレフィックス
    resultTemplate db '0', 0xA, 0  ; 計算結果と改行を含むテンプレート

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
    mov rdx, 9             ; メッセージプレフィックスの長さ
    syscall                ; システムコールを実行

    ; 計算結果を表示
    mov rax, 1             ; sys_write
    mov rdi, 1             ; 標準出力
    mov rsi, resultTemplate ; 計算結果のアドレス
    mov rdx, 3             ; 計算結果文字列の長さ（数字 + 改行 + null終端）
    syscall                ; システムコールを実行

    ; プログラムを終了
    mov rax, 60            ; sys_exit
    xor rdi, rdi           ; 終了ステータス0
    syscall                ; システムコールを実行
```

このサンプルコードでは、5と3を足し合わせた後に2を引くという単純な計算を行い、その結果（6）を画面に表示します。計算結果はnumバッファにASCII文字として格納され、sys_writeシステムコールを使用して標準出力に表示されます。この例では、計算結果を直接数値として出力するのではなく、結果をASCII文字に変換しています。これは、アセンブリ言語において数値を直接テキストとして出力する機能がないためです。

このコードはNASMでアセンブルし、ldでリンクすることができます。実行すると、画面にResult: 6と表示されます。このサンプルは基本的な例であり、より複雑な数値や計算結果を扱う場合は、数値を文字列に変換するための追加のロジックが必要になります。
