###########################
Interface Specifications
###########################

MATRIX Standard
============================================

Contracts that have the following interfaces can be registered as a Matrix in MatrixMaster.::

    // Provide materials of EGG to MatrixMaster.
    function spawnCondition() external returns(IEggBuilder.ComposeCondition memory);

    // Return the amount of ANIMA required for EGG generation. The paid ANIMA will be rewarded to the developer upon generation.
    function getPrice() external view returns (uint256);

    // Matrix users are limited to users with the Square Key of the returned ID here.
    function correspondingSquareKey() external view returns (uint256);

    // Check the owner.
    function getOwner() external view returns (address);

-------------------------------


Other Smart Contract Interfaces
============================================

To be published on GitHub soon.