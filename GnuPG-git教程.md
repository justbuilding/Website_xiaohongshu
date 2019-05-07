### 1.概念

程序生成地球上惟一的一对钥匙，分别称为公钥和私钥（即 public key 和 private/secret key）。公钥用于加密、私钥用于解密。使用公钥加密过的信息只能由配对的私钥解开。这种加密方式叫做非对称加密。

GnuPG 是一个集钥匙管理、加密解密、数字签名于一身的工具。Windows版下载网址：https://www.gpg4win.org

##### 安装GnuPG后记得配置环境，cmd输入gpg --help查看安装是否成功

```
C:\Users\jayq>gpg --help
gpg (GnuPG) 2.2.15
libgcrypt 1.8.4
Copyright (C) 2019 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: C:\Users\jayq\AppData\Roaming\gnupg
Supported algorithms:
Pubkey: RSA, ELG, DSA, ECDH, ECDSA, EDDSA
Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256
Hash: SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2

Syntax: gpg [options] [files]
Sign, check, encrypt or decrypt
Default operation depends on the input data

Commands:

 -s, --sign                  make a signature
     --clear-sign            make a clear text signature
 -b, --detach-sign           make a detached signature
 -e, --encrypt               encrypt data
 -c, --symmetric             encryption only with symmetric cipher
 -d, --decrypt               decrypt data (default)
     --verify                verify a signature
 -k, --list-keys             list keys
     --list-signatures       list keys and signatures
     --check-signatures      list and check key signatures
     --fingerprint           list keys and fingerprints
 -K, --list-secret-keys      list secret keys
     --generate-key          generate a new key pair
     --quick-generate-key    quickly generate a new key pair
     --quick-add-uid         quickly add a new user-id
     --quick-revoke-uid      quickly revoke a user-id
     --quick-set-expire      quickly set a new expiration date
     --full-generate-key     full featured key pair generation
     --generate-revocation   generate a revocation certificate
     --delete-keys           remove keys from the public keyring
     --delete-secret-keys    remove keys from the secret keyring
     --quick-sign-key        quickly sign a key
     --quick-lsign-key       quickly sign a key locally
     --sign-key              sign a key
     --lsign-key             sign a key locally
     --edit-key              sign or edit a key
     --change-passphrase     change a passphrase
     --export                export keys
     --send-keys             export keys to a keyserver
     --receive-keys          import keys from a keyserver
     --search-keys           search for keys on a keyserver
     --refresh-keys          update all keys from a keyserver
     --import                import/merge keys
     --card-status           print the card status
     --edit-card             change data on a card
     --change-pin            change a card's PIN
     --update-trustdb        update the trust database
     --print-md              print message digests
     --server                run in server mode
     --tofu-policy VALUE     set the TOFU policy for a key

Options:

 -a, --armor                 create ascii armored output
 -r, --recipient USER-ID     encrypt for USER-ID
 -u, --local-user USER-ID    use USER-ID to sign or decrypt
 -z N                        set 
 
 level to N (0 disables)
     --textmode              use canonical text mode
 -o, --output FILE           write output to FILE
 -v, --verbose               verbose
 -n, --dry-run               do not make any changes
 -i, --interactive           prompt before overwriting
     --openpgp               use strict OpenPGP behavior

(See the man page for a complete listing of all commands and options)

Examples:

 -se -r Bob [file]          sign and encrypt for user Bob
 --clear-sign [file]        make a clear text signature
 --detach-sign [file]       make a detached signature
 --list-keys [names]        show keys
 --fingerprint [names]      show fingerprints

Please report bugs to <https://bugs.gnupg.org>.
```



### 2.生成GPG密钥

##### 完全手动配置生成gpg：

```
$ gpg --full-generate-key
gpg (GnuPG) 2.2.13-unknown; Copyright (C) 2019 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 5y
Key expires at 2024年05月 5日  8:28:17
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: jayunq
Email address: 13415145594@163.com
Comment:
You selected this USER-ID:
    "jayunq <13415145594@163.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key 11F0A7A2121C66FB marked as ultimately trusted
gpg: revocation certificate stored as '/c/Users/jayq/.gnupg/openpgp-revocs.d/1D388D82EB02555C64FCE30411F0A7A2121C66FB.rev'
public and secret key created and signed.

pub   rsa4096 2019-05-07 [SC] [expires: 2024-05-05]
      1D388D82EB02555C64FCE30411F0A7A2121C66FB
uid                      jayunq <13415145594@163.com>
sub   rsa4096 2019-05-07 [E] [expires: 2024-05-05]
```

##### 或者按照默认配置生成：`

`gpg --gen-key`，根据提示，生成GPG key，注意：确保邮箱的那项是你github账号认证的邮箱；还有记住输入的密码。





### 3.配置git

###### 	



1. ###### 查看GPG key：

   ###### `（1）gpg --list-keys`
注意：sub:私钥；pub:公钥；右边才是GPG key ID

   ###### （2）或者gpg --list-secret-keys --keyid-format LONG（2.1以上版本用这个）

   ```
   $ gpg --list-secret-keys --keyid-format LONG
   gpg: checking the trustdb
   gpg: marginals needed: 3  completes needed: 1  trust model: pgp
   gpg: depth: 0  valid:   3  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 3u
   gpg: next trustdb check due at 2021-04-28
   
   ## /c/Users/jayq/.gnupg/pubring.kbx
   
   sec   rsa2048/22899DB6EC48C4D7 2019-04-29 [SC] [expires: 2021-04-28]
         F4424E54D2AC814DE457B97622899DB6EC48C4D7
   uid                 [ultimate] jayunq <13415145594@163.com>
   ssb   rsa2048/CDA6F72A5BF64516 2019-04-29 [E] [expires: 2021-04-28]
   
   sec   rsa2048/D4D156DC31875478 2019-05-05 [SC] [expires: 2021-05-04]
         EE68F1E93F45A825E4F04894D4D156DC31875478
   uid                 [ultimate] jayunq <13415145594@163.com>
   ssb   rsa2048/7FF29AAD1AD3850F 2019-05-05 [E] [expires: 2021-05-04]
   
   sec   rsa4096/11F0A7A2121C66FB 2019-05-07 [SC] [expires: 2024-05-05]
         1D388D82EB02555C64FCE30411F0A7A2121C66FB
   uid                 [ultimate] jayunq <13415145594@163.com>
   ssb   rsa4096/35A67043B17EFCC5 2019-05-07 [E] [expires: 2024-05-05]
   ```

2. ###### 查看公钥内容：gpg --armor --export 22899DB6EC48C4D7

   ```
   $ gpg --armor --export 22899DB6EC48C4D7
   -----BEGIN PGP PUBLIC KEY BLOCK-----
   
   mQENBFzGxIUBCACiimdHoAr35I0Si4F9hbQwt9efvJm6m1hlQzDeMNszyDNdo4u5
   ................................................................
   =HFfJ
   -----END PGP PUBLIC KEY BLOCK-----
   ```

3. ###### github设置GPG key

   ###### 	拷贝上面得到的公钥到github账号中，注意：格式如：

   -----BEGIN PGP PUBLIC KEY BLOCK-----（包含）

   mQENBFzGxIUBCACiimdHoAr35I0Si4F9hbQwt9efvJm6m1hlQzDeMNszyDNdo4u5
   ................................................................
   =HFfJ
   -----END PGP PUBLIC KEY BLOCK-----（包含）

   

4. ###### *导出公钥`：gpg -a -o gpg.public.export` --export-secret-keys 22899DB6EC48C4D7

5. ###### *git下的`gpg --import`分别导入公钥和私钥

6. ###### 设置git签名时用的key：`git config --global user.signingkey pub_GPG_key_ID`

7. ###### 开启GPG签名commit：`git config commit.gpgsign true`

8. ###### 关闭GPG签名commit：`git config commit.gpgsign false`

9. ###### 所有的本地仓库都使用GPG签名：`git config --global commit.gpgsign true`

## 4.查看当前文件正在使用的签名

​	git log --show-signature -1



	$ git log --show-signature -1
```
commit 3a7cbcc45a33a8ca14b83636168ee07e57437cd1 (HEAD -> master, origin/master, origin/HEAD)
gpg: Signature made 2019年05月 6日  0:02:49
gpg:                using RSA key 4AEE18F83AFDEB23
gpg: Can't check signature: No public key
Author: Jay Q <41616424+justbuilding@users.noreply.github.com>
Date:   Mon May 6 00:02:49 2019 +
0800Update README.md
```

