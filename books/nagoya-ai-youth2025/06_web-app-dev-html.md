---
title: "5-2. HTML"
---
いよいよ「三目並べ」を実際に作っていきます！
まずは「骨組み（HTML）」から作っていきましょう！

以下のプロンプトをChatGPTに入力し、HTMLのコードを出力してもらいます。

>index.html,style.css,script.jsを使って三目並べを作成してください。  
まずはhtmlだけを出力してください。

![](/images/nagoya2025/chatgpt-html-sanmoku.png)

送信すると、すぐにコードの出力が始まります。

出力されるコードは人によって違う場合があるため、必ずこの画像と同じにならなければならないということはありません。

コードの出力が終了したら、コードの右上にある「コピーする」を押してコピーします。

![](/images/nagoya2025/chatgpt-html-copy.png)

コピーができたらVSCodeに移り、 `index.html` に貼り付けます。  
Windowsでは `Ctrl+V` 、Macでは `⌘+V` で貼り付けることができます。

![](/images/nagoya2025/vscode-html-sanmoku-1.png)

出力されたコードが全て貼り付けられていればOK！

![](/images/nagoya2025/vscode-save-html.png)

コードの追加、削除、書き換えがあると、画面上部のファイル名の横に白丸が付きます。  

変更があったら、Windowsでは `Ctrl+S` 、Macでは `⌘+S` で**必ず保存**しておきましょう。

保存が完了したら、画面右下に小さく出ている `Go Live` をクリックしてブラウザで開いてみましょう。

![](/images/nagoya2025/vscode-golive-test-sanmoku-1.png)

三目並べのタイトルと、リスタートのボタンは表示されています。

ですが、マス目が表示されていないのでまだ「三目並べ」には見えませんね。

次にCSSを使って見た目を整えることでマス目を表示していきます！