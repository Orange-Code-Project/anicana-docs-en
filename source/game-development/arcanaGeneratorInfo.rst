####################################
ARCANA Generation Information
####################################

| For details on the mechanism of ARCANA generation, please refer to `this page <../mechanism/arcana-generate.html>`_.
| For environmental information, please refer to the respective environmental information pages.

------------------------------------
ARCANA Generation Information
------------------------------------

ARCANA generation information is managed by ArcanaGeneratorInfo and holds the following data:

InfoStatus::

         struct InfoStatus {
             Info info;   // Information as described below
             bool isDone; // true: generated, false: not generated
         }

Info::

         struct Info {
             string manaAddress;  // Mana address
             uint256 eggId;       // Egg ID used for generation
             address beneficiary; // Wallet address of the recipient (user)
             uint256 seed;        // Seed used for generation
             bytes signature;     // Signature used for generation
             uint256 timestamp;   // Timestamp
         }

■ Functions for Publishers

Get the length of the InfoStatus array::

         @param beneficiary wallet address
         @returns uint256   Length of the associated InfoStatus array
         function getInfoCountByBeneficiary(address beneficiary) public view returns (uint256)

Get InfoStatus::

         @param beneficiary wallet address
         @param startIndex  
         @param limit Number of items to retrieve
         @returns result InfoStatus[]
         function getInfoByBeneficiary(address beneficiary, uint256 startIndex, uint256 limit) public view returns (InfoStatus[] memory result)

