
## Ontology CLI User Guide

- [CLI Account Command](#cli-account-cmd)
- [CLI Info Show Command](#cli-info-show-cmd)
- [CLI ASSET Command](#cli-asset-cmd)
- [CLI Setting Command](#cli-setting-cmd)
- [CLI Contract Command](#cli-contract-cmd)

```
User can start ontology directly,by the command as follow:
$./ontology

If want to know the command that ontology contains, user can run ontology with --help:
$./ontology --help
```
--- 

## <a name="cli-account-cmd"></a> CLI Account Command

### Add account

Create a new account contains a key pair and an address.

First select the key type, which could be specified via `-t` option.

```
$ ontology account add

Select a signature algorithm from the following:

  1  ECDSA
  2  SM2
  3  Ed25519

[default is 1]: 
```

If SM2 or EdDSA is selected, the parameters are auto set since each of the two only supports one default setting.

```
SM2 is selected.
Use curve sm2p256v1 with key length of 256 bits and SM3withSM2 as the signature scheme.
```
or

```
Ed25519 is selected.
Use curve 25519 with key length of 256 bits and Ed25519 as the signature scheme.
```

If ECDSA is selected, the next step is to select the curve:

```
Select a curve from the following:

    | NAME  | KEY LENGTH (bits)
 ---|-------|------------------
  1 | P-224 | 224
  2 | P-256 | 256
  3 | P-384 | 384
  4 | P-521 | 521

This determines the length of the private key [default is 2]: 
```

The curves determine the key length of 224, 256, 384 and 521 respectively.
This parameter could be specified via `-b` option.

Then select a signature scheme:

```
Select a signature scheme from the following:

  1  SHA224withECDSA
  2  SHA256withECDSA
  3  SHA384withECDSA
  4  SHA512withECDSA
  5  SHA3-224withECDSA
  6  SHA3-256withECDSA
  7  SHA3-384withECDSA
  8  SHA3-512withECDSA
  9  RIPEMD160withECDSA

This can be changed later [default is 2]: 
```

The above selections can be skipped by adding `--default` option, while using the default parameters.

The private key needs be encrypted. This requires a password:

```
Enter a password for encrypting the private key:
Re-enter password:
```

The private key can be re-encrypted using the `encrypt` command.

After all the parameters are selected, it will generate a key pair. 

The public key will be converted to generate the address. Then output the public informations.

```
Create account successfully.
Address: `base58-address-string`
Public key: `hex-string`
Signature scheme: SHA256withECDSA
```

### List existing account

```
$ ontology account list
* 1  xxxxx
  2  xxxxx
```

The `*` indicates the default account.

With `-v` option, details of each account would be displayed.

```
$ ontology account list -v
* 1 xxxxx
    Signature algorithm: ECDSA
    Curve: P-256
    Key length: 256 bits
    Public key: xxxx
    Signature Scheme: SHA256withECDSA

  ...
```

### Modify account

Modify the account settings, such as the signature scheme.
Account is specified by the index displaying in the list command.


### Delete account

Delete an existing account by specifying the index.


### Re-encrypt account

Change the password for an account.

```
$ ontology account encrypt 1

Please enter the original password:
```

Then input the new password if the original password is correct.

```
Enter a password for encrypting the private key:
Re-enter password:
```

## <a name="cli-info-show-cmd"></a>CLI Info Show Command
```
Usage:
    ontology info [command options] [args]

Description:
    With ontology info, you can look up blocks, transactions, etc.

Command:
    version
    block
        --hash value                  block hash value
        --height value                block height value
    tx
        --hash value                  transaction hash value
```

### Example for info version 
```
$ ./ontology info version
Result will show as follow:
Node version: 653c-dirty
```

### Example for info block (with height)
```
$ ./ontology info block --height 12
Result will show as follow: 
{
	"Action": "getblockbyheight",
	"Desc": "SUCCESS",
	"Error": 0,
	"Result": {
		"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
		"Header": {
			"BlockRoot": "1ff293c1e15e1a37d449bba5aebda52280ceee645547f9f219ea903f7ad18386",
			"Bookkeepers": [
				"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
			],
			"ConsensusData": 5922267418785983000,
			"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
			"Height": 12,
			"NextBookkeeper": "TACATSTXT4E6UJHY57Ccv2TNBPGjbD9hfU",
			"PrevBlockHash": "bdbe264712d38f6d46bffdea8f6a9ab3ef73d343b043d31a0a0594758b73da1d",
			"SigData": [
				"016f3669a1998f2716e91093ca7946263433f92605ae9e6bf2b695145dbe24de5b38c93f8e91ae1d1f89626a4e87ac101f4344fb312c3e482b105a94f7d15f3fe9"
			],
			"Timestamp": 1524280951,
			"TransactionsRoot": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
			"Version": 0
		},
		"Transactions": [
			{
				"Attributes": [],
				"Fee": [],
				"Hash": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
				"NetworkFee": 0,
				"Nonce": 0,
				"Payload": {
					"Nonce": 1524280951763615000
				},
				"Sigs": [
					{
						"M": 1,
						"PubKeys": [
							"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
						],
						"SigData": [
							"01885e3078fe398987c5d89d650714d4e4ab9432ea5bcb98505cf4913d224920203c2f98b1ea24857e6af0f06b3bdf72d862bbe3b0989937cbe06c91775e2aa6e8"
						]
					}
				],
				"TxType": 0,
				"Version": 0
			}
		]
	},
	"Version": "1.0.0"
}

NOTE:
If a invalid value of height is given, the result will show as follow:
{
	"Action": "getblockbyheight",
	"Desc": "UNKNOWN BLOCK",
	"Error": 44003,
	"Result": "",
	"Version": "1.0.0"
}
```

### Example for info block (with hash)
```
$ ./ontology info block --hash 805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2
Result will show as follow: 
{
	"Action": "getblockbyheight",
	"Desc": "SUCCESS",
	"Error": 0,
	"Result": {
		"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
		"Header": {
			"BlockRoot": "1ff293c1e15e1a37d449bba5aebda52280ceee645547f9f219ea903f7ad18386",
			"Bookkeepers": [
				"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
			],
			"ConsensusData": 5922267418785983000,
			"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
			"Height": 12,
			"NextBookkeeper": "TACATSTXT4E6UJHY57Ccv2TNBPGjbD9hfU",
			"PrevBlockHash": "bdbe264712d38f6d46bffdea8f6a9ab3ef73d343b043d31a0a0594758b73da1d",
			"SigData": [
				"016f3669a1998f2716e91093ca7946263433f92605ae9e6bf2b695145dbe24de5b38c93f8e91ae1d1f89626a4e87ac101f4344fb312c3e482b105a94f7d15f3fe9"
			],
			"Timestamp": 1524280951,
			"TransactionsRoot": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
			"Version": 0
		},
		"Transactions": [
			{
				"Attributes": [],
				"Fee": [],
				"Hash": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
				"NetworkFee": 0,
				"Nonce": 0,
				"Payload": {
					"Nonce": 1524280951763615000
				},
				"Sigs": [
					{
						"M": 1,
						"PubKeys": [
							"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
						],
						"SigData": [
							"01885e3078fe398987c5d89d650714d4e4ab9432ea5bcb98505cf4913d224920203c2f98b1ea24857e6af0f06b3bdf72d862bbe3b0989937cbe06c91775e2aa6e8"
						]
					}
				],
				"TxType": 0,
				"Version": 0
			}
		]
	},
	"Version": "1.0.0"
}

NOTE:
If a invalid value of block hash is given, the result will show as follow:
{
	"Action": "getblockbyheight",
	"Desc": "UNKNOWN BLOCK",
	"Error": 44003,
	"Result": "",
	"Version": "1.0.0"
}
```

### Example for info transaction
```
$ ./ontology info tx --hash 805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2
Result will show as follow: 
{
	"Action": "gettransaction",
	"Desc": "SUCCESS",
	"Error": 0,
	"Result": {
		"Attributes": [],
		"Fee": [],
		"Hash": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
		"NetworkFee": 0,
		"Nonce": 0,
		"Payload": {
			"Nonce": 1524280951763615000
		},
		"Sigs": [
			{
				"M": 1,
				"PubKeys": [
					"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
				],
				"SigData": [
					"01885e3078fe398987c5d89d650714d4e4ab9432ea5bcb98505cf4913d224920203c2f98b1ea24857e6af0f06b3bdf72d862bbe3b0989937cbe06c91775e2aa6e8"
				]
			}
		],
		"TxType": 0,
		"Version": 0
	},
	"Version": "1.0.0"
}

NOTE:
If a invalid value of transaction hash is given, the result will show as follow:
{
	"Action": "gettransaction",
	"Desc": "UNKNOWN TRANSACTION",
	"Error": 44001,
	"Result": "",
	"Version": "1.0.0"
}
```
---

## <a name="cli-asset-cmd"></a> CLI Asset Command
```
Usage:
    ontology asset [command options] [args]

Description:
    With this command, you can control assert through transaction.

Command:
    transfer
        --caddr     value                 smart contract address
        --from      value                 wallet address base58, which will transfer from
        --to        value                 wallet address base58, which will transfer to
        --value     value                 how much asset will be transfered
        --password  value                 use password who transfer from
    status
        --hash     value                  transfer transaction hash
```

### Example for asset transfer
```
$ ./ontology asset transfer --caddr=ff00000000000000000000000000000000000001 --value=500 --from TA6VvtGekMfinP97CTL9SH5WTowChUungL   --to TA7bRMkjMbP4JHhAVASN1fwpB56bi8aYUK  --password passwordtest
If transfer asset successd, the result will show as follow:
[
	{
		"ContractAddress": "ff00000000000000000000000000000000000001",
		"TxHash": "e0ba3d5807289eac243faceb1a2ac63e8dee4eba208ceac193b0bd606861b729",
		"States": [
			"transfer",
			"TA6VvtGekMfinP97CTL9SH5WTowChUungL",
			"TA7bRMkjMbP4JHhAVASN1fwpB56bi8aYUK",
			500
		]
	}
]

Otherwise, the null value will given.
```

### Example for asset status
```
$ ./ontology asset status --hash e0ba3d5807289eac243faceb1a2ac63e8dee4eba208ceac193b0bd606861b729
If query succeed, the result will show as follow:
[
	{
		"ContractAddress": "ff00000000000000000000000000000000000001",
		"TxHash": "e0ba3d5807289eac243faceb1a2ac63e8dee4eba208ceac193b0bd606861b729",
		"States": [
			"transfer",
			"TA6VvtGekMfinP97CTL9SH5WTowChUungL",
			"TA7bRMkjMbP4JHhAVASN1fwpB56bi8aYUK",
			500
		]
	}
]

Otherwise, the null value will given.
```

---

## <a name="cli-setting-cmd"></a> CLI Setting Command
```
Usage:
    ontology set [command options] [args]

Description:
    With ontology set, you can configure the node.

Command:
    --debuglevel value                 debug level(0~6) will be set
    --consensus value                  [ on / off ]
```

### Example for setting debuglevel
```
$ ./ontology set --debuglevel 1
When setting succeed, the result will show as follow:
map[desc:SUCCESS error:0 id:0 jsonpc:2.0 result:true]
```

### Example for setting consensus
```
$ ./ontology set --consensus on
When setting succeed, the result will show as follow:
map[desc:SUCCESS error:0 id:0 jsonpc:2.0 result:true]
```
---


## <a name="cli-contract-cmd"></a> CLI Contract Command
```
Usage:
    ontology contract [command options] [args]

Description:
    With this command, you can invoke a smart contract

Command:
    invoke
        --caddr      value               smart contract address that will be invoke
        --params     value               params will be

    deploy
        --type       value               contract type ,value: 1 (NEOVM) | 2 (WASM)
        --store      value               does this contract will be stored, value: true or false
        --code       value               directory of smart contract that will be deployed
        --cname      value               contract name that will be deployed
        --cversion   value               contract version which will be deployed
        --author     value               owner of deployed smart contract
        --email      value               owner email who deploy the smart contract
        --desc       value               contract description when deploy one
```

### Example for contract deploy
```
$ ./ontology contract deploy --type=1 --store=true --code=./deploy.txt --cname=testContract --cversion=0.0.1 --author=Yihen --desc="this is my first test contract" --email="name@emailaddr.com"
User need to input password, when deployed succeed, the result will show as follow:
Deploy smartContract transaction hash: b68307e7659a53a10d3061a3e4721b5a152bd4e6e80b75002f5cc8b5294be493
```

### Example for contract invoke
```
$ ./ontology contract invoke --caddr TA6VvtGekMfinP97CTL9SH5WTowChUungL --params contract-params-need
User need to input password, when invoke succeed, the result will show as follow:
invoke transaction hash:64976014daec682f8e3a4fc62c26f4636ac7be6bd548f67f24f62211394f8923
```
