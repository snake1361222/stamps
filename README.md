
# STAMPS: A Protocol for Storing Images On-Chain in Transaction Outputs Immutably on Bitcoin

**IMPORTANT NOTICE: STAMPS IS A BLOCKCHAIN-AGNOSTIC PROTOCOL.<br>
FOR RULES SPECIFIC TO THE BITCOIN STAMPS PROJECT, PLEASE VISIT:<br>
https://github.com/mikeinspace/stamps/blob/main/BitcoinStamps.md**

Storing "Art on the Blockchain" as a method of achieving permanence is often a misnomer in the NFT world. Most NFTs are merely image pointers to centralized hosting or stored on-chain in prunable witness data. We propose a method of embedding base64-formatted image data using transaction outputs in a novel fashion.

The means by which this is achieved is encoding an image's binary content to a base64 string, placing this string as a suffix to `STAMP:` in a transaction's description key, and then broadcasting it using the Counterparty protocol onto the Bitcoin ledger. The length of the string means that Counterparty defaults to bare multisig, thereby chunking the data into outputs rather than using the limited (and prunable) OP_RETURN. By doing so, the data is preserved in such a manner that is impossible to prune from a fullnode, preserving the data immutably forever.

Given the cost of preserving data in this manner, we suggest the following guidance: 24x24 pixel, 8-colour-depth PNG or GIF. The constraints of this "canvas" are ideal for pixel art. In particular, the CryptoPunks use a native resolution of 24x24 pixels.

STAMPS will be numbered based on the transaction timestamp. This is to ensure that the STAMPS directory is ordered chronologically. The first STAMP will be the first transaction to include the `STAMP:` string with a valid base64 string appended in the description key, and so on. A transaction with an invalid or indecipherable base64 string will not be considered a STAMP. The STAMP number will begin at zero and continue indefinitely.

## What Makes a STAMP?

A STAMP is a Counterparty transaction which contains a valid `STAMP:base64` string in the description key. STAMPS can be decoded directly from the original Bitcoin transaction. In order for speed of processing and to eliminate needs for indexing, we are utilizing Counterparty API to decode the original Bitcoin transactions. Once the decoding is complete, we upload the images to stampchain.io for consumption via web applications as a convenience. It is intended that anyone may decode these transactions and interpret the underlying image data for rendering on any application. 

## STAMPS abide by the following rules:

- The image data must be in either jpg, png, gif or webP format and encoded in base64.

**Recommended Format:**

- `STAMP:<base64 data>`

Example:

- `STAMP:iVBORw0KGgoAAAANSU...`

## Potential Future State formatting:

Warning: Do not try this until its actually approved. Doing so may result in an invalid STAMP as plans may change.

- `STAMP:data:image/png;base64,iVBORw0KGgoAAAANSU...`

## Decoding a STAMP

A raw bitcoin transaction may be decoded using tools such as:

https://jpja.github.io/Electrum-Counterparty/decode_tx.htm

This will reveal the description field of the STAMP transaction. The description field will contain the base64 string. This string can be decoded using any base64 decoder. 

## Absence of MIME-type and encoding

Our rationale for excluding both the MIME-type and encoding goes as follows:

- The fewer the bytes the better.
- Given the limited scope of acceptable file formats, we are confident that decoding them accurately based on the base64 string alone is trivial.
- We are only interested in decoding base64, so if the string does not conform to valid base64 it is rejected. Therefore, specification of the encoding is unnecessary.

This all pertains to current state. The future-state proposal would require a MIME-type like 'text/plain' for the auxilary content to be decoded.

## XCHAIN-specific markup

While no specific markup should be required, STAMPS are purposely designed to be very small in the range of 24x24 pixels. While they can be presented at this size or even scaled-up using the traditional method, the user experience would be sub-optimal. Using a few simple CSS rules will optimize the rendering. Eg: image-rendering: pixelated;

Visual example of pixel art scaling without image degradation: https://i.imgur.com/CGLqw11.jpg

## Trading

Users are able to trade the token on the Counterparty DEX, Dispensers or OTC or any other method as traditional Counterparty assets.

