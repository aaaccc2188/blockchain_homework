# ZBCoin - Proof of Authority Development Chain

For this assignment, I have set up a private testnet blockchain for ZBank.

---

## Environment Setup Instructions and Dependencies

### Installing MyCrypto Desktop App

Download [MyCrypto](https://www.mycrypto.com/) Desktop App to manage ethereum wallets and make transactions in the blockchain.

### Go Ethereum Tools

[Go Ethereum](https://geth.ethereum.org/) is one of the three original implementations of the Ethereum protocol. It is written in Go, fully open-source and licensed under the GNU LGPL v3. Go Ethereum Tools are included in the [zbcoin](zbcoin) folder.

## Launch the Testnet

**Important Note:** Windows users **MUST** use `git-bash` and not the default Windows command prompt when you are requested to open the terminal window to execute commands.

### Configuration of the ZBCoin testnet

   ![testnet_config](Screenshots/zbcoin_config.PNG)

### Start Node1 

* Open a terminal window, navigate to the zbcoin folder and run the following command: 

   ```bash 
   ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
   ```

* Substitute the "SEALER_ONE_ADDRESS" with the the public address of the first node listed in [Keys](zbcoin/Keys.txt) (do **not** include the leading `0x`). 

* **Important:** Type your password and hit enter - _even if you don't see a prompt!_ (password in [Keys](zbcoin/Keys.txt))

* Copy the resulting enode address from the terminal:

   ![enode](Screenshots/enode.PNG)

### Start Node2

* Open another terminal window, navigate to the zbcoin folder and run the following command: 

   ```bash     
   ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
   ```

* Substitute the "SEALER_TWO_ADDRESS" with the the public address of the second node listed in [Keys](zbcoin/Keys.txt) (do **not** include the leading `0x`).

* Substitute the "SEALER_ONE_ENODE_ADDRESS" with the enode address of node 1 that was copied in step 1.  

* **Important**: Type your password and hit enter - _even if you don't see a prompt!_ (password in [Keys](zbcoin/Keys.txt))

* The chain should be up and running after you start the second node.

---

## Send a test transaction

With both nodes up and running, the blockchain can be added to MyCrypto for testing.

* Open the MyCrypto app, then click `Change Network` at the bottom left:

* Click "Add Custom Node", then add the custom network information that you set in the genesis.

   ![custom network](Screenshots/custom-network.png)

* After connecting to the custom network in MyCrypto, select the `View & Send` option from the left menu pane, then click `Keystore file`.

* On the next screen, click `Select Wallet File`, then navigate to the keystore directory inside the 'zbcoin/Node1' directory, select the file located there, provide your password when prompted and then click `Unlock`. This will open your account wallet inside MyCrypto. 
   
   ![keystore_unlock](Screenshots/balance.PNG)

* In the `To Address` box, type the account address from Node2, then fill in an arbitrary amount of ETH. Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.  

* Click the `Check TX Status` when the green message pops up, confirm the logout:

* You should see the transaction go from `Pending` to `Successful` in around the same blocktime you set in the genesis.

   ![transaction-success](Screenshots/tx_success.PNG)

* Voila, you just made the first successful transaction on ZBCoin testnet!