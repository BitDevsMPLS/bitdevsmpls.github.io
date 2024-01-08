---
layout: post
type: socratic
title: "Socratic Seminar 11"
---

## Welcome

Welcome back! Big thanks to new our host [Improving Inc](https://improving.com/) for providing the space!
This meetup will be run in the format of a Socratic Seminar, inspired by other [Bitdevs Socratic Seminars across the country](https://bitdevs.org/cities).

# Details
 - Where: [Improving Inc](https://www.google.com/maps/place/1515+NE+Central+Ave,+Minneapolis,+MN+55413/@45.0037797,-93.2469316,17z/data=!4m6!3m5!1s0x52b32d965c06ad57:0x277e62e6c3015129!8m2!3d45.0039428!4d-93.2456978!16s%2Fg%2F11bw3z3dw6) 1515 NE Central Ave Minneapolis, MN 55413
 - When: Tuesday January 9th. Socratic Seminar from 5pm - 7pm. Actual content will start ~5:30pm. 
 - Happy Hour afterwards at [Indeed Brewery](https://www.indeedbrewing.com/)

# Rules
 - No Photos
 - Be Respectful
 - Keep the conversation technical
 - [Chatham House Rule](https://www.facilitator.school/blog/chatham-house-rule)

# Helpful Links
 - [Meetup](https://www.meetup.com/minneapolis-bitcoin-developers/events/298091015/)
 - [Twitter](https://twitter.com/BitcoinersMPLS)
 - [Website](https://bitdevsmpls.org)
 - [SimpleX](https://simplex.chat/contact#/?v=1-2&smp=smp%3A%2F%2FenEkec4hlR3UtKx2NMpOUK_K4ZuDxjWBO1d9Y4YXVaA%3D%40smp14.simplex.im%2F2yDM8Eh4B5js6FLUOsANpVYwUt79Q_TO%23%2F%3Fv%3D1-2%26dh%3DMCowBQYDK2VuAyEAqaz4Ij9Xxn3ziHXN9DhPBdbTgYc-XjGpKcr-oDBL-hc%253D%26srv%3Daspkyu2sopsnizbyfabtsicikr2s4r3ti35jogbcekhm3fsoeyjvgrid.onion&data=%7B%22type%22%3A%22group%22%2C%22groupLinkId%22%3A%22I3WA2zuDa5OOHwDT6m0G8Q%3D%3D%22%7D)


<img src="../simplex.jpeg" width="250" height="250" />

# Agenda
 - Introductions
 - Socratic Seminar Questions
 - Discussion

# Lightning
 - [V3 Transactions Review](https://petertodd.org/2023/v3-transactions-review)
 - [Rethinking Lightning](https://stacker.news/items/379225)
 - [Liquidity griefing in multi-party transaction protocols](https://delvingbitcoin.org/t/liquidity-griefing-in-multi-party-transaction-protocols/264)

# Bitcoin
 - [Altruistic Rebroadcasting - A Partial Replacement Cycling Mitigation](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2023-December/022188.html)
 - [2023 Node Performance Tests](https://archive.ph/QCgOr)

## Covenant Discusssion

- Reactive Security (ie: eliminate threat of key theft). This has added benefit that backups become less cumbersome. Requires 2 TX to fully unencumber coins in base use case.

### OP_CTV
- [BIP 119](https://github.com/bitcoin/bips/blob/master/bip-0119.mediawiki)
- [Simple CTV Vault](https://github.com/jamesob/simple-ctv-vault)
    - How does a pure OP_CTV vault compare to an OP_VAULT vault?

### OP_VAULT
- [BIP 345](https://github.com/bitcoin/bips/blob/de9ef59307f5d94883eefd2c6691c67d358d915a/bip-0345.mediawiki)
- [On the unsuitability of pre-signed transactions](https://delvingbitcoin.org/t/the-unsuitability-of-presigned-transactions-for-vaults/113)
- [On the benefit with OP_CTV](https://x.com/jamesob/status/1742375641641574896?s=20)
- [OP_VAULT Demo](https://www.youtube.com/watch?v=7Zwm5iHFyBQ)

- What is the purpose of the CTV in the time-locked CTV tapleaf of a trigger transaction? The necessity of the timelock is clear, but what advantage does CTV offer in this context over plain OP_CHECKSIGVERIFY?

"dynamic unvault targets, which allow the proposed withdrawal target for a vault to be specified at withdrawal time rather than when the vault is first created. This would remove the need for a prespecified, intermediate wallet that only exists to route unvaulted funds to their desired destination."

"These tapleaf replacement rules, described more precisely below, ensure a timelocked withdrawal, where the timelock is fixed by the original OP_VAULT parameters, to a fixed set of outputs (via OP_CHECKTEMPLATEVERIFY[2]) which is chosen when the withdrawal process is triggered."
"During the withdrawal process, the proposed final destination for value being withdrawn must be committed to."
- Who cares that withdrawal commits to a fixed set of outputs? OP_VAULT is already a covenant. Why do we need the nested CTV covenant?

- How does the OP_VAULT opcode check that the output being created by the trigger transaction consist of the exact same taptree with only the OP_VAULT leaf substituted for the templated time-locked leaf script?
The taproot "control block" consists of all the data necessary to evaluate taproot spends. This consists of a tapleaf script being spent, alond with a merkle path from that leaf to the taptree root. The opcode can simply replace the executing leaf with the new leaf, recompute a taptree root and verify that this root matches + internal key matches the created output's script public key. The address will not specify it's taptree root. Isn't that information only provided at spend time? If the internal key is the same then we can check that our computed taptree root post-substitution + internal key yields the same raw public key.

Via a *single* taptree leaf replacement mechanism, the OP_VAULT opcode enforces that the transaction which spends from our vault does NOT contain ANY new spending conditions EXCEPT for a pre-committed template script leaf which will replace the OP_VAULT script leaf. This ensures that any vault withdrawal moves to an intermediate staging output with no degredation in security and which is time-locked so that we may have time to respond to un-authorized vault withdrawals. It carries forward our recovery script leaf and enforces that the other leaf will be exactly as templated.


# Fedimint
 - [Fedimint 0.2.1 Federate all the Things](https://github.com/fedimint/fedimint/releases/tag/v0.2.1)
 - [Awesome Fedimint](https://github.com/fedimint/awesome-fedimint)
 - [Mutiny Wallet Fedimint Support](https://github.com/MutinyWallet/mutiny-node/releases/tag/v0.5.1)
 - [Stacker News Fedimint Territory](https://stacker.news/~fedimint)

# Misc
 - [Mercury Layer](https://bitcoinmagazine.com/technical/mercury-layer-a-massive-improvement-on-statechains)
 - [Resolvr Legends of Lightning](https://www.nobsbitcoin.com/legends-of-lightning-vol-2-winners/)
 - [Aqua Wallet](https://aquawallet.io/)
