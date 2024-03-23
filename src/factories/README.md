## Contracts

# `E741V1Factory741`
For creating a new E741 token
  `create(bytes32 _vanitySalt, bytes _encodedParameters) returns (address e741)`
   - Create a new E741 contract according to the parameters in:
      - `_encodedParameters`. Generate `_encodedParameters` with [BytecodeGenerator](/src/utils/BytecodeGenerator.sol)
      - And with a CREATE2 salt `_vanitySalt`
        
  `predict(bytes32 vanitySalt) view returns (address e741)`
    
  - Returns the expected address of the token given a salt
     
# `E741V1Factory741w`
For creating an E741 wrapper
  `create(bytes32 _vanitySalt, bytes _encodedParameters) returns (address e741)`
   - Create a new E741 contract according to the parameters in:
      - `_encodedParameters`. Generate `_encodedParameters` with [BytecodeGenerator](/src/utils/BytecodeGenerator.sol)
      - And with a CREATE2 salt `_vanitySalt`
        
  `predict(bytes32 vanitySalt) view returns (address e741)`
    
  - Returns the expected address of the token given a salt
    
# `E741V1FactoryBase`
Parent contract for other factories

# `E741V1FactoryStorage`
For tracking and controlling factories
