## E741 - Multi token standard

E741 is an implementation of a combined ERC20 and ERC721 token

- ERC20 and ERC721 transfers directly affect each other
- Token IDs preserved on all transactions
- 1.0 ERC20 transfer = 1 ERC721 transfer (ID chosen from a holdings list)
- 1 ERC721 transfer = 1.0 ERC20 transfer
- 
# Contracts

E741 contracts are found in src

```ml
src
├─ factories
  ├─ E741V1Factory741 - "Create new E741 from scratch"
  ├─ E741V1Factory741w - "Wrap existing E741 into another E741"
  ├─ E741V1FactoryBase - "Parent contract for factory implementations"
  └─ E741V1FactoryStorage - "For tracking tokens created with the factories"
├─ interfaces
├─ tokens
  ├─ E741V1Base - "Parent contract for token implementations"
  ├─ E741V1Token - "Basic E741 implementation"
  ├─ E741V1Wrapped741 - "Wrapped E741 implementation"
  └─ Emeralds - "The Emeralds contract"
└─ utils
  └─ BytecodeGenerator - "For deriving encoded bytes for contract initialization"

```
