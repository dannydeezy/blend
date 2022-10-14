# blend
a p2p borrowing and lending protocol

## motivation
there should be a transparent system for borrowers and lenders to find each other and make deals. the bitcoin ecosystem currently wants this because many skilled lightning node runners can earn good yield, but lack access to capital. but the protocol should extend to any type of bilateral borrowing/lending arrangement in any currency.

## how it works: messages, trust, and reputation
messages are published using the [nostr protocol](https://github.com/nostr-protocol/nostr). nostr relays gather the messages and present them to users. anybody can be a nostr relay and it is expected that several different websites emerge, each run by a different relay, each with a different style. for example some relays may be free and broadcast every request, whereas others may be more selective and only broadcast requests from borrowers who pay a fee. 

each message should have one of the following types: `OPEN_REQUEST`, `COMMENT`, `CANCEL_REQUEST`, (more to be added!).

the basic flow:
- potential borrower posts an `OPEN_REQUEST` stating their terms (this can be public or privately sent to select individuals)
- other users can publish an `COMMENT` message rating the quality of other users or the quality of their particular debt offerings
- potential lender contacts borrower (can be through nostr-native private encrypted messaging or email or telegram or anything)
- potential borrower posts a `CANCEL_REQUEST` to take down their listing

#### OPEN_REQUEST
a potential borrower will submit a message of type `OPEN_REQUEST` that will look something like this:
```
{
    "type": "OPEN_REQUEST",
    "public_key": "021c97a90a411ff2b10dc2a8e32de2f29d2fa49d41bfbb52bd416e460db0747d0d",
    "time": 1665704942626,
    "message": "Requesting 1 on-chain BTC, will pay back 1.004611 BTC in 3 weeks (5% APY)",
    "signature": "rn7wunrniuq4ppsqdhc7ag1nbrjxow74m588y8b3sw4hhun31zbwegz6cmjbwyh9nsfm53juqhfchkkffiq1cz3wop7mwxaq48bem7pt",
}
```
or this:
```
    "type": "OPEN_REQUEST",
    "public_key": "033d8656219478701227199cbd6f670335c8d408a92ae88b962c49d4dc0e83e025",
    "message": "Requesting $100 paid via Cash App, will pay back $105 in 2 days.",
    "time": 1665704952485,
    "contact": {
        "telegram": "@gambling_addict_69"
    },
    "signature": "rdu4anjhrc8unb7q71r7iqgigz9giqt68iz7mrts9g9cm48tfm7whsaz6e7cxdooosw9ut443kz3ug9jr7rgb65snt353tmeabfqbx3f"
```

#### COMMENT
comments are the backbone of the trust model, as everything is based on reputations. it is expected that publicly known people and/or trusted  companies will become credit rating agencies that rate the quality of borrowers.

a comment may look something like this:
```
{
    "type": "COMMENT",
    "public_key": "024bfaf0cabe7f874fd33ebf7c6f4e5385971fc504ef3f492432e9e3ec77e1b5cf",
    "message": "021c97a90a411ff2b10dc2a8e32de2f29d2fa49d41bfbb52bd416e460db0747d0d is a high quality lightning node run by Lightning Labs and has an A+ Deezy Score. Their recent debt offering of 1 BTC for 5% APY in 3 weeks is very low risk",
    "time": 1665705232643,
    "signature": "dhg4emzp5oqa7inxhij6szz3che1ssayc6uf4aq35ou6u7pjsctgkb1tqxzjk4bupa1ni9rfd1khwrzbd4wihtnnnm8jmytxfuwa38gu"
}
```

or this:
```
{
    "type": "COMMENT",
    "public_key": "033d8656219478701227199cbd6f670335c8d408a92ae88b962c49d4dc0e83e025",
    "message": "i've never seen 033d8656219478701227199cbd6f670335c8d408a92ae88b962c49d4dc0e83e025 before and it looks like they are a degenerate gambler. very high risk, do not recommend engaging with them.",
    "time": 1665705272643,
    "signature": "dhg4emzp5oqa7inxhij6szz3che1ssayc6uf4aq35ou6u7pjsctgkb1tqxzjk4bupa1ni9rfd1khwrzbd4wihtnnnm8jmytxfuwa38gu"
}
```

#### CANCEL_REQUEST
A `CANCEL_REQUEST` just instructs the nostr relays to stop broadcasting a previous `OPEN_REQUEST`. This preserves the privacy of the borrower and the lender. Only the borrower knows if the deal was accepted, and nobody knows who the lender is if there is one.


## legal
this is very simply freedom of speech

# TODO
hella fun stuff to do:
- do we want some "blips" or something to make this into a real protocol (if that's even necessary)?
- 