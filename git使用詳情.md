# 項目提交到Gitbub

## 創建項目

1. 右上角的+ New repository
2. 信息
   > - Repository name：倉庫名
   > - Descriptions：項目描述
   > - Public/Private：是否公開
   > - Initialize this repository with a README：如果要上傳本地項目，可以不選
3. Create repository

## 上傳項目

1. 項目根目錄右鍵`Git Bash`
2. 先檢查一下有沒有遠程倉庫`git remote -v`
   > 輸出為空，就説明沒有關聯
   > 如果已經有origin，再看看地址對不對
3. 執行
   ```git remote add origin https://github.com/Yau-ShuoWen/Lexicon-of-Yuzhang-Android.git```
4. 執行
   ```git add .
   git commit -m "第一次提交"
   git branch -M main       # 把 master 改成 main
   git push -u origin main
   ```

----

# IDE配置Git

假設路徑在  `D:\install_route\git\Git\bin\git.exe`

- 在cmd中輸入 `D:\install_route\git\Git\bin\git.exe --version`，如果能輸出版本號就説明git本身沒問題
- IDE中`文件 → 設置 → 版本控制 → git → Path to Git executable`
- 填入`D:\install_route\git\Git\bin\git.exe`點擊TEST如果顯示則成功

# 使用SSH

打開git bash 輸入`ls -al ~/.ssh`


# 標記

調錯debug：🐛
說明：✏️



