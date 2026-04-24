```bash
# 1. DNSサービスのバージョン検出
nmap -sV -p 53 dns.example.com
```

```zsh
# 2. DNS特有のスクリプトを使用して脆弱性をチェック
nmap --script dns-zone-transfer,dns-cache-snoop,dns-brute -p 53 dns.example.com
```
スクリプトの詳細:
- **dns-zone-transfer**: ゾーン転送を試みて、DNSサーバーの全情報を取得します。
- **dns-cache-snoop**: DNSキャッシュに保存された情報を取得します。
- **dns-brute**: DNSサーバーに対してブルートフォース攻撃を行い、サブドメインを列挙します。
---
# サブドメインの列挙
DNSサーバーに対してブルートフォース攻撃を行い、サブドメインを列挙する方法です。

```bash
# dns-bruteスクリプトを使用してサブドメインを列挙
nmap --script dns-brute -p 53 dns.example.com
```

- **dns-brute**: サブドメインを列挙するためのNmapスクリプトです。

### Bashスクリプトによるドメイン名探索
指定したIPレンジ内でアクティブなホストを見つけるためのスクリプトです。

```bash
# 指定したIPレンジ内でアクティブなホストを検索
for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"
```

- **seq 200 254**: IPアドレスの範囲を指定します。
- **host 51.222.169.$ip**: 各IPアドレスに対してDNS情報を取得します。
- **grep -v "not found"**: DNSが見つからなかったホストを除外します。

### `dnsrecon`ツールによる情報収集
`dnsrecon`は、DNSリコンサンスを行うためのツールで、さまざまなDNS情報を収集します。

```bash
# 基本的なドメイン情報の収集
dnsrecon -d example.com

# サブドメインの列挙
dnsrecon -d example.com -t brt

# ゾーン転送のチェック
dnsrecon -d example.com -t axfr
```

- **-d**: 対象ドメインを指定します。
- **-t brt**: ブルートフォースによるサブドメイン列挙を実行します。
- **-t axfr**: ゾーン転送を試みます。
---

# DNS_Enumeration
### 各種レコード
- NS : ネームサーバー レコードには、ドメインの DNS レコードをホストする権限のあるサーバーの名前が含まれます。
- A : ホスト レコードとも呼ばれる「a レコード」には、ホスト名 (www.megacorpone.com など) の IPv4 アドレスが含まれます。
- AAAA : クアッド A ホスト レコードとも呼ばれる「aaaa レコード」には、ホスト名 (www.megacorpone.com など) の IPv6 アドレスが含まれます。
- MX：メール交換レコードには、ドメインのメール処理を担当するサーバーの名前が含まれます。ドメインには複数のMXレコードを含めることができます。
- PTR : ポインタ レコードは逆引き参照ゾーンで使用され、IP アドレスに関連付けられたレコードを見つけることができます。
- CNAME : 正規名レコードは、他のホスト レコードのエイリアスを作成するために使用されます。
- TXT : テキスト レコードには任意のデータを含めることができ、ドメイン所有権の検証など、さまざまな目的に使用できます。
### IPアドレス調査

```bash
host www.megacorpone.com
```
- デフォルトでAレコード
### レコードの指定
```bash
host -t mx megacorpone.com
```
```bash
host -t txt megacorpone.com
```
### DNS ブルートフォース攻撃手法の自動化
1. ホスト名リストを作成する
2. ワンライナーを使用して各ホスト名の解決
```bash
for ip in $(cat list.txt); do host $ip.megacorpone.com; done
```
### 逆引き検索 を用いてこの範囲をスキャンし、 各IPのホスト名を要求
```bash
for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"
```
### dnsrecon
```bash
dnsrecon -d megacorpone.com -t std
```
```bash
dnsrecon -d megacorpone.com -D ~/list.txt -t brt
```
- -D 潜在的なサブドメイン文字列を含むファイル名を指定する
- -t 列挙の種類 (この場合はbrtブルート フォース)

### DNSEnum
広範囲のDNS列挙
```bash
dnsenum megacorpone.com
```

### nslookup
```bash
nslookup mail.megacorptwo.com
```
特定のホストに属するTXTレコードについて、特定のDNSサーバにクエリを実行
```bash
nslookup -type=TXT info.megacorptwo.com 192.168.50.151
```