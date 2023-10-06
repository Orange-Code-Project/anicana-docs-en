###########################
Get a List of Owned EGGs
###########################

Sample to retrieve a list of EGGs currently owned by the user.

Please refer to the contract, JSON-RPC, and ABI files for test environment information.

.. caution::
   Please use web3 version 1.9.8.

------------------------------------------------------------------------------------------------------------------------------------------

Example of Retrieving a List of EGGs (JavaScript)::

        var Web3 = require('web3');
        var eggAbi = require("./egg.json");

        const web3 = new Web3("https://stgchains.anicana.org/"); // Specify the JSON-RPC URL

        const eggAddr = "0xb374640Ca3E3DA6F836ca8c60130fCAE2da3B929"; // Specify the address of the Egg contract
        const holderAddr = "0xe092b1fa25DF5786D151246E492Eed3d15EA4dAA"; // Address for which you want to check the EGG ownership

        const eggContract = new web3.eth.Contract(eggAbi, eggAddr);

        const listOfEggs = async () => {

            var balance = await eggContract.methods.balanceOf(holderAddr).call();
            console.log(balance);

            var eggIds = [];
            for (var i = 0; i < balance; i++) {
                var res = await eggContract.methods.tokenOfOwnerByIndex(holderAddr, i).call();
                eggIds.push(res);
            }

            console.log(eggIds);
        }

Batch Retrieval of Owned EGGs Function::

        @param account Address of the account holding the tokens
        @param index Index number of the token to retrieve
        @param limit Maximum number of tokens to retrieve
        @return Array of token information
        // You can retrieve up to around 1000 tokens in one call. The limit depends on the state of the smart contract, but if you exceed the limit, an error will be returned.
        function tokenOfOwnerByIndexBatch(address owner, uint256 index, uint256 limit) public view returns (uint256[] memory)