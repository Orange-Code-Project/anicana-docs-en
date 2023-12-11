###########################
ARCANA Generation API
###########################

You can invoke the ARCANA generation screen by embedding the following script tag in your content.

API Specifications
===========================

--------------------------------------------
Script to Invoke ARCANA Generation Page
--------------------------------------------


Sample Generation Script::

    <script src="https://staging.anicana.org/arcana.js" id="gen_arcana_script" data-requestid="9999999" data-toaddr="0xFf5BC900110f5c4eb6Ce2faf2081B4151655B3f3" data-seed="10000" data-eggid="10" data-signature="0xdfe893d3906b31c0cfcc05b05387c7cf3bf31524caeac2fb5e3d7b9d144dbc9550a9ce41d92ad4c070c6f34c38ba8329d8d1b32818f2d01a637758f61b012a211c" data-callback="https://staging.anicana.org/test_button.html" data-logout="true" ></script> 
    <div style='text-align: center'><button onclick="__go_to_arcana_generator()">Generate ARCANA</button></div>


.. csv-table::
    :header-rows: 1
    :align: center

    Parameter, required/optional, Type, Description
    id,               required, String, gen_arcana_script (Do not change)
    src,              required, URL,     {endpoint}/arcana.js (Refer to the environment information page for the endpoint)
    data-eggid,       required, Number,  The EGG eggid held by the publisher.
    data-seed,        required, Number,  Seed
    data-signature,   required, String,  Publisher's signature. Refer to the signature generation procedure page.
    callback-url,     optional, URL,     "Callback URL. The requestId and txHash will be added as GET parameters and redirected. If you specify http://test.com, it will become http://test.com?requestId=1&txHash=xxxxx. You can also omit the callback, in which case a button will be displayed to navigate to the wallet page on the portal."
    data-requestid,   required, Number,  Any number specific to the publisher (0 ~ 18446744073709551615). Used in check status.
    data-toaddr,      required, address, Wallet address for distributing ARCANA
    data-logout,      optional, boolean, "If true, forcefully trigger a re-login. If false, automatically log in if there is a session, otherwise, prompt for re-login. If not specified, it is the same as false."
    data-symbol,      optional, String,  Symbol that can be set by the publisher.
    data-manaInfo,    optional, String,  Text that can be set by the publisher. It is envisaged to add value to ARCANA by writing things like user experience information or encrypted personal information in content.
    data-manaValue,   optional, Number,  Numeric value that can be set by the publisher.
    data-manaAddress, optional, address, Specify the manaAddress of the interrupted ARCANA generation.


To directly call the generation page, do as follows::

    {endpoint}/arcana-gen/{eggId}/{seed}/{signature}/{requestId}/{toAddress}?r={callbackUrl}&logout=true

   (with mana information)
    {endpoint}/arcana-gen/{eggId}/{seed}/{signature}/{requestId}/{toAddress}/{symbol}/{manaInfo}/{manaValue}?r={callbackUrl}&logout=true

   (with manaAddress specified)
    {endpoint}/arcana-gen/{manaAddress}


.. admonition:: supplement

  - When calling the generation page directly and not specifying symbol, manaInfo, and manaValue, please insert null in the respective locations.
  - The maximum number of "manaInfo" characters is limited to the total of all request headers. Although there are some conflicts with other parameters, the maximum number of characters for symbol, manaInfo, and manaValue together should be 800 or less for Japanese and 7200 or less for single-byte alphanumeric characters.
  - The text to be displayed in the mana information is currently not line breakable.


------------------------------------------------------------------------------------------------------------------------------------------------------------------------


------------------------------------
Check Status
------------------------------------

Retrieve the status of ARCANA generation.

Method::

    GET

Endpoint::

    /api/arcana-status/{wallet_address}/{request_id}


.. csv-table::
    :header-rows: 1
    :align: center

    Parameter, Description
    wallet_address, Address of the signer (address of the EGG holder)
    request_id, Request ID specified when calling the ARCANA generation API


Sample response

.. code-block:: json

    {
        "data": {
            "status": "done",
            "transaction_id": "0x2e35551b1bf7bb6942610be99dcf60fafe804f167c19a2070c45ff1a0a7f50de"
        },
        "status": "success"
    }

Value of status (inside data)

.. csv-table::
    :header-rows: 1
    :align: center

    Status, Description
    no_transaction, User has not yet completed the ARCANA generation process. (Including cases where the user exited)
    transaction_created, ARCANA generation transaction has been sent to the blockchain but the result is not confirmed yet.
    error, Transaction failed for some reason and terminated (ARCANA has not been generated).
    done, ARCANA has been generated and the process completed successfully.


Error response

.. code-block:: json

    {
        "message": "request_idが見つかりません"
    }

Note::

    In case of error, a 404 status will be returned.


------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------
Flow to ARCANA Generation
------------------------------------
The process for ARCANA generation follows a flow similar to the following:

1. Validator Setup.
2. Granting SHARD, ANIMA
3. Registering Matrix, Activating Matrix
4. Generating EGG in Validator Management Interface.
5. Obtaining the private key of the Validator from a dedicated site.
6. Creating a signature using the obtained private key.
7. Generating ARCANA using the EGG and signature created above.

In the staging environment, you can perform the following steps:

1. Register with an email address in the Validator Management Interface. A wallet will be created.
2. The privatekey is obtained by using the privatekey of the walletaddress issued above. privatekey can be checked from the console of the development tools in the browser by logging in to the Validator UI as the target user. Use the private key displayed with "0x" added at the beginning for creating the signature.
3. EGGs in the staging environment are issued by administrative authority, not by generating them from the Validator UI.
4. Set the issued EGG's ID in the eggid parameter. You can check the EGGs you own in the Validator Management Interface.

