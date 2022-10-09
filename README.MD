# Sibiryakov Ilya M3337 HW1

## Task 1

https://github.com/gnosis/MultiSigWallet/blob/master/contracts/MultiSigWallet.sol - сделать, чтобы с баланса
multisig-контракта за одну транзакцию не могло бы уйти больше, чем 66 ETH

```
[+] modifier validateMaxValue(uint value) {
[+]    require(value < 67 ether);
[+]    _;
[+] }

[-]     transactionId = addTransaction(destination, value, data);
[+]     validateMaxValue(value)
[+]     transactionId = addTransaction(destination, value, data);
```

## Task 2

https://github.com/OpenZeppelin/openzeppelin-contracts/blob/f2112be4d8e2b8798f789b948f2a7625b2350fe7/contracts/token/ERC20/ERC20.sol - 
сделать, чтобы токен не мог бы быть transferred по субботам

```
[+] function _isNotSaturday(uint timestamp) internal pure returns (bool) {
[+]     return ((timestamp / 86400 + 4) % 7) != 6;
[+] }

[-]     _beforeTokenTransfer(sender, recipient, amount);
[+]     require(_isNotSaturday(block.timestamp), "Can't make transfer in Saturday")
[+]     _beforeTokenTransfer(sender, recipient, amount);
```

## Task3

https://github.com/mixbytes/solidity/blob/076551041c420b355ebab40c24442ccc7be7a14a/contracts/token/DividendToken.sol -
сделать чтобы платеж в ETH принимался только специальной функцией, принимающей помимо ETH еще комментарий к платежу `(
bytes[32])`. Простая отправка ETH в контракт запрещена

```
[-] event Deposit(address indexed sender, uint256 value);
[+] event Deposit(address indexed sender, uint256 value, bytes[32] comment);

[-] function() external payable {
[+] function deposit(bytes[32] comment) external payable {

[-]     emit Deposit(msg.sender, msg.value);
[+]     emit Deposit(msg.sender, msg.value, comment);
```