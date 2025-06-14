# ATProto for Ethereum People

how can we make Ethereum community members feel like atproto aligns better with the existing values around "decentralization"?

part technical link, part vibes.

## Onboarding Gateway

The onboarding gateway is a static web page hosted on IPFS, but usually accessed thru some sort of .eth url - atproto-gateway.eth.limo or similar.

Associating a .eth link to a CID on ipfs work:

 * Make a static website consisting of a `.well-known/atproto-did` file containing the DID and pin it with some pinning service. [See Example](https://bot.reality.eth.link/.well-known/atproto-did). If they already have a static website but without an `atproto-did` file it needs to be added to the existing static website. 
 * Have the ENS owner set the `Content Hash` record for their domain. They can do this manually by going to the records page of their domain on the ENS site - [see example](https://app.ens.domains/bot.reality.eth?tab=records) - or we can try to send the transaction from our page and open a Metamask window etc.
 * The DID will show up on both `.eth.limo` and `.eth.link` gateways. (It might take a bit of time but it should be under a minute.)

It's not necessary technically to use the ENS link - it's for social signaling / vibes. But everyone will need some kind of handle and using bsky.social would be weird so maybe if you don't have an ENS we should issue you one as a subdomain?

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

PLC doesn't verify `alsoKnownAs` field on creation - we need to do the handle validation check in our frontend to ensure that users get valid handles if they are bringing a `.eth` based domain, or another custom domain.

2) use `did:web` with a `*.eth.limo`/`*.eth.xyz` domain. 

This requires an on-chain action. TODO: need someone who understand this part to fill it in.

## PDS

There are 3 options for PDS hosting for users we onboard, also not mutually exclusive.

### Use a bsky PDS

This is the easiest path, but also probably the worst one in terms of appealing to the Ethereum community, because it's a bit less decentralized. It would be a missed opportunity to contribute to the decentralization of PDS hosting on the network.

### Create a hosted PDS

This has significantly more effort, including ongoing ops work to make sure the PDS is reliable. 

This seems like the best option if we can pull it off. Ethereum community appeal would be higher than using a bsky PDS, and the barrier to onboarding successfully is _much_ lower than having users self-host.

The initial cost to run this is something we can easily eat. We could setup a multisig wallet with an ENS to take donations to cover ongoing costs, and i think we'd get enough tokens donated to cover things easily. 

My main concern with this would be the ongoing ops/reliability work - none of the initial people working on this are really ops-focused, and i don't want to be on-call for people being able to post.

### User brings a PDS

This is maximally decentralized, and doesn't incur the necessity of ongoing ops work to keep the PDS online. 

However, almost no user that hasn't been onboarded will do this. It's rare enough even among dedicated atproto people. This might be better to add support for later, if we get initial traction.

## Community UX Defaults ?

There's a few changes to the default user experience that would probably make the environment more welcoming. 

### Unpin Discover Feed

The "Discover" feed on bluesky is default and a common source of perception complaints about bluesky. we want to avoid having users argue about this point.

I've asked @why.bsky.team if it's possible to onboard users without this feed pinned, we'll see what he says.

### Default Blocklist 

Bluesky, as a moderately large public social media, has plenty of people who are really weird about crypto. We can somewhat solve this, at least well enough to improve the initial experience, by having a suggested blocklist for the most prominent anti-crypto reactionaries. An open question is whether we can default subscribe new users to this sort of list, or merely suggest it.

### Starter Packs ?

The counterpoint to a default blocklist is probably community starter packs. Tree made one a while ago: https://bsky.app/starter-pack/tree.fail/3lapya53cvo2s
