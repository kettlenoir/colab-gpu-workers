# 🚀 Colab LLM Worker

Google Colab 上で任意の GGUF モデル（Huihui-Qwen3.8-27B、Qwen2.5-Coder、Llama-3、Mistral 等）をロードし、**Google 公式 SSH ポートフォワード**（または Cloudflare トンネル）経由で自宅の AGENT WEB から高速・安全にテキスト生成推論を行うための実行ノートブックです。

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kettlenoir/colab-llm-worker/blob/main/colab-llm-worker.ipynb)

---

## 🌟 特徴

- **Google 公式 SSH 接続対応**: 外部中継を一切介さず、Google 公式 WebSocket + OpenSSH で完全な閉域・暗号化トンネル（`http://127.0.0.1:8765`）直結。
- **最新 Colab 環境の完全適合**: CUDA 12 / 13 自動判別、`libcudart.so.12` 未検出エラー防止、`fileno` 例外回避、Google Drive FUSE ハング対策を完備。
- **GGUF 全層 GPU オフロード**: NVIDIA L4 GPU（24GB VRAM）を活用し、27B〜32B クラスの大型モデルも高速推論可能。
- **Colab フォーム (`#@param`) 搭載**: ノートブックのコードを触らずに、GUI フォームからモデルパスやコンテキスト長を切り替え可能。

---

## 📖 使い方

### 1. Google Drive の準備
Google Drive にフォルダ（例: `colab-model/`）を作成し、お好みの GGUF モデル（例: `Huihui-Qwen3.8-27B-abliterated-GSQ-RCO-IQ3_S.gguf`）を配置しておきます。

### 2. Colab でノートブックを開く
上記の **[Open in Colab]** バッジ、または Colab の「GitHub」タブからこのノートブックを開きます。
- ランタイムのタイプ: **L4 GPU**（推奨）を選択してください。

### 3. セルを上から順に実行
1. **1️⃣ 環境自動構築**: `llama-cpp-python` と CUDA 共有ライブラリを自動設定。
2. **2️⃣ Google Drive マウント & モデル選択・ロード**: フォームでモデル名・フォルダ・コンテキスト長を選択し、GPU へロード。
3. **3️⃣ 単体動作テスト（任意）**: Colab 単体で推論動作を確認。
4. **4️⃣ AGENT WEB 連携 Worker 起動**: ポート 8765 で待機サーバーを起動し、接続トークンを出力。

### 4. AGENT WEB 側での接続
ローカル VM のターミナルで SSH ポートフォワードを実行（バックグラウンド待機中の場合は不要です）:
```bash
ssh -N -f -L 8765:localhost:8765 colab
```
AGENT WEB の [Colab 管理画面](#colab) の「接続・ノートブック設定」で以下を登録します:
- **接続URL**: `http://127.0.0.1:8765`
- **接続キー**: セル4に出力されたトークン文字列

---

## 🔒 セキュリティ
- 認証キーはランタイム起動ごとに `secrets.token_urlsafe(32)` で使い捨て生成されます。
- 個人設定、SSH秘密鍵、APIキー等の秘匿情報はリポジトリおよびノートブック内に一切含まれません。
