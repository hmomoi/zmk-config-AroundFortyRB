# zmk-config-AroundFortyRB (zmk-v0.4 / DYA Studio)

Around Forty RB の ZMK v0.4（Zephyr 4.1）および DYA Studio 対応版ファームウェアです。

本ブランチは **ZMK v0.4 (Zephyr 4.1)** をベースに、Custom Studio Protocol によるキーマップ、Macro、Combo、PMW3610、ポインター処理のランタイム設定に対応します。

---

## 主な実装内容・特徴

### 🟢 ZMK v0.4 (Zephyr 4.1) への移行
- **最新 Zephyr 4.1 対応**: ZMK main（Zephyr 4.1 系統）を pin し、新規格に適合
- **新ボード定義形式への対応**: ボード指定を `xiao_ble//zmk`、インターコネクト ID を `seeed_xiao` に更新
- **Devicetree での NFC ピン GPIO 化**: Zephyr 4.1 での Kconfig 廃止に伴い、P0.09 / P0.10 の GPIO 再利用指定を DTS（`&uicr`）へ移行
- **外部モジュールの Zephyr 4.1 追従**:
  - `cormoran/zmk-driver-pmw3610-with-custom-studio-rpc`: PMW3610 の設定・診断を DYA Studio へ公開
  - `cormoran/zmk-module-runtime-input-processor`: ポインター、スクロール、回転、反転、一時レイヤーをランタイム設定
  - `caksoylar/zmk-rgbled-widget`: Zephyr 4.1 対応版へ更新

### 🟢 トラックボールおよび BLE 通信の最適化
- **トラックボール応答性・復帰速度の改善**: 報告間隔（15ms）の同期および復帰遅延チューニング
- **BLE スタックメモリ・バッファ最適化**: `CONFIG_BT_HCI_TX_STACK_SIZE_WITH_PROMPT=y` の適用など左右のスタック設定を最適化

### 🟢 DYA Studio 対応
- `studio-rpc-usb-uart` スニペットを有効化し、USB 接続時のリアルタイムキーマップ編集に対応
- Runtime Macro / Combo、Fast Keymap、拡張 Physical Layout に対応
- PMW3610 の CPI・省電力設定と、ポインター／スクロール処理をブラウザから変更可能
- BLEプロファイル管理と、接続先／OSごとの Win-Base・Mac-Base 自動切り替えに対応
- アイドル／スリープ設定をブラウザから変更可能
- Device Info、Watchdog incident、左右KSCAN topology／統計の診断に対応
- Studio への書き込みは Settings レイヤーの `&studio_unlock` 実行後だけ許可
- Device Info、Watchdog、KSCAN診断もStudio Unlock後だけ参照可能
- 押下キーをブラウザへ送る `zmk-feature-input-stream` はプライバシーを考慮して無効

### 🟢 全角半角の切り替えマクロ
- `ime_tog` マクロにより、1 つのキーで日本語入力の全角/半角トグル切り替えが可能

---

## 保留事項
- 🟡 **Prospector Scanner**: Bluetooth 接続の安定性を最優先するため、本ブランチでも非対応としています

---

## ご利用ガイド

キーボードの使い方や設定の詳細は以下をご参照ください。

- [ご利用ガイド (note)](https://note.com/razily/n/n0b3c5ff58d92)
