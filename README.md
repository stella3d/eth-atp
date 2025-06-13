# ATProto for Ethereum People

how can we make Ethereum community members feel like atproto aligns better with the existing values around "decentralization"?

part technical link, part vibes.

## Onboarding Gateway

The onboarding gateway is a static web page hosted on IPFS, but usually accessed thru some sort of .eth url - atproto-gateway.eth.limo or similar.

it's not necessary technically to use the ENS link - it's for social signaling / vibes.

### Keys 

The gateway must generate a self-custodied rotation key for the user's new did, where you have to write down a seed. This key must be registered in the user's DID document.

This part is important both technically and socially.

#### Technical

Ensuring that all users onboarded this way have self-custodied rotation keys is a genuine improvement in decentralization vs the status quo on Bluesky, where most users do not have their own rotation keys.
This can help us avoid future arguments around decentralization of atproto.

#### Social

Self-custody of the keys aligns tightly with existing ideas & practices in Ethereum. Pretty much anyone with a wallet is self-custodying the keys for their wallet. 
This is important for a few reasons:

1) it's much easier to convince these users to self-custody. you don't have to argue about it with them.
2) writing down the seed _feels_ like crypto. 
3) "not your keys not your posts"

## DID Setup

We currently have an open question around what sort of DID we setup for users. We have two obvious options, which are not mutually exclusive:

1) use `did:plc` with self-custodied keys. 

This can be accomplished by constructing a correct, signed did document and posting it to https://plc.directory/:did 

PLC doesn't verify `alsoKnownAs` field on creation - we need to do the handle validation check in our frontend to ensure that users get valid handles.

2) use `did:web` with a `*.eth.limo`/`*.eth.xyz` domain. 

This requires an on-chain action. TODO: need someone who understand this part to fill it in.


