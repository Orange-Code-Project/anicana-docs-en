######################################
Requesting Matrix Development
######################################

Matrix Development
==========================
| The EGG tokens that serve as the source for generating ARCANA tokens are created by the Matrix.
| Engineers can deploy their own Matrix to the network by following specific standards.
| ※ Development engineers who have received the request will build the Matrix using the following steps.

--------------------------------

Matrix Construction Steps
==========================

The construction involves the following steps:

* Code the Matrix according to the standards (Solidity smart contract).
* Acquire ARCANA SHARD.
* Deploy the Matrix contract.
* Transfer ARCANA SHARD to the Matrix contract.
* Set the price per EGG generation in the Matrix contract.
* Set the content hash of metadata in the Matrix contract (refer to `Uploading to IPFS <../egg-management/IPFS-upload.html>`_).
* Set the SquareKey ID in the Matrix contract.
* Register the Matrix contract with the MatrixMaster contract (broadcast).
* Inform the Validator administrator of the MatrixId assigned by MatrixMaster.

--------------------------------

Matrix Standards
==========================

Refer to the `standards here <../contract-info/interfaces.html>`_.

--------------------------------

Matrix Templates
==========================

Coming soon on GitHub.
