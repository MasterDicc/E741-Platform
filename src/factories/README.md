## Contracts

# `E741V1Factory741`
  `create(bytes32 _vanitySalt, bytes _encodedParameters) returns (address e741)`
   - Create a new E741 contract according to the parameters in:
      - `_encodedParameters`. Generate `_encodedParameters` with [BytecodeGenerator](/src/utils/BytecodeGenerator.sol)
      - And with a CREATE2 salt `_vanitySalt`
  `predict(bytes32 vanitySalt) view returns (address e741)`
      Returns the expected address give a salt
# `E741V1Factory741w`
  `create(bytes32 _vanitySalt, bytes _encodedParameters) returns (address e741)`
   - Create a new E741 contract according to the parameters in:
      - `_encodedParameters`. Generate `_encodedParameters` with [BytecodeGenerator](/src/utils/BytecodeGenerator.sol)
      - And with a CREATE2 salt `_vanitySalt`
  `predict(bytes32 vanitySalt) view returns (address e741)`
      Returns the expected address give a salt
# `E741V1FactoryBase`

# `E741V1FactoryStorage`
