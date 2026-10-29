# CLAUDE.md

## ブランチとPRの手順（コンフリクトを防ぐため）

PRはスカッシュマージ（変更を1つのコミットにまとめて main に入れる）している。
同じ作業ブランチを使い続けると、ブランチ側のコミットと main 側のまとめたコミットが
別の変更として扱われ、次のPRで `math/log.md` などがコンフリクトする。

1. **新しいissueを始める前に**、作業ブランチに最新の main を取り込む
   ```
   git fetch origin main
   git merge origin/main
   git diff origin/main --stat   # 何も出なければOK（ブランチ＝main）
   ```
   前のPRの内容は main にもブランチにも同じものがあるので、この時点ならコンフリクトしない。
   強制プッシュや rebase は使わない。
2. issueの作業（`math/log.md` のログ、必要なら `math/glossary.md` の用語）をコミットしてプッシュする
3. **PRを作る前に**、`git diff origin/main --stat` で差分がそのissueの分だけか確かめる。
   ほかの変更が混ざっていたら、先に 1 をやり直す
4. PRはスカッシュマージする。タイトルは「issue #番号 内容」の形
5. マージしたら、すぐに 1 をもう一度やってプッシュしておく
