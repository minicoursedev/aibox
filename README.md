# AIBox

以實體裝置燈號提示 AI 回覆結束或授權請求，透過搖動／聲音事件讓桌面端開啟對應對話。

## 專案組成

| Repository | 職責 |
|---|---|
| [aibox-mac](https://github.com/minicoursedev/aibox-mac) | macOS 選單列 App、通知、SSH 連線管理與 BLE |
| [aibox-firmware](https://github.com/minicoursedev/aibox-firmware) | XIAO nRF52840 Sense 韌體、LED 與感測器 |
| [aibox-remote](https://github.com/minicoursedev/aibox-remote) | 遠端通知安裝與轉送 Python 程式 |
| [aibox-spec](https://github.com/minicoursedev/aibox-spec) | 共用規格、通訊協定與驗證紀錄 |

Windows App 尚未建立。此 repo 是整合入口，以 Git submodule 固定各元件的 commit。

## 取得完整工作目錄

需要對各私有 repo 有讀取權限，並設定 GitHub SSH 金鑰。

```sh
git clone --recurse-submodules git@github.com:minicoursedev/aibox.git
cd aibox
```

既有 checkout 更新後，執行：

```sh
git submodule update --init --recursive
```

## 開發與驗證

```sh
cd aibox-mac
swift test
zsh scripts/build-app.sh
```

遠端程式測試：`python3 aibox-remote/tests/test_notify.py`。
韌體主機測試：`bash aibox-firmware/tests/run.sh`。

Mac 在 `Sources/AIBoxCore/Remote` 另以 submodule 引用同一個 `aibox-remote` repo，讓單獨 clone Mac repo 時也能打包。更新遠端程式後，需同步更新 Mac 內與本入口的引用至同一 commit。

各元件應先在自己的 repo 提交與推送，再於本入口提交 submodule 版本變更。本入口的 commit 記錄一組元件版本，不代表硬體全流程已驗證；實機驗證狀態請查閱 aibox-spec。

## 發行

目前提供原始碼，尚未建立版本標籤或 GitHub Release。日後元件可各自發行 App／韌體，入口再記錄相容版本與下載連結。
