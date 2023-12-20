#####################################
Generating and Distributing PERSONA
#####################################

Overview Diagram
============================================

.. image:: ../img/PERSONA/personaMint.png

--------------------------------------------------------------------------------------------------------------------------------

Generating PERSONA
============================================
| Generating PERSONA requires consuming ANIMA. The initial attributes are determined based on the amount of ANIMA deposited during minting. A higher deposit results in higher attribute values.
| The deposit amount can be set within the range specified by the seat number of the Knight to which you belong.
| The distribution ratio of attributes other than FORCE can be determined by the publisher, while FORCE has a fixed ratio.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Absorbing
============================================
Refer to `here <../game-development/persona-absorb.html>`_ for details.

--------------------------------------------------------------------------------------------------------------------------------

PERSONA Contract
=============================================================

■ Functions for Publishers

Generating PERSONA (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param to The address where PERSONA is generated.
         @param fromId The starting value of the ID portion of the minted Persona. The generated Persona token ID has the following structure for 256-bit data:
         The token ID of the generated persona token has a value from fromId to fromId + numTokens - 1
         All IDs must be unused.
          255                     32 31         16 15          0
         +--------------------------+-------------+-------------+
         |  persona id in contents  | square key  | contents id |
         +--------------------------+-------------+-------------+
         @param numTokens The number of Persona tokens to mint.
         @param conditions MintCondition
         @return An array of generated Persona token IDs.
         function mintBatch(address to, uint256 fromId, uint256 numTokens, MintCondition[] calldata conditions) public onlyMinter returns (uint256[] memory tokens)

Generating PERSONA (No Array Version) (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         function mintBatchUnified(address to, uint256 fromId, uint256 numTokens, MintCondition calldata condition) public returns (uint256[] memory tokens)

.. admonition:: Determining fromId

  The fromId used for minting can be obtained using the findAvailableIds function described below.

MintCondition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param animaAmounts The amount of Anima tokens to be deposited for minting each Persona. The array's length must be numTokens.
         The total amount of anima in this array must be approved to the Persona contract before calling this function.
         The deposit amount must be within the minimum and maximum deposit limits set for the square key's associated Knight's seat.
         @param weightsList Weight allocation for the attributes of each generated Persona. The array's length must be numTokens. Each element has the following structure:
         weights[n][0] Weight of ABS for the nth generated persona
         weights[n][1] Weight of DFT for the nth generated persona
         weights[n][2] Weight of MND for the nth generated persona
         weights[n][3] Weight of INT for the nth generated persona
         weights[n][4] Weight of EXP for the nth generated persona

         struct MintCondition {
             uint256  animaAmounts; // Amount of anima deposited
             uint64   elements;     // Specify the element (0~6)
             uint8[5] weights;      // Weight allocation for the attributes of each generated Persona
             string   metadata;     // Set metadata
         }

| ※ Elements can be specified for PERSONA as described in the `lottery probability table of Elements <../contract-info/attributes.html>`__.

About PERSONA's Attribute Values::

        PERSONA has six attribute values as parameters:
        Attribute values are subject to increase or decrease through Absorbing.
        These attributes are also used as conditions for DrawChain execution.

            FOR (Force/Energy)
            ABS (Abyss)
            DFT (Determination)
            MND (Mind)
            INT (Intelligence)
            EXP (Experience)

Attribute Value Assignment:: 

        The total attribute value is determined by the amount of anima that is put in when minting Persona.
        When minting a persona, the amount of anima input determines the total attribute values.
        The higher the input amount, the higher the total attribute values of the generated persona.
        The amount of anima input can be set within the range set by the Knight's seat number.
        Based on the total of these attribute values, each attribute value is determined according to the allocation weight set at the time of minting.
        Since FOR is a fixed allocation (1/6 of the total value), an allocation is set for the remaining attribute values.
        The maximum value for each attribute is 4195.
        Example)
        　Input ANIMA amount: 10
        　Allocation Weight[ABS,DFT,MND,INT,EXP][2,1,1,1,1,1].
        　⇒Total value: 549
        　Attribute value of presona generated [FOR,ABS,DFT,MND,INT,EXP][91,152,76,76,76,76].
        
        See the following figure for the relationship between the amount of ANIMA input and the total attribute values

.. image:: ../img/PERSONA/mint.png

.. csv-table::
    :header-rows: 1
    :align: center

    Input ANIMA amount,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,52,54,56,58,60,62,64,66,68,70,72,74,76,78,80,82,84,86,88,90,92,94,96,98,100,105,110,115,120,125,130,135,140,145,150,155,160,165,170,175,180,185,190,195,200,210,220,230,240,250,260,270,280,290,300,310,320,330,340,350,360,370,380,390,400,420,440,460,480,500,520,540,560,580,600,620,640,660,680,700,720,740,760,780,800,820,840,860,880,900,920,940,960,980,10000,10200,10400,10600,10800,11000,11200,11400,11600,11800,12000,12200,12400,12600,12800,13000,13200,13400,13600,13800,14000,14200,14400,14600,14800,15000,15200,15400,15600,15800,16000,16400,16800,17200,17600,18000
    Total value,355,452,549,645,742,839,935,1032,1129,1226,1322,1419,1516,1612,1709,1806,1902,2000,2040,2080,2120,2160,2200,2240,2280,2320,2360,2400,2440,2480,2520,2560,2600,2640,2680,2720,2760,2800,2840,2880,2920,2960,3000,3040,3080,3120,3160,3200,3240,3280,3320,3360,3400,3440,3480,3520,3560,3600,3640,3680,3720,3760,3800,3840,3880,3920,3960,4000,4050,4100,4150,4200,4250,4300,4350,4400,4450,4500,4550,4600,4650,4700,4750,4800,4850,4900,4950,5000,5050,5100,5150,5200,5250,5300,5350,5400,5450,5500,5550,5600,5650,5700,5750,5800,5850,5900,5950,6000,6058,6117,6175,6234,6292,6351,6409,6468,6526,6585,6626,6668,6709,6751,6792,6834,6875,6917,6958,7000,7032,7064,7096,7128,7161,7193,7225,7257,7289,7322,7348,7374,7400,7427,7453,7479,7506,7532,7558,7585,7607,7629,7651,7673,7696,7718,7740,7762,7784,7807,7826,7845,7864,7884,7903,7922,7942,7961,7980,8000,8000,8000,8000,8000,8000

About Metadata::

         Set metadata using the following steps:
         ・Upload the desired image to IPFS and obtain the hash.
         ・Upload a JSON file to IPFS and obtain the hash.
         ・Set the obtained hash in the metadata.
         The JSON file format should be as follows:
         
         {
             "name": "persona", // Persona's name
             "creator": "user", // Creator's name
             "image": "QmYCQ3oX4M8snuesMah8cCfH5z9wuDWZm9rxLmZT5z1BzH", // Hash of the uploaded image
             "description": "" // Description
         }

Setting Mutable Metadata (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param tokenId PersonaTokenID
         @param metadata Metadata to set
         function setMutableMetadata(uint256 tokenId, string memory metadata)

Getting Metadata (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param tokenId PersonaTokenID
         @return immutableMetadata, mutableMetadata
         function getMetadata(uint256 tokenId) public view returns (string memory immutableMetadata, string memory mutableMetadata)

Finding Available PERSONA IDs (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param _fromId Starting tokenId
         @param _untilId Ending tokenId
         @param numTokens Number of tokens
         @return uint256  0: No IDs within the search range meet the conditions. Otherwise: The first available ID.
         function findAvailableIds(uint256 _fromId, uint256 _untilId, uint256 numTokens) external view returns (uint256)

Sample Usage::

         // Starting search value
         const fromId = squareKey.shln(16);
         // Ending search value
         const untilId = fromId.or(new BN('ffffffffffffffffffffffffffffffffffffffffffffffffffffffff00000000', 16));
         // Find available PERSONA IDs
         const targetId = await persona.findAvailableIds(fromId, untilId, number of tokens to search for);
         // Use the searched ID for mintBatch
         await persona.mintBatch(recipient's address, targetId, number of Persona tokens to mint, [conditions]);


Approving the Transfer of a Specific NFT to Addresses Other Than the Owner (With Signature) (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param to The address to which the transfer is allowed.
         @param tokenId PERSONA ID
         @param nonce Refer to the signature generation procedure.
         @param sig Refer to the signature generation procedure.
         function approve(address to, uint256 tokenId, uint256 nonce, bytes memory sig) public validToken(tokenId)

Transferring NFTs (With Signature) (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param from The address from which the transfer originates.
         @param to The address to which the transfer is made.
         @param tokenId PERSONA ID
         @param nonce Refer to the signature generation procedure.
         @param sig Refer to the signature generation procedure.
         function transferFrom(address from, address to, uint256 tokenId, uint256 nonce, bytes memory sig) public validToken(tokenId)

Approving the Transfer of a Specific NFT to Addresses Other Than the Owner (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param to The address to which the transfer is allowed.
         @param tokenId PERSONA ID
         function approve(address to, uint256 tokenId) public validToken(tokenId)

Transferring NFTs (Persona.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

         @param from The address from which the transfer originates.
         @param to The address to which the transfer is made.
         @param tokenId PERSONA ID
         function transferFrom(address from, address to, uint256 tokenId) public validToken(tokenId)

