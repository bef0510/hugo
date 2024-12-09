+++
date = '2024-12-09T11:35:38+08:00'
draft = true
title = 'PowerShell7 Install Oh-My-Posh'
+++

## **PowerShell 7** 下載
[PowerShell網站](https://github.com/PowerShell/PowerShell/releases/tag/v7.4.6 "PowerShell 網站")

#### 1. 安裝 **PowerShell 7**
![](/images/powerShell7Install/01.png)
![](/images/powerShell7Install/02.png)

#### 2. 安裝 **Windows Terminal** 最新版
```
winget install Microsoft.WindowsTerminal --accept-source-agreements
```
![](/images/powerShell7Install/03.png)

#### 3. 安裝 **Oh My Posh**
```
winget install JanDeDobbeleer.OhMyPosh -s winget
```
![](/images/powerShell7Install/04.png)

#### 4. 重開 **PowerShell**

#### 5. 安裝 **Oh My Posh** 所需的字型
```
oh-my-posh.exe font install CascadiaCode
```
![](/images/powerShell7Install/05.png)

#### 6. 下載 **Nerdfonts** 字型
[Nerdfonts下載](https://www.nerdfonts.com/font-downloads "Nerdfonts 下載")
![](/images/powerShell7Install/06.png)

#### 7. 解壓縮 → 右鍵全選
![](/images/powerShell7Install/07.png)

#### 8. 安裝字型
![](/images/powerShell7Install/08.png)

#### 9. 開啟 **Windows Terminal**
![](/images/powerShell7Install/09.png)

#### 10. 開啟 **Windows Terminal** 設定
![](/images/powerShell7Install/10.png)

#### 11. 點選 預設值 → 外觀
![](/images/powerShell7Install/11.png)

#### 12. 點選 字體
![](/images/powerShell7Install/12.png)

#### 13. 新增 **$PROFILE** 檔
```
New-Item -Path $PROFILE -Type File -Force
```
![](/images/powerShell7Install/13.png)

#### 14. 開啟 **$PROFILE** 檔
```
notepad $PROFILE
```
![](/images/powerShell7Install/14.png)

#### 15. 修改 **$PROFILE** 檔
```
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json"  | Invoke-Expression
```
![](/images/powerShell7Install/15.png)

## VS Code 修改亂碼

#### 1. **VS Code** Ctrl+p
![](/images/powerShell7Install/16.png)

#### 2. 選取 **settings.json**
```
>settings
```
![](/images/powerShell7Install/17.png)

#### 3. 安裝 **Termial Icons**
```
Install-Module -Name Terminal-Icons -Repository PSGallery -Force
```
![](/images/powerShell7Install/18.png)

#### 4. 開啟 **$PROFILE** 檔
```
notepad $PROFILE
```

#### 5. 修改 **$PROFILE** 檔 (Icons)
```
Import-Module Terminal-Icons
```
![](/images/powerShell7Install/19.png)

#### 6. 修改 **$PROFILE** 檔 (記錄10個指令)
```
Set-PSReadLineOption -PredictionViewStyle ListView
```
![](/images/powerShell7Install/20.png)

## 參考
[美化你的 Windows Terminal (oh-my-posh, history autocomplete, terminal icons)](https://youtu.be/yKiOVSu9LQE "")