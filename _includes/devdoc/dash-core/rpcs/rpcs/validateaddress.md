{% comment %}
This file is licensed under the MIT License (MIT) available on
http://opensource.org/licenses/MIT.
{% endcomment %}
{% assign filename="_includes/devdoc/dash-core/rpcs/rpcs/validateaddress.md" %}

##### ValidateAddress
{% include helpers/subhead-links.md %}

{% assign summary_validateAddress="returns information about the given Bitcoin address." %}

{% autocrossref %}

The `validateaddress` RPC {{summary_validateAddress}}

*Parameter #1---a P2PKH or P2SH address*

{% itemplate ntpd1 %}
- n: "Address"
  t: "string (base58)"
  p: "Required<br>(exactly 1)"
  d: "The P2PKH or P2SH address to validate encoded in base58check format"

{% enditemplate %}

*Result---information about the address*

{% itemplate ntpd1 %}
- n: "`result`"
  t: "object"
  p: "Required<br>(exactly 1)"
  d: "Information about the address"

- n: "→<br>`isvalid`"
  t: "bool"
  p: "Required<br>(exactly 1)"
  d: "Set to `true` if the address is a valid P2PKH or P2SH address; set to `false` otherwise"

- n: "→<br>`address`"
  t: "string (base58)"
  p: "Optional<br>(0 or 1)"
  d: "The bitcoin address given as parameter"

- n: "→<br>`scriptPubKey`"
  t: "string (hex)"
  p: "Optional<br>(0 or 1)"
  d: "The hex encoded scriptPubKey generated by the address"  
  
- n: "→<br>`ismine`"
  t: "bool"
  p: "Optional<br>(0 or 1)"
  d: "Set to `true` if the address belongs to the wallet; set to false if it does not.  Only returned if wallet support enabled"

- n: "→<br>`iswatchonly`"
  t: "bool"
  p: "Optional<br>(0 or 1)"
  d: "Set to `true` if the address is watch-only.  Otherwise set to `false`.  Only returned if address is in the wallet"

- n: "→<br>`isscript`"
  t: "bool"
  p: "Optional<br>(0 or 1)"
  d: "Set to `true` if a P2SH address; otherwise set to `false`.  Only returned if the address is in the wallet"

- n: "→<br>`script`"
  t: "string"
  p: "Optional<br>(0 or 1)"
  d: "Only returned for P2SH addresses belonging to this wallet. This is the type of script:<br>• `pubkey` for a P2PK script inside P2SH<br>• `pubkeyhash` for a P2PKH script inside P2SH<br>• `multisig` for a multisig script inside P2SH<br>• `nonstandard` for unknown scripts"

- n: "→<br>`hex`"
  t: "string (hex)"
  p: "Optional<br>(0 or 1)"
  d: "Only returned for P2SH addresses belonging to this wallet.  This is the redeem script encoded as hex"

- n: "→<br>`addresses`"
  t: "array"
  p: "Optional<br>(0 or 1)"
  d: "Only returned for P2SH addresses belonging to the wallet.  A P2PKH addresses used in this script, or the computed P2PKH addresses of any pubkeys in this script.  This array will be empty for `nonstandard` script types"

- n: "→ →<br>Address"
  t: "string"
  p: "Optional<br>(0 or more)"
  d: "A P2PKH address"

- n: "→<br>`sigrequired`"
  t: "number (int)"
  p: "Optional<br>(0 or 1)"
  d: "Only returned for multisig P2SH addresses belonging to the wallet.  The number of signatures required by this script"

- n: "→<br>`pubkey`"
  t: "string (hex)"
  p: "Optional<br>(0 or 1)"
  d: "The public key corresponding to this address.  Only returned if the address is a P2PKH address in the wallet"

- n: "→<br>`iscompressed`"
  t: "bool"
  p: "Optional<br>(0 or 1)"
  d: "Set to `true` if a compressed public key or set to `false` if an uncompressed public key.  Only returned if the address is a P2PKH address in the wallet"

- n: "→<br>`account`"
  t: "string"
  p: "Optional<br>(0 or 1)"
  d: "*Deprecated: will be removed in a later version of Bitcoin Core*<br><br>The account this address belong to.  May be an empty string for the default account.  Only returned if the address belongs to the wallet"

- n: "→<br>`hdkeypath`"
  t: "string"
  p: "Optional<br>(0 or 1)"
  d: "*Added in Bitcoin Core 0.13.0*<br><br>The HD keypath if the key is HD and available"  
  
- n: "→<br>`hdmasterkeyid`"
  t: "string (hash160)"
  p: "Optional<br>(0 or 1)"
  d: "*Added in Bitcoin Core 0.13.0*<br><br>The Hash160 of the HD master public key"  
  
{% enditemplate %}

*Example from Bitcoin Core 0.13.1*

Validate the following P2PKH address from the wallet:

{% highlight bash %}
bitcoin-cli validateaddress 17fshh33qUze2yifiJ2sXgijSMzJ2KNEwu
{% endhighlight %}

Result:

{% highlight json %}
{
    "isvalid": true,
    "address": "17fshh33qUze2yifiJ2sXgijSMzJ2KNEwu",
    "scriptPubKey": "76a914492ae280d70af33acf0ae7cd329b961e65e9cbd888ac",
    "ismine": true,
    "iswatchonly": false,
    "isscript": false,
    "pubkey": "0312eeb9ae5f14c3cf43cece11134af860c2ef7d775060e3a578ceec888acada31",
    "iscompressed": true,
    "account": "Test"
}
{% endhighlight %}

Validate the following P2SH multisig address from the wallet:

{% highlight bash %}
bitcoin-cli -testnet validateaddress 2MyVxxgNBk5zHRPRY2iVjGRJHYZEp1pMCSq
{% endhighlight %}

Result:

{% highlight json %}
{
    "isvalid" : true,
    "address" : "2MyVxxgNBk5zHRPRY2iVjGRJHYZEp1pMCSq",
    "ismine" : true,
    "iswatchonly" : false,
    "isscript" : true,
    "script" : "multisig",
    "hex" : "522103ede722780d27b05f0b1169efc90fa15a601a32fc6c3295114500c586831b6aaf2102ecd2d250a76d204011de6bc365a56033b9b3a149f679bc17205555d3c2b2854f21022d609d2f0d359e5bc0e5d0ea20ff9f5d3396cb5b1906aa9c56a0e7b5edc0c5d553ae",
    "addresses" : [
        "mjbLRSidW1MY8oubvs4SMEnHNFXxCcoehQ",
        "mo1vzGwCzWqteip29vGWWW6MsEBREuzW94",
        "mt17cV37fBqZsnMmrHnGCm9pM28R1kQdMG"
    ],
    "sigsrequired" : 2,
    "account" : "test account"
}
{% endhighlight %}

*See also*

* [ImportAddress][rpc importaddress]: {{summary_importAddress}}
* [GetNewAddress][rpc getnewaddress]: {{summary_getNewAddress}}

{% endautocrossref %}