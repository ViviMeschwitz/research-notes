# Day 13 — CS: bungouコード理解 + Anthropic API Fundamentals

## bungouコード理解
- page.tsxは現在1つだけ（SPA構造）
- page.tsxは「指揮者 」, 各componentsは「楽器」であり、この2者の関係は、オーケストラの指揮者が各楽器に「今お前が弾け」と指示するような関係と類似したものだ。
- インポート->VIew型->分岐機能

## Anthropic API Fundamentals
- Claudeをチャットによって使うことと、APIを用いることで使うことは全く同じ構造
- APIでClaudeに話しかけるには3つ必要：APIキー、モデル名、メッセージ
- APIキーは「家の鍵」。絶対に公開してはいけない。.envファイルに保存
- コースは全6回：getting_started(全体像), messages_format(会話の礼儀), models(Haiku, Sonnet, Opusの違い=相手の選択), parameters(temperatureなどの設定), Streaming(リアルタイムに応答を受け取る方法), vision(画像を見せる方法)