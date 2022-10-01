# ITMO-BC-1
ITMO Blockchain HW 1

1) https://github.com/gnosis/MultiSigWallet/blob/master/contracts/MultiSigWallet.sol - сделать, чтобы с баланса multisig-контракта за одну транзакцию не могло бы уйти больше, чем 66 ETH

```
- 193 transactionId = addTransaction(destination, value, data);

+ 193 require(value <= 66 ether);
+ 194 transactionId = addTransaction(destination, value, data);
```

2) https://github.com/OpenZeppelin/openzeppelin-contracts/blob/f2112be4d8e2b8798f789b948f2a7625b2350fe7/contracts/token/ERC20/ERC20.sol - сделать, чтобы токен не мог бы быть transferred по субботам

```
- 210 require(recipient != address(0), "ERC20: transfer to the zero address");

+ 210 require(recipient != address(0), "ERC20: transfer to the zero address");
+ 211 require(((block.timestamp / 86400) + 4) % 7 != 6);
```

3) https://github.com/mixbytes/solidity/blob/076551041c420b355ebab40c24442ccc7be7a14a/contracts/token/DividendToken.sol - сделать чтобы платеж в ETH принимался только специальной функцией, принимающей помимо ETH еще комментарий к платежу (bytes[32]). Простая отправка ETH в контракт запрещена

```
- 21 event Deposit(address indexed sender, uint256 value);
+ 21 event Deposit(address indexed sender, uint256 value, bytes[32] comment);

- 40 function() external payable {
+ 40 function deposit(bytes[32] comment) external payable {

- 42 emit Deposit(msg.sender, msg.value);
+ 42 emit Deposit(msg.sender, msg.value, comment);
```
