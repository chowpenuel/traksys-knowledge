# Calculation Tag

## Summary

### Entity Name

Calculation Tag

### Database Table Name

`tTag`, `tTagCalculation`

### API Object Name

`DbTagCalculationComposite`

### Entity Description

Calculation Tags perform simple arithmetic and string operations on two input Tags. Supported arithmetic operations include addition, subtraction, multiplication, division, modulus, and random number generation. String operations include concatenation and left and right substring extraction.

## Properties

`Left Operand [ LeftTagID or LeftConstant ]`

Value of the left (first) operand of the calculation, which may be a constant or the value of another Tag. This setting must have a valid Data Type for the specified Operation.

`Operation [ Operation ] : ETS.Core.Enums.TagCalculationOperation`

Calculation Operation to perform on the Left and Right Operands.

**'+' Add (Integer or Float)** - Adds the value of the Left Operand and the Right Operand, and returns the result.

**'-' Subtract (Integer or Float)** - Subtracts the value of the Right Operand from the value of the Left Operand, and returns the result.

**'\*' Multiply (Integer or Float)** - Multiplies the value of the Left Operand by the value of the Right Operand, and returns the result.

**'/' Divide (Integer or Float)** - Divides the value of the Left Operand by the value of the Right Operand, and returns the result.

**'%' Modulus (Integer or Float)** - Divides the value of the Left Operand by the value of the Right Operand, and returns the remainder. Example: 10 % 3 = 1.

**Concatenate (String)** - Concatenates (combines) the string value of the Left Operand with the string value of the Right Operand, and returns the result. Example: "thermo" CONCAT "former" = "thermoformer".

**Left**

**Left Operand: String**

**Right Operand: Integer**

**Result: String**

Extracts a substring from the string value of the Left Operand, using the leftmost number of characters specified by the value of the Right Operand. Example: LEFT("thermoformer", 6) = "thermo".

**Right**

**Left Operand: String**

**Right Operand: Integer**

**Result: String**

Extracts a substring from the string value of the Left Operand, using the rightmost number of characters specified by the value of the Right Operand. Example: RIGHT("thermoformer", 6) = "former".

**Random (Integer or Float)** - Generates a random number every Logic Service scan, using the value of the Left Operand as the minimum possible value and the value of the Right Operand as the maximum possible value.

`Right Operand [ RightTagID or RightConstant ]`

Value of the right (second) operand of the calculation, which may be a constant or the value of another Tag. This setting must have a valid Data Type for the specified Operation.
