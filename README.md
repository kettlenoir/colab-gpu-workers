# 🚀 Colab GPU Workers

Google Colab の GPU（L4 / T4）を活用して、AGENT WEB から安全・高速に「LLMテキスト生成」「SDXL高精細画像生成」「AnimateDiff動作用生成」「Blender 3Dレンダリング」を実行するための実行ノートブック集です。

---

## 📑 収録ノートブック一覧（ワンクリック起動）

| 機能 | ノートブック | 推奨GPU | 起動リンク |
| :--- | :--- | :--- | :--- |
| **LLM テキスト生成 (GGUF / Qwen3.8等)** | `llm.ipynb` | **L4 GPU** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kettlenoir/colab-gpu-workers/blob/main/llm.ipynb) |
| **SDXL 高精細画像生成 (1024px基準)** | `sdxl.ipynb` | **L4 / T4** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kettlenoir/colab-gpu-workers/blob/main/sdxl.ipynb) |
| **動作用生成 (AnimateDiff / 16フレーム)** | `motion.ipynb` | **T4 / L4** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kettlenoir/colab-gpu-workers/blob/main/motion.ipynb) |
| **Blender 4.x 3Dレンダリング (Cycles / Eevee)** | `blender.ipynb` | **T4 / L4** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kettlenoir/colab-gpu-workers/blob/main/blender.ipynb) |

---

## 🌟 特徴

- **Google 公式 SSH 接続対応（キー入力不要）**:
  外部中継サーバ（Cloudflare）を介さず、Google 公式 WebSocket + OpenSSH で完全な閉域・暗号化トンネル（`http://127.0.0.1:8765`）直結。AGENT WEB 側からは接続キーの入力も不要でワンクリック自動接続されます。
- **最新 Colab 環境の完全適合**:
  CUDA 12 / 13 自動判別、`libcudart.so.12` 未検出エラー防止、`fileno` 例外回避、Google Drive FUSE ハング対策を完備。
- **AGENT WEB との完全連動**:
  各ワーカーの推論・生成結果は自動的にローカル VM 側へ保存・管理されます。

---

## 📖 使い方

1. 上の表の **[Open in Colab]** バッジをクリックして目的のノートブックを開きます。
2. ノートブック上部のランタイム設定で、推奨 GPU（L4 または T4）を選択します。
3. セルを上から順に実行します。
4. AGENT WEB（`#colab` 画面）の「接続する (自動取得)」ボタンを押すと接続完了します。

---

## 🔒 セキュリティ
- 認証キーはランタイム起動ごとに `secrets.token_urlsafe(32)` で使い捨て生成されます。
- 個人設定、SSH秘密鍵、APIキー等の秘匿情報はリポジトリおよびノートブック内に一切含まれません。
