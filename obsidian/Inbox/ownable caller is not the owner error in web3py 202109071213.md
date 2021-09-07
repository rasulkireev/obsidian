---
status:
  - writing_idea
tags:
  - code/snippet
---

When developing a [[Web3]] contract you may run into where a function is not executed because you are not an owner. This might happen if your [[Smart Contract]] inherits a Ownable class, like so:

```solidity
contract CistercianDate is ERC721URIStorage, **Ownable** {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    constructor() ERC721("Cistercian Date", "CDATE") {}

    function mintNFT(address recipient, string memory tokenURI)
        **public onlyOwner**
        returns (uint256)
    {
        _tokenIds.increment();

        uint256 newItemId = _tokenIds.current();
        _mint(recipient, newItemId);
        _setTokenURI(newItemId, tokenURI);

        return newItemId;
    }

}
```

then you would make a call with [[web3py]] that would look like that:

```python
nft_contract = w3.eth.contract(abi=contract['abi'], address=contract_address)
nft_contract.functions.mintNFT(PUBLIC_KEY, tokenURI).estimateGas()
```

this might give you a following error:
> web3.exceptions.ContractLogicError: execution reverted: Ownable: caller is not the owner

Well, to resolve this issue you can simply add the from key to the estimateGas() function, like so:

```python
nft_contract.functions.mintNFT(PUBLIC_KEY, tokenURI).estimateGas()
```