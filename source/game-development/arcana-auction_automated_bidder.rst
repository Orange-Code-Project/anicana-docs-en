###########################
Automated Bidder Service
###########################

====================================
Automated Bidder Service
====================================

| An automated bidding service running on ECS. It monitors Arcana token auctions and automatically places bids based on predefined conditions.
| The necessary information is provided below.

Contract Information
============================

Retrieve Auction Information (ExtractorAuction.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

     @param tokenId ERC721 token ID.
     @return auction Auction information.
     @return maxBid Highest bid amount
    function auctionInfo(uint256 tokenId) public view override returns (Auction memory auction, Bid memory maxBid){auction = auctions[tokenId];maxBid = bids[maxDepositByKey(tokenId)];}


Auction
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

            struct Auction {
                uint256 tokenId;
                uint256 budget;
                uint256 tentativeBid;
                address budgetProvider;
                /// @notice Auction status. ACTIVE = 1; WAIT_FOR_FINALIZE = 2; WAIT_FOR_REFUND = 3; DEAD = 4;
                uint8 state;
            }


Returns an array of AuctionWithMaxBid structures containing auction information (ExtractorAuction.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

        @param offset Starting token ID (inclusive)
        @param count Number of items to retrieve (inclusive)
        @return Array of AuctionWithMaxBid structures containing auction information
        function getActiveAuction(uint256 offset, uint256 count) public view returns (AuctionWithMaxBid[] memory)


Place a Bid in an Auction (ExtractorAuction.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

        @param tokenId Target token ID
        @param bidAmount Bid amount
        @param requestShard Whether to receive the reward as a Shard
        @return bidId Bid ID
        function placeBid(uint256 tokenId,uint256 bidAmount,bool requestShard) public override authorized("WHITE_BIDDER") notBlocked("BLACK_BIDDER") returns (uint256)


Cancel a Bid (ExtractorAuction.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

        @param bidId Bid ID
        function cancelBid(uint256 bidId) external


Retrieve Budget for the Target Token (ExtractorBudget.sol)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

        @param tokenId Target token ID
        @return Budget
        function getBudget(uint256 tokenId) public view returns (Budget memory)

Budget
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

        struct Budget {
                /// @notice Indicates whether the budget has been paid.
                address paid;
                /// @notice Indicates whether the associated ERC721 token has been burned.
                bool tokenBurned;
                /// @notice Address of the budget provider
                address budgetProvider;
                /// @notice ERC721 token ID associated with the budget
                uint256 tokenId;
                /// @notice Amount of Anima allocated to the budget
                uint256 animaAmount;
                /// @notice Amount of Levica allocated to the budget
                uint256 levicaAmount;
                /// @notice Timestamp of payment
                uint256 paidTimestamp;
                /// @notice Address to which the shard is transferred
                address tokenReceiverAddress;
                /// @notice Publisher address
                address publisherAddress;
            }
