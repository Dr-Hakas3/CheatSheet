# treeコマンド

```bash
tree -l -L 3 /usr/share/wordlists
```

# 圧縮・解凍

#### .zip

##### 圧縮

```bash
zip archive.zip file.txt
```

##### 解凍

```bash
unzip test.zip
```


#### .gz

##### 圧縮

```bash
# .gzの圧縮コマンドがありませんでしたので、必要であれば追記してください。
```

##### 解凍

```bash
gzip -d file.gz
```
### .tar
#### 圧縮
```bash
tar -zvf archive_name.tar /path/to/directory_or_files
```
#### 解凍
```bash
tar -xvf archive_name.tar.gz /path/to/directory_or_files
```
#### .tar.gz

##### 圧縮

```bash
tar -zcvf xxxx.tar.gz directory
```

##### 解凍

```bash
tar -xzvf filename.tar.gz
```

#### .tar.bz2
##### 圧縮
```bash
tar -jcvf xxxx.tar.bz2 directory
```
##### 解凍
```bash
tar -jxvf xxxx.tar.bz2
```
#### 7zip
```bash
# 7zipのコマンドがありませんでしたので、必要であれば追記してください。
```

### viエディタ

#### 置換
1. フォーマット
```bash
:%s/aaa/bbb/g
```
2. ,(カンマ)を改行に置換
```bash
:%s/,/\r/g
```
---
### ls

#### lsのタイムスタンプを見やすくする

```bash
ls -l --time-style=long-iso
```

### awk
- ログ解析などに有用なコマンド
- awkはスペースでフィールドを区切る
- awk '条件 {処理}'
```bash
awk '/exe/  {print $0}'
```
exeのあるファイルを表示
```bash
awk '{print $6}' wordpress.log | sort | uniq -c
```
### sed
####標準入力からバックスラッシュを削除
```bash
echo "User\\Name" | sed 's/User\\//g'
```
このコマンドを実行すると、「UserName」が出力されます。

#### ファイル内の「User」からバックスラッシュを削除
```bash

sed 's/User\\//g' inputfile.txt > outputfile.txt
```
#### awkとの組み合わせ
```bash
 awk '{print $3}' users.txt| sed 's/User\\//g'  > username.txt
```
#### Interface名を全変更
```bash
![image](https://github.com/user-attachments/assets/2f042e29-36ba-49dd-bf95-592a8c8a0e10)

```
---
### cp

```bash
# cpコマンドでディレクトリ内の中身のみ、他のディレクトリにコピーする 
cp -r dir1/. dir2/
```

### find

```bash
find / -name ファイル名
```

### grep

#### Recurs
```bash
grep -r hoge
```

#### AND

```bash
grep hoge | grep fuga
```

#### OR
```bash
grep -e hoge -e fuga
```
### echo

```bash
# hosts追記
echo "10.10.11.249 play.crafty.htb" | sudo tee -a /etc/hosts
```