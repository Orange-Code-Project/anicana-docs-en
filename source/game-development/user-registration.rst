###########################
User Wallet Retrieval
###########################

While it is not necessary for content-side systems to directly interact with the blockchain, there may be a need to obtain user wallet information.

Therefore, we provide a method for associating user information held on the content side with wallet address information by performing owner authentication of the address through ANICANA wallet integration.

---------------------------------

User Registration Flow
==========================

The following user registration flow is expected:

1. Users register an account with the content.
2. During account registration, user’s wallet address will be retrieved when connecting the wallet. 
   If the user does not have a wallet, one will be automatically generated during the initial connection.
3. Link the content account with the user's address and maintain the information on the content side.
4. Authentication of the address holder can be achieved through wallet integration, enabling login to the content through address authentication instead of methods like password authentication. 
   This allows for a Single Sign-On (SSO) that can be shared with other content providers.
