# Self-custody trade offs

[![Contributors](https://img.shields.io/github/contributors/Stashh/self-custody)](https://github.com/Stashh/self-custody/graphs/contributors)
[![Forks](https://img.shields.io/github/forks/Stashh/self-custody)](https://github.com/Stashh/self-custody/network/members)
[![Issues](https://img.shields.io/github/issues/Stashh/self-custody)](https://github.com/Stashh/self-custody/issues)

![Logo](images/Bitcoin%20Self%20Custody%20Trade-offs.png)

This guide will take the presumption that you already value bitcoin and wish to self custody, to be the bearer of your [bearer asset.](https://amber.app/education/what-are-bearer-instruments/) 

This guide aims to help people take ownership of their bitcoin, which is the whole point of a bearer asset - to not have counterparty risk (external trust and dependency on a third party). We will not tell you what to do, that is not our intent, it is to try and work with market participants to help people clearly state the tradeoffs associated with different methods and tools. AmberApp does not provide financial advice, seek independent council, and AmberApp will not be held liable for lost coins or any action taken with this article. Self custody means self responsibility and accountability, don't trust, verify.

<details>
 <summary>
  <h3>
    Why is self-custody important?
  </h3>
 </summary>

Over the years, there have been many examples of why this is important, like the hacks and insolvencies from Mt Gox, FTX, Celsius, BlockFi etc. This resulted in many people losing a lot of funds.

Satoshi said: _“A purely __peer-to-peer__ version of __electronic cash__ would allow online payments to be __sent directly__ from one party to another __without going through a financial institution.__”_

As Satoshi mentions above, Bitcoin is to be sent directly, without having to trust a financial institution. Bitcoin’s value proposition as a censorship-resistant (decentralized network) and finite (scarce) bearer (no counterparty risk) asset is only valuable if you self-custody. 

If you are __leaving coins on an exchange__, or can’t withdraw your Bitcoin because you __have exposure to it via an ETF, or some derivative thereof, you are trusting that person or organization to not be rehypothecating__ funds (giving out more IOU’s than they have in reserves). __By taking ownership__ of your Bitcoin and using the Bitcoin network, __you are verifying that you own and control those funds.__
</details>

<details>
 <summary>
  <h3>
    What is the best setup?
  </h3>
 </summary>
Your solution will be unique to your subjective valuation of Bitcoin and threat model for securing it. For example, if you have 0.002 Bitcoin, versus you having 20 Bitcoins, you are going to spend different amounts of time, effort and money into understanding and securing your funds. We will take the presumption here that you value your bitcoin significantly, as you should, given that at some point in the future, it will likely be a lot more valuable than it is today. 

There are plenty of guides for how to quickly and simply generate a wallet that __should be__ sufficient as an initial step, again, we will take the presumption that you just want to do it right the first time, although security is a moving target and can always be improved upon, as new features and technological advancements evolve. “Doing it right” is based on our current understanding, and we recommend that you always do your own research and understand the tradeoffs before making any decision, while this is a guide based on our recommendations, we are not liable for the decisions you make.

There are many great guides, such as [Sparrow's recommendation](https://sparrowwallet.com/docs/best-practices.html) (image below), and [Arman's work](https://armantheparman.com/bitcoin-storage-get-better/). It's good to look at a few different options, see the trade-offs and make an informed decision. The effort spent on your security will depend upon how you value it, as mentioned above.

|                 | Beginner          | Intermediate      | Expert             |
|-----------------|-------------------|-------------------|--------------------|
| Max Amount      | $10,000           | $100,000          | -                  |
| Wallet Type     | Single signature  | Single signature  | Multi-signature    |
| Server Type     | Public Electrum   | Private Bitcoin Core | Private Electrum  |
| Private To      | None              | Passive Listeners | Active Attackers   |

We recommend that you read a few guides, and choose what's best for your specific needs. 
</details>

Let's just get started with generating a seed and helping you get those sats off an exchange and into *YOUR* wallet!

It is worth noting that any software you download, you should verify it's authenticity, the best desktop wallet, Sparrow, helps this process become as easy as drag and drop. [Verify your downloads](https://www.sparrowwallet.com/download/)!

My ([Kiwi](https://keybase.io/kiwi_)) current thoughts on the [ideal solution](#kiwis-ideal-setup) is at the very bottom, for those interested.

There are three components, __*Generation*__</h4>: generating a seed, __*At Rest*__: storing your seed, and __*At Use*__: using it. 

Here are our recommendations for each, we hope you enjoy this content and provide valuable feedback, so we can always improve of knowledge, resource base, and ultimately value to our clients and the Bitcoin ecosystem. 


## **Seed: Generation**
<details>
<summary>
 <h3>What is a seed?</h3>
</summary> 
 
It is a ([BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)) standardized list of English words, which makes the binary code human-readable, which makes it easier for people to generate and store all the necessary secret information to recover and use your Bitcoin.

To generate your seed, there are a few options. Remember, all options have trade-offs between the conveniences provided and verifying security. 

Some Bitcoiners recommend [generating your seed offline](#how-to-generate-your-own-seed). This is so you are not trusting any code in the hardware or software wallet. The reasoning for this is that you have to be an incredibly competent developer and a hardware security expert to verify that there is little to no risk with generating your seed in hardware or software wallets. 

If you don’t wish to generate your own seed offline, you can generate it on a device and also add a passphrase, this ensures that you are generating a new seed - (private key and xpub: set of addresses to receive your Bitcoin), rather than blindly trusting the one generated by the hardware wallet. This is because adding a passphrase creates a completely new wallet.
</details>

<details>
 <summary>
  <h3>
    12 or 24 words?
  </h3>
 </summary>
 
The minimum security standard of Bitcoin is 128 bits, which is what a 12-word seed phrase encodes. HOWEVER, the first 11 words only encode 11x11 = 121 bits of entropy. The last word encodes 7 bits of entropy, and 4 checksum bits.

For scale, omitting 7 bits of entropy simplifies the space by 2^7 = 128x. In other words, the 121 bits of the first 11 words has only 1/128 = 0.0078 = 0.78% of the strength of a full 128 bits. Put another way, if the 12th word’s entropy bits are not random, your seed has lost 1 - 0.0078 = 0.992 = 99.2% of its strength.

For this reason, some bitcoiners generally do not recommend self-rolling 12-word seeds. It’s only marginally more difficult to roll 23 words rather than 11, and it gives you a whole lot of room to have an error and still maintain at least 128 truly random bits of entropy.
</details>

<details>
 <summary>
  <h3>Passphrase:</h3>
 </summary>

After you have successfully generated your seed in a device or have created your seed offline and have done your checksum and created the last word for your seed, then checked it in another device to ensure it is correct, you can then add a passphrase. 

If anyone finds your seed words, or extracts it from your unsafe practices, a passphrase provides an extra level of security.

Warning: This will generate a completely new wallet.  If you forget or lose the password, you lose access to the private key and any funds associated with it, "with great power comes great responsibility."

Your passphrase should be 15 - 30 random characters long, so that it can not easily be brute forced if someone were to find out what your seed words are from unsafe practices. One word, or a name, is like one character, it is not recommended to have 15 - 30 words, use unique characters.

This should be 3 strings of numbers and text, as an example:

__3gjd99dwLH!fj*-y__

Obviously the more characters, the stronger the entropy but also the more room for mistakes. This is a trade-off where you must decide which you are comfortable with. Consider how often you will be using this to move funds.
</details>

<h3>
  Advanced:
</h3>

<details>
 <summary>
  <h3 id="how-to-generate-your-own-seed">
   How to generate your own seed?
  </h3>
</summary>

There are three options to do this which I recommend: 

1) [Seed picker](https://github.com/jimbojw/seed-picker-solitaire) cards by Jimbo
2) [Entropia orange pills](https://btc-hardware-solutions.square.site/product/entropia-v2-seed-tablets/11) by Seed Signer
3) Cutting up a bip-39 word list on paper and putting it in a hat

Once you have written down your 11 or 23 words, you will need to do a checksum, which is just “a way to ensure that the rest of your seed phrase has been accurately recorded. In other words, it is derived from, and dependent on, all the previous words in your seed phrase.”[1](https://getcoinplate.com/blog/seed-phrase-last-word-checksum/#:~:text=It%20plays%20a%20specific%2C%20calculated,words%20in%20your%20seed%20phrase.) 

Here are the tutorials for how to generate a seed with [playing cards](https://www.youtube.com/watch?v=qTSG_Nzp19U), [Entropia pills](https://www.youtube.com/watch?v=dCAr2urEe1o) or your word list. Regardless of whether you chose 12 or 24 words, you will have randomly selected your 11 or 23 words and then need to perform a checksum to generate the last word. Here are the tutorials to generate your last word with either a Seed Signer, Passport or Cold Card. It is a good idea to check on multiple signing / hardware devices that you generated the seed correctly and have identical public and private keys.

If you want to complete a checksum by hand, and really go the extra mile, you can see Arman’s work [here](https://armantheparman.com/dicev2/).

Sufficient entropy is incredibly important, whether this is shuffling cards, mixing your entropia pills or cut up words list, using coin tosses, rolling dice, the more entropy, the more secure your seed is. The idea is that if you add logic to the selection (i.e. picking seed words that you "like" or arranging them in a logical sequence) it becomes more guess-able. Just some nuance, but randomness is essential.
</details>

<details>
 <summary>
  <h3>Multi-Sig:</h3>
 </summary>

Multi-Signature is a setup where in order to spend bitcoin, you need a certain amount of keys, such as 2 / 3 (or more) keys to spend. For example it could be 2 / 4 or 5 / 8, it’s really up to you. 

You can imagine an old vault in a bank full of gold, where it may take two out of three keys to open the vault. This is the analogy, with Bitcoin, you are the bank, and you can hold all the keys, or distribute them with family/friends / or an institution.

This means that if any nation-state or bad actor holds you ransom, they will have to somehow find out who has the keys, interact with family or friends overseas and try to convince them to collude. You can have all sorts of booby traps, safe words and incorrect pins that brick devices. 

Note: Having more keys makes it more expensive to spend. Most people don't need multi-signature, a seed and passphrase is sufficient security, if done right, for most people. Only do multi-signature if you are an expert or supervised by an expert.

We will not recommend exactly how you set this up, as we all subjectively value the tradeoff with convenience and verification, we will only discuss the merits and trade-offs as we currently see them.

Setting up a multi-sig that is internationally distributed is the apex of security. You can meet a friend or family member at every Bitcoin conference and create, test, then add that key to your vault.  This should be done offline so that there is no digital footprint for privacy and security reasons.

This is obviously quite a lot of work, so it depends on your threat model, which corresponds to how much bitcoin you own. Keep in mind that what you own now could be worth considerably more in the near future. 

Again, don’t let “perfection” lead to having too much complexity, many people have lost their keys by creating something too complex and them loosing or not remembering critical information. Be careful you don’t unnecessarily risk locking yourself out. 

Note: If you lose a private key, you're going to need __ALL__ of the public keys (typically in the form of a wallet descriptor) to be able to take advantage of the fault tolerance that multisig allows for.

A lot of people use multivendor (multiple various signing devices / hardware wallets) for their multi-signature wallets and then distribute their seeds globally. Given we are generating our seed offline, this is less applicable, as we are not relying on any vendor to create our seed. We merely use them to sign transactions, to minimize any risks, you can remove the microSD card after booting the device for signing devices that can sign PSBT’s (partially signed bitcoin transactions) via QR.
</details>
</details>
</details>

## **Seed: At Rest**

<details>
 <summary>
  <h3>Backing Up Your Seed:</h3>
</summary>

This leads us into the next and most important point, back-ups. There are a few options to write your seed words and passphrase with. 

One approach is to write it on something that will withstand the test of time and be resistant to any accidents that could occur, i.e. natural disasters like floods or fire. Steel is the preferred option here. 

Another is to have it in plain sight, in multiple locations, but to be so illogical that no one would guess this is a seed. It could be words written in italic in your photo album, highlighted words in a poem, there are some really unique ways of doing this where it would a disadvantage for us to give you a specific way. Be creative, but remember, the more complexity you add, the more risk of loosing your funds. If you take this route, you should use a passphrase and store them separately. 

Here are some options: 

1) [Steel QR plates](https://vulcan21.com/steelqr/)
2) [CC steel plate](https://store.coinkite.com/store/seedplate)
3) [Steel plate and pen](https://www.amazon.com/Hotop-Cryptocurrency-Hardware-Compatible-Metallic/dp/B09B4MX9HS/ref=sr_1_30?hvadid=604629082052&hvdev=c&hvlocphy=9018769&hvnetw=g&hvqmt=e&hvrand=2010572611125505365&hvtargid=kwd-1590316374874&hydadcr=25435_13484274&keywords=ledger%2Bthe%2Bbillfodl&qid=1687374028&sr=8-30&th=1)
1) [Seed Hammer](https://seedhammer.com/)

Advanced:  For those of you who wish to help others with this locally, you should consider a Seed Hammer. 

Here are the corresponding tutorials for how to do this: 

1) [Seed Hammer](https://seedhammer.com/get-started/)
2) [CC steel plate](https://www.youtube.com/watch?v=_m5BjsdeXIY)

It is important to write down your seed words, passphrase if you have one, and finger print (XFP) or xpub. This will let you know if you have the correct wallet or not when you use this again at a later date. 

It is also very important to write down your xpubs if you are using multi-sig. Whether that's each wallets xpub and the multi-sigs xpub, or the wallet descriptors which contain this information.

Now that we have created our seed words + passphrase and have backed them up, we are ready to use a hardware wallet or signing device to sign transactions and use bitcoin. 
</details>

## **Seed: In Use**

<details>
 <summary>
  <h3>Choosing A Hardware Wallet:</h3>
</summary>

The point of a hardware wallet or signing device is to create a barrier between your devices (private and public keys) and the internet. A hardware wallet provide digital storage of private keys and also create digital signature to use those keys, signing devices, alternatively do no persistently store key material after a usage session, and are just used for generating digital signatures.

Every wallet has its own set of tradeoffs. At AmberApp, we believe in the Bitcoin mantras “Don’t Trust, Verify” and also “Not Your Keys, Not Your Coins”. This is why we meet users at their map of the world and help them along their hero’s journey to realize their sovereignty. 

There are a few major trade-offs to consider, one is the secure element on plug and play devices. There is a difference between plugging into a computer ([Trezor](https://trezor.io/), [Bitbox](https://bitbox.shop/en/products/bitbox02-bitcoin-only-4/) etc) and air gapped ([Seed Signer](https://seedsigner.com/), [Passport](https://foundationdevices.com/passport/), [Coldcard](https://coldcard.com/), [Jade](https://blockstream.com/jade/)), you can hear some of the nuances about being air gapped and the issues with USB HWWs discussed [here](https://twitter.com/nvk/status/1561068212489428993).

There are multiple benefits of having a hardware wallet with a secure element, as it keeps the maintaining key in its enclave and enables the device to potentially warn the user if a recent firmware update is malicious or not. Trade-offs everywhere, with everything.
</details>

<details>
 <summary>
  <h3>Secure Element</h3>
</summary>

Pro’s: 
- Keeps maintaining key in device and can warn users if there is a malicious update
- Convenience of plug and play

Con’s:
- One more thing to understand deeply in order to verify it’s trade-offs
- You need to verify that you’ve obtained an authentic device from the manufacturer anyway
- Secure Elements are closed source and can not be verified, however, there are large bounties for anyone to crack them, which none have been claimed

Note: Trezor is trying to create their own [secure element chip that is open source](https://tropicsquare.com/).

Stateless Device

Pro’s:
- No threat if you lose the device
- Does not retain private key information and completely wipes any temporarily stored information upon being powered off.

Con’s:
- Have to verify QR security to verify it’s trade-offs
- Need to have seed (QR or seed words) with you to spend from

On top of that there is a difference between air gapped options, using a micro SD + secure element, or using QR codes. 

Realistically, unless you are an incredibly competent developer, you will have to have some level of trust. This could be trusting the educator / influencer debating the merits of one over the other, but you will still have to trust them and / or the provider if you can’t read and understand code to verify the trade-off’s. It’s about minimizing trust as much as possible for most people, for those who deep dive, it’s learning how to read code and verify. 

Some HWWs, such as Seed Signer are not only FOSS (Free Open Source Software) and reproducible (can build from source code) but you can also order general hardware parts online and build it yourself within 30 minutes. It’s incredibly easy. This mitigates any supply chain attack and reduces trust required as you sourced the parts (from different places) and built it yourself. However, The hardware (Raspberry Pi’s) are closed source, and there is no secure element, so you will need to verify your download each time you update the firmware.

You could get a Jade HWW from Blockstream which comes prebuilt, and you can choose translucent cases. It has a [virtual secure element](https://help.blockstream.com/hc/en-us/articles/9639949755673-How-does-Blockstream-Jade-s-oracle-enforced-PIN-protection-work-). Blockstream is a reputable company which has been on the right side of many bitcoin battles, such as the block size wars. On top of that, Adam Back is at the helm and is also very reputable. They are also [FOSS](https://blockstream.com/jade/#:~:text=Blockstream%20Jade%20is%20fully%20open%20source.). 

Passport stems from Cold Cards software, is similar to Seed Signer, in the sense they are FOSS and use QR codes to sign, but rather than being sourced and built by yourself, they come pre-built. They also have a secure element and are a stateful device, meaning they retain private key information within the device.

Cold Card, the calculator looking like device that started off as FOSS but moved to OSS (Open Source Software) and it too has a reproducible build. This is still air-gapped but rather than using QR codes to sign transactions (PSBT), they use a microSD card for the Mk4, the ColdCard Q has the ability to use QR codes (BBQr). 

Regardless of what signing device you choose, you will need to choose based off of the trade-offs you deem acceptable. Unless you are a competent hardware designer, you will not be able to quantify and understand the merit of each tradeoff and will need to defer to subjectively trusted expertise. 
</details>

<details>
 <summary>
  <h3>
   Desktop Wallets:
  </h3> 
 </summary>

[Sparrow Wallet](https://sparrowwallet.com/) is one of the Bitcoin community’s favourite wallets, it is open source and free to use. Sparrow is feature packed and can do anything bitcoiners need. When you are more advanced you can dive into their [privacy features](https://sparrowwallet.com/docs/spending-privately.html) and ensure you have good UTXO management.

Sparrow enables you to [verify your downloads](https://www.sparrowwallet.com/download/) with ease too, with simple drag and drops of the download and signatures, you can ensure you have the right file. 

Tutorials - [Arman](https://armantheparman.com/sparrow/), [Southern Bitcoiner](https://www.youtube.com/watch?v=tE-oEQPMrdI), [BTC Sessions](https://www.youtube.com/watch?v=qJ_SpQX_YKw).

[Specter Wallet](https://specter.solutions/desktop/index.html) is another good option, it is FOSS and also allows you to have coin control. 

For the pro’s, Electrum is generally preferred as there is a lot of unorthodox tools available, however, if you are competent enough to use this, you don’t need us to explain the benefits or tradeoffs.  

Many use desktop wallets for their vaults, where you don’t intend on spending it for many epochs (four-year cycles), as phones spy, and you don’t want to be using or checking this often. Do it once, do it well, the more you touch it, the more likely you are to lose it and / or give away information unnecessarily.
</details>

<details>
 <summary>
   <h3>Mobile Wallets:</h3> 
 </summary>

#### ***Checking account - On-Chain:***

[Green Wallet](https://blockstream.com/green/), [Blue Wallet](https://bluewallet.io/), [Nunchuk](https://nunchuk.io/) and [Keeper](https://bitcoinkeeper.app/).

#### ****Spending account - Lightning:****

[AmberApp](https://www.amber.app/), [Wallet of Satoshi](https://www.walletofsatoshi.com/), [Zeus](https://zeusln.com/).
</details>

<details>
 <summary>
  <h3>
   Seed: Recovery
  </h3> 
 </summary>

It is a good idea for you to be familiar with the process of recovering your funds by recovering your wallet using your seed words and passphrase, if you have one. For multi-sig, you will recover using your wallet by [scanning two of your wallet descriptors](https://www.youtube.com/watch?v=sJNWM6luCzA), or all of your xpubs. 

A great way to test this, is to simply download [Green Wallet](https://blockstream.com/green/) and [Blue Wallet](https://bluewallet.io/) on your mobile. Create a new wallet on one of them, write down the seed words, then open the other and select to restore a new wallet, then enter your recovery phrase (seed words). 

DO NOT do this testing for any wallet you wish to use, this test is merely to teach you the importance of your seed words, passphrase, XFP (extended finger print) to identify and xpubs (for multi-sig). 

This will help give you peace of mind, that as long as you have these seed words stored somewhere safe, you will always be able to access that wallet.
</details>

<img src="images/Ben_Kiwi_Laz0rs_ONLY_40Mbps_moshed_07_29_01_10_04_294.gif" alt="kiwi lazers" style="border-radius: 50%; width: 150px; height: 150px; object-fit: cover;">

<details>
 <summary>
  <h2 id="kiwis-ideal-setup">Kiwi's ideal setup</h2>
 </summary>

As you will see in the Seed Generation tab, in the advanced section, setting up a multi-signature wallet, using three different vendors significantly reduces any attack vector from any provider. 

I believe getting a PO Box setup is important, that way when you order your signing devices and back-up tools, if any of that information is leaked, your home address will not be. This reduces the likelihood of anyone showing up to your house. 

As mentioned in the first section, [download Sparrow Wallet](https://www.sparrowwallet.com/download/), read the download page linked and use it to verify any downloads you have for your signing devices. 

Whether you choose multi-signature, or single-signature, I believe generating your own 24 seed word(s) using the Seed-Picker cards, Entropia Pills, or simply cutting up a BIP-39 word list and mixing the words in a bowl, will provide more than sufficient entropy to ensure you create a quality seed. You can see more about these options in Seed Generation, Advanced. 

For multi-sig, I think the best mixture of signing devices is [Jade by Blockstream](https://store.blockstream.com/?code=AmberApp), Passport by Foundation, and the [Q or Mk4 by CoinKite](https://store.coinkite.com/promo/AMBERAPP). The backup options, you should use the capsule or metal from Blockstream, as it covers the details listed. You will want to ensure that if anyone turns up to your house, they can't get anything, meaning, you have to travel to friends or family to get that key's information. The problem this creates, is that you could then be dependent on the family member or friend. Consider creating multiple backups for the key you will share, and bury it or hide it somewhere that is not in your household. 

For single signature, you obviously only have one key, however you can still split these 24 words into two or more backups. Meaning that even if one is found, it is useless without the other. Again, as per above, consider making it so you would have to travel to get the other key, with the recipient of said key knowing some code words, in case you are in trouble, and have some call to action like meeting at a public place with the authorities trailing. Also consider having another copy of their half of the keys details somewhere safe, perhaps buried, in case they lose it. I recommend choosing out Passport by Foundation, and the [Q or Mk4 by CoinKite](https://store.coinkite.com/promo/AMBERAPP), as Jade is general purpose hardware, like Seed-Signer, which can play a role in a multi-sig setup, but likely should not in a single sig setup in my opinion. DYOR. 

Regardless of which one you choose, you should have a decoy wallet at home, with little funds, to give if you ever find yourself in trouble. For the family or friend that holds that other key, create a code word to let them know if you are in trouble, so they can call authorities or help you in other ways. 
</details>

## Conclusion:

There are no perfect choices, only trade-offs. Every person will have different strengths regarding what they can verify, and what they will prefer to trust, they will subjectively value different components accordingly. 

We hope that this self custody SOP brought you value, if you have any feedback, please join our Telegram and let us know, alternatively, if you are competent with GitHub, make a pull request to update it! 

