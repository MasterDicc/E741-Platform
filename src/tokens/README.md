## Contracts

# `E741V1Base`
Parent contract of all E741 token contracts
  - Implements all ERC20 and ERC721 functionalities

  Internal variable `ONE` defines the ERC20 amount equivalent to one ERC721 ID where `ONE = 10 ** _decimals`

  `transfer(address to, uint amount) returns (bool)`

  - Operates as either an ERC20 transfer or ERC721 transfer
    - Acts as an ERC20 transfer when the amount entered is NOT an ERC721 ID owned by the user
      - Will transfer `amount` tokens and `n` IDs where `n = amount / ONE` via `_transfer741`
    - Acts as an ERC721 transfer if the specific amount is an ID owned by the user
      - Will use `amount` as the token ID and will also transfer ONE tokens
        
  `transferFrom(address from, address to, uint amount) returns (bool)`
  - Same operation as transfer but with added approval checks
    - If treated as an ERC20 transfer, the spender must be approved as if an ERC20
    - If treated as an ER721 transfer, the spender must be approved for the give ID or all

  `safeTransferFrom(address from, address to, uint256 tokenId, bytes memory data)`
  - Operates only as an ERC721 and transfers ONE tokens

  `address public constant BROKEN_ADDRESS = address(0x5e7ec)`
  
  This is the broken IDs address. When a user breaks an ID inside `_transfer741` it is teporarily stored at this address. Commonly used in `brokenIDsArray = ownedNfts[BROKEN_ADDRESS]`
  
  `_transfer741(address from, address to, uint amount) internal`

  The internal function defining the relationship between ERC20 and ERC721 transfers. Only called when an ERC20 transfer is performed.

  1. Preforms a simple ERC20 transfer
  2. Compares starting and ending balances to "break" or "make" a token as needed
     - When the `from` user's balance rolls under a multiple of `ONE` tokens, then "break" a token ID (if they have one) and add it to the brokenIDsArray
     - When  the `to` user's s balance rolls over a multiple of `ONE` tokens, they "make" a token ID from either the brokenIDsArray or by minting
  3. Check if the user has disabled minting and, if so, adjust their ID transfer amount to only include their owned IDs
  4. Distribute token IDs from `from` to `to` according to the following order:
     1. Transfer IDs alread owned by `from`
     2. "Make" tokens from the brokenIDsArray
     3. Mint new token IDs to `to`
  
# `E741V1Token`
Simple implementation of `E741V1Base`
For creating an E741 wrapper
  `initialize(bytes memory encodedParameters)`
   - Initialize the token contract:
      - `_encodedParameters` represent the properties of the token. Generate `_encodedParameters` with [BytecodeGenerator](/src/utils/BytecodeGenerator.sol)
    
# `E741V1Wrapped741`
Implementation of the E741 wrapper. Can take any E741 and wrap it into a new E741.

  `initialize(bytes memory encodedParameters)`
   - Initialize the token contract:
      - `_encodedParameters` represent the properties of the token. Generate `_encodedParameters` with [BytecodeGenerator](/src/utils/BytecodeGenerator.sol)
    
  `function deposit(uint[] memory _amountsArray) public`
  
  For wrapping E741 tokens. Has 2 input modes:
  
  1. ERC20 deposit - For when a user wishes to deposit multiple tokens with no concern for which IDs
    
  - `_amountsArray` must be a length of 1
  - `_amountsArray[0]` represents the eth20 amount being wrapped
    
  2. ERC721 deposit - For when a user wishes to deposit specific IDs
  
  - `_amountsArray` represents a list of all erc721 IDs the user wants to wrap

  `function withdraw(uint[] memory _amountsArray) public`
  
  For unwrapping wrapped E741 tokens returning the underlying E741. 
  
  Has same input options as `deposit()`
  
  Takes a fee of `withdrawalFees` where `0.05% <= withdrawalFees <= 0.5%`



  
