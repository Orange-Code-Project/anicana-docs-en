#######################################
Signature Generation Procedure
#######################################

In order to generate an ARCANA token, the Validator (on the content side) needs to allow the user to convert their EGG token into ARCANA. Additionally, during this process, it is necessary to embed the result value of the content into the ARCANA token without tampering with this value. To achieve this, the following procedure is performed: the content side creates a signature, and the user uses this signature to send a transaction. The private key of the EGG ID owner can be obtained from a dedicated website.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Creation of Signature Data for ARCANA Generation
======================================================================

To create signature data, the following data is required.

.. csv-table:
    :header-rows: 1
    :align: center

    Parameter, Description
    eggid,       ID of the target EGG token
    toAddr,      Address where ARCANA will be generated (recipient of EGG unlock permission)
    seed,        Result value of the content
    contract,    Incubator contract address
    privateKey,  Private key of the EGG ID owner. Prefix it with "0x" as obtained from the dedicated site.

Based on the above data, create the dataToBeSigned, which is the data to be signed, using the following steps::

    const genSig = require("./genSig.js");

    const signature = genSig.signForIncubate(eggid, toAddr, seed, contract, privateKey);

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Creation of Signature Data for PERSONA Distribution
======================================================================

.. csv-table:
    :header-rows: 1
    :align: center

    Parameter, Description
    from,       Address of the PERSONA token holder
    to,         Address where the PERSONA token will be transferred
    tokenId,    ID of the target PERSONA token
    contract,   PERSONA contract address
    privateKey, Private key of the PERSONA token owner. Prefix it with "0x" as obtained from the dedicated site.

Based on the above data, create the signature data using the following steps::

    const genSig = require("./genSig.js");

    const sigInfoApp = genSig.signForPersonaApprove(to, tokenId, contract, privateKey);

    const sigInfoAppNonce = sigInfoApp.nonce;
    const sigInfoAppSign  = sigInfoApp.sign;

    const sigInfoTrans = genSig.forPersonaTransferFrom(from, to, tokenId, contract, privateKey);

    const sigInfoTransNonce = sigInfoTrans.nonce;
    const sigInfoTransSign  = sigInfoTrans.sign;

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Libraries
======================================================================

Refer to the environmental information.