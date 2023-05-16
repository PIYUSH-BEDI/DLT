# DLTlab-
Experiments of DLT Lab 


### Exp-2  Deploy a smart contract on the Ethereum blockchain using the Solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyContract {
    uint256 public myNumber;

    string public person="Hello World !!";

    constructor(uint256 _number) {
        myNumber = _number;
    }
}
```

### Exp-3 DAPP in Solidity
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyToken {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 public totalSupply;
    
    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;
    
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    
    constructor(string memory _name, string memory _symbol, uint8 _decimals, uint256 _initialSupply) {
        name = _name;
        symbol = _symbol;
        decimals = _decimals;
        totalSupply = _initialSupply * (10 ** uint256(decimals));
        balanceOf[msg.sender] = totalSupply;
    }
    
    function transfer(address _to, uint256 _value) public returns (bool) {
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");
        _transfer(msg.sender, _to, _value);
        return true;
    }
    
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool) {
        require(balanceOf[_from] >= _value, "Insufficient balance");
        require(allowance[_from][msg.sender] >= _value, "Not allowed to transfer");
        _transfer(_from, _to, _value);
        _approve(_from, msg.sender, allowance[_from][msg.sender] - _value);
        return true;
    }
    
    function approve(address _spender, uint256 _value) public returns (bool) {
        _approve(msg.sender, _spender, _value);
        return true;
    }
    
    function _transfer(address _from, address _to, uint256 _value) internal {
        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
        emit Transfer(_from, _to, _value);
    }
    
    function _approve(address _owner, address _spender, uint256 _value) internal {
        allowance[_owner][_spender] = _value;
        emit Approval(_owner, _spender, _value);
    }
}
```
### Exp-4 Basic Functions in Solidity
```
pragma solidity ^0.8.0;

contract BasicFunctions {
    uint256 public myNumber;
    string public myString;
    bool public myBoolean;
    address public myAddress;
    mapping(address => uint256) public myMapping;
    uint256[] public myArray;
    
    constructor() {
        myNumber = 0;
        myString = "";
        myBoolean = false;
        myAddress = address(0);
    }
    
    function setNumber(uint256 _number) public {
        myNumber = _number;
    }
    
    function setString(string memory _string) public {
        myString = _string;
    }
    
    function setBoolean(bool _boolean) public {
        myBoolean = _boolean;
    }
    
    function setAddress(address _address) public {
        myAddress = _address;
    }
    
    function addToMapping(address _address, uint256 _value) public {
        myMapping[_address] = _value;
    }
    
    function addToArray(uint256 _value) public {
        myArray.push(_value);
    }
}
```
### Exp-6 Inheritance 
```
pragma solidity ^0.8.0;

contract Parent {
    uint256 public parentVariable;
    
    function modifyParentVariable(uint256 _value) public {
        parentVariable = _value;
    }
}

contract Child is Parent {
    uint256 public childVariable;
    
    function modifyParentVariable(uint256 _value) public override {
        childVariable = _value;
    }
}
```

### Exp-9 Different Data Locations

```
// SPDX-License-Identifier: MIT
pragma solidity >=0.5.0 <0.9.0;

contract DataLocations {
    uint256 public storageVariable; // Stored in storage
    
    function setStorage(uint256 _value) public {
        storageVariable = _value;
    }
    
    function getStorage() public view returns (uint256) {
        return storageVariable;
    }
    
    function sum(uint256 a, uint256 b) public pure returns (uint256) {
        uint256 result = a + b; // Stored in memory
        return result;
    }
    
    function concatenate(string calldata _str1, string calldata _str2) public pure returns (string memory) {
        bytes memory str1Bytes = bytes(_str1); // Stored in calldata
        bytes memory str2Bytes = bytes(_str2); // Stored in calldata
        
        string memory concatenated = new string(str1Bytes.length + str2Bytes.length);
        bytes memory concatenatedBytes = bytes(concatenated);
        
        uint256 k = 0;
        for (uint256 i = 0; i < str1Bytes.length; i++) {
            concatenatedBytes[k++] = str1Bytes[i];
        }
        for (uint256 i = 0; i < str2Bytes.length; i++) {
            concatenatedBytes[k++] = str2Bytes[i];
        }
        
        return string(concatenatedBytes);
    }
}
```

### Lab-10 Supply Chain Management 
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SupplyManagementSystem {
    struct Product {
        uint256 quantity;
        bool exists;
    }
    
    mapping(uint256 => Product) public products;
    
    function addProduct(uint256 _productId, uint256 _quantity) public {
        require(!products[_productId].exists, "Product already exists");
        
        Product memory newProduct = Product({
            quantity: _quantity,
            exists: true
        });
        
        products[_productId] = newProduct;
    }
    
    function updateProductQuantity(uint256 _productId, uint256 _newQuantity) public {
        require(products[_productId].exists, "Product does not exist");
        
        products[_productId].quantity = _newQuantity;
    }
    
    function getProductQuantity(uint256 _productId) public view returns (uint256) {
        require(products[_productId].exists, "Product does not exist");
        
        return products[_productId].quantity;
    }
}
```
