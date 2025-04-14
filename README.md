# Eclipse-Tabnine

以下に、 **「Eclipse + Pleiades + Tabnine の共存環境構築手順」** を、チーム共有用にまとめました。  
**TabnineとPleiadesの競合回避**を意識しつつ、再現性高く構築できるように整理しています。
Tabnine　　https://www.tabnine.com/
---

# Eclipse + Pleiades + Tabnine セットアップ手順書（Windows版）

---

## 📌 対象読者

- Java開発に Eclipse を使っている方  
- Eclipse を日本語化（Pleiades）しつつ、Tabnine を導入したい方  
- ローカルLLMや補完ツールとの競合を回避しつつ使いたい方

---

## 🧭 手順の全体像

| ステップ | 内容 |
|----------|------|
| Step 1 | Eclipse（zip版）をダウンロードして配置する |
| Step 2 | Pleiades（日本語化プラグイン）を導入する |
| Step 3 | Eclipse起動・Pleiadesによる日本語化を確認 |
| Step 4 | Tabnine プラグインを導入する（Eclipse Marketplace経由） |
| Step 5 | Tabnineアカウント登録＆Pro機能連携 |
| Step 6 | AI補完とチャット機能の動作確認 |

---

## ✅ Step 1：Eclipse（zip版）をダウンロードして配置

1. 以下のURLから、安定版 Eclipse を zip 形式でダウンロード  
   👉 https://www.eclipse.org/downloads/packages/release/2024-09/r

2. 対象：
   ```
   Eclipse IDE for Java Developers（Windows 64bit ZIP版）
   ```

3. ダウンロードしたzipを解凍し、任意の場所に配置（例：`C:\eclipse`）

---

## ✅ Step 2：Pleiades プラグインの導入（日本語化）

1. 以下のURLから Pleiades プラグインを zip 形式でダウンロード  
   👉 https://mergedoc.osdn.jp/pleiades/

2. ダウンロード後、zipを解凍し、フォルダ内の以下をコピー：

   - `features/` フォルダ
   - `plugins/` フォルダ
   - `pleiades.ini`
   - `eclipse.exe -clean.cmd`（←起動用）

3. これらをすべて Eclipse インストールフォルダ（例：`C:\eclipse`）直下に**上書きコピー**

---

## ✅ Step 3：Eclipse 起動と日本語化の確認

- `eclipse.exe -clean.cmd` を**初回は必ず実行**すること  
- Pleiadesによって Eclipse が日本語化されていれば OK

---

## ✅ Step 4：Tabnine プラグインを導入（Eclipse Marketplace）

1. Eclipse メニューから：

   ```
   ヘルプ > Eclipse マーケットプレース
   ```

2. 検索欄に `Tabnine` と入力し、「インストール」をクリック  
   ※Marketplace 上で見つからない場合（2025年4月15日現在見つからない）：
   - 以下のURLから「Install」ボタンを Eclipse にドラッグ＆ドロップ  
     👉 https://marketplace.eclipse.org/content/tabnine-ai-assistant-chat-software-developers

3. ダイアログに従い、「確認」「同意」「再起動」で完了

---

## ✅ Step 5：Tabnine アカウント登録と連携

1. Tabnine公式ページで無料アカウント登録（メールアドレスでOK）  
   👉 https://app.tabnine.com/signup

2. Eclipse 上で下部にあるTabnine Dev をクリックし、`Open Hub` をクリック

3. ブラウザが開いたらログイン状態を確認  
   - Proトライアル中であれば AI補完（Cloud AI）とチャット機能が有効化される

---

## ✅ Step 6：補完・チャット動作確認

### 🔹 補完チェック

以下のようにコードを入力して確認：

```java
// 配列の平均を求める関数
public▍
```

- 灰色のゴーストテキストで `public static double average(int[] nums)` などが出れば Tabnine 補完が動作中

### 🔹 Tabnine Chat の起動

- Eclipse下部に `Tabnine Chat` タブが表示されていることを確認
- Claude や GPT ベースの LLMと会話可能

---

## ⚠️ 注意点（トラブル回避）

| 項目 | 対処法 |
|------|--------|
| Tabnine が UI に表示されない | `eclipse.exe -clean.cmd` で再起動する |
| Tabnine 設定画面が最小限しか出ない | Pro登録を行ってから再起動・再ログイン |
| Tabnine 補完が効かない | コメント補完が効くか試す。AI補完はProのみ対応 |
| TabnineとPleiadesの競合 | `-javaagent:...pleiades.jar` の順序に注意。Pleiadesは後に書く方が安全 |

---

## 📁 補足：共有時のフォルダ構成（例）

```
C:\eclipse
│
├─ eclipse.exe
├─ eclipse.ini
├─ pleiades.ini
├─ eclipse.exe -clean.cmd
├─ dropins\（空でもOK）
├─ plugins\（PleiadesとTabnine両方入り）
└─ workspace\HelloTabnine\（プロジェクト）
```

---

## ✅ 最終チェックリスト

- [x] Eclipseが日本語UIで起動する  
- [x] Tabnineが `設定 > Tabnine` に表示されている  
- [x] Tabnine Chat がタブとして使える  
- [x] コメントからの補完が灰色で出る  
- [x] アカウント連携済み（ブラウザで表示されている）

---
