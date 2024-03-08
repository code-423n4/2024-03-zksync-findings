
## Pubdata Contents and Blobs
Given how data representation changes on the consensus layer (where blobs live) versus on the execution layer (where calldata is found), there is some preprocessing that takes place to make it compatible. When calldata is used for pubdata, we keep is as is and no additional processing is required to transform it. Recalling the above section when pubdata is sent via calldata it has the format: source byte (1 bytes) || pubdata || blob commitment (32 bytes) and so we must first trim it of the source byte and blob commitment before decoding it. A more detailed guide on the format can be found in our documentation. Using blobs requires a few more steps:
```python
ZKSYNC_BLOB_SIZE = 31 * 4096
# First we pad the pubdata with the required amount of zeroes to fill
# the nearest blobs
padding_amount = ZKSYNC_BLOB_SIZE - len(pubdata) % ZKSYNC_BLOB_SIZE)