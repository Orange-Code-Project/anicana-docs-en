###########################
Implementation of Tenebrae
###########################

Overview Diagram

   .. figure:: ../img/tenebrae/tenebrae.png

Operator (RECIPE Owner)
====================================================

Skill Contract
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Create a contract implementing the ITenebraeSkill interface (ITenebraeSkill.sol)::

        @notice Activate the skill
        @param tenebraeInfo Target tenebrae
        @return Activation effect
        function activate (TenebraeTokenInfo calldata tenebraeInfo) external returns (ActivationEffect memory);

TenebraeTokenInfo[]::

        struct TenebraeTokenInfo {
                uint256 id;                 // Tenebrae ID
                uint256 attachedTo;         // Attached to ID
                uint16  activationCount;    // Number of skill activations
                uint8   attachedTokenType;  // Attached to token type (TenebraeConst.TOKEN_TYPE_XXXX)
                uint8   attachedSlot;       // Attached slot number
                address skill;              // Skill
                uint256 skillSet;           // Skill set (classification within the skill)
        }

ActivationEffect[]::

        struct ActivationEffect {
                int16[6] abilityValues; // Changes in attached entity's ability values
                int16[6] abilityRatios; // Changes in attached entity's ability ratios
                bool[6]  resetAbility;  // true: reset ability changes
                bool     dismissal;     // true: detach Tenebrae after execution. false: don't detach from slot
                string   skillMetadata; // Metadata to be set as activation result
        }

TenebraeConst::

        contract TenebraeConst {
            uint8 public constant TOKEN_TYPE_NONE = 0;
            uint8 public constant TOKEN_TYPE_SHARD = 1;
            uint8 public constant TOKEN_TYPE_ARCANA = 2;
            uint8 public constant TOKEN_TYPE_PERSONA = 3;
            uint8 public constant TOKEN_TYPE_EGG = 4;

            uint8 public constant EVENT_MINT = 0;
            uint8 public constant EVENT_ATTACH = 1;
            uint8 public constant EVENT_ACTIVATE = 2;
            uint8 public constant EVENT_VANISH = 3;
        }

Registration of Skill Contract
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Register a contract implementing the ITenebraeSkill interface (RecipeController.sol)::

     @notice Register TenebraeSkill
     @param assesor // Contract address implemented
     @param description // Description
     @return skillId
     function registerSkill(address skill,string calldata description) public override onlyRegisterer returns (uint256)

Reference of Skill Contract
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Reference a contract implementing the ITenebraeSkill interface (RecipeController.sol)::

     @param skillId
     @return RegisteredInfo
     function getSkill(uint256 skillId) public override view returns (RegisteredInfo memory)

For multiple:

     @param offset
     @param limit
     @return RegisteredInfo
     function getSkills(uint256 offset,uint256 limit) public override view returns (RegisteredInfo[] memory)

Get the number of registered skills:

     function getLastSkillId() public override view returns (uint256)

Tenebrae Mint Assessor Contract
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Create a contract implementing the ITenebraeMintAssesor interface (ITenebraeMintAssesor.sol)::

        @notice Determine whether the mint conditions of Tenebrae are met.
        @param tokenType Type of token TenebraeConst.TOKEN_TYPE_XXXX
        @param ids Array of token IDs to consume
        @param amounts Quantities of tokens to consume
        @return true: mintable under specified conditions, false: not mintable under specified conditions
        function asses(uint8 tokenType,uint256[] calldata ids,uint256[] calldata amounts) external view returns (bool);

Registration of Tenebrae Mint Assessor Contract
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Register a contract implementing the ITenebraeMintAssesor interface (RecipeController.sol)::

        @notice Register TenebraeMintAssesor
        @param assesor // Contract address implemented
        @param description // Description
        @return assesorId
        function registerAssesor(address assesor,string calldata description) public override onlyRegisterer returns (uint256)

Reference of Tenebrae Mint Assessor Contract
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Reference a contract implementing the ITenebraeMintAssesor interface (RecipeController.sol)::

     @param assesorId
     @return RegisteredInfo
     function getAssesor(uint256 assesorId) public override view returns (RegisteredInfo memory)

For multiple:

     @param offset
     @param limit
     @return RegisteredInfo
     function getAssesors(uint256 offset,uint256 limit) public override view returns (RegisteredInfo[] memory)

Get the number of registered assessors:

     function getLastAssesorId() public override view returns (uint256)

Recipe Minting
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Mint a Recipe (Recipe.sol)::

        @notice mint
        @param to Address of the recipient
        @param skillId Skill ID to grant
        @param assesorId Assessor ID of minting conditions
        @return ID of the minted Tenebrae token
        function mint(address to,uint256 skillId,uint256 skillSet,uint256 assesorId) public onlyMinter returns (uint256)

TokenInfo::

        struct TokenInfo {
                uint256 id;        // RECIPE ID
                address assesor;   // Assessor contract for Tenebrae MINT conditions
                address skill;     // Skill
                uint256 skillSet;  // Classification within the skill
        }

Fetching Ability Values of ARCANA Token/PERSONA Token
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Get the incremental changes in ability values (TenebraeHost.sol)::

        @param hostType Type of TenebraeConst.TOKEN_TYPE_XXXX
        @param hostId Host ID
        @return HostInfo
        function hostInformation(uint8 hostType,uint256 hostId) public view returns (HostInfo memory)

HostInfo::

        /// @notice Holds the changes in ability values
        struct HostInfo {
                /// @notice ARCANA/PERSONA
                uint8 hostType;
                /// @notice tokenId of ARCANA/PERSONA
                uint256 hostId;
                /// @notice slot for attaching TENEBRAE
                uint256[] slot;
                /// @notice metadata of the result of activation of TENEBRAE
                string[] activatedMetadata;
                /// @notice increments of attribute values
                int32[6] incrementValues;
                /// @notice multiplier of attribute values (1/100000)
                int32[6] incrementRatios;
        }

Get the ability values of Arcana (original + adjusted values) (TenebraeHost.sol)::

        @notice Get the ability values of Arcana (original + adjusted values).
        @param tokenId Token ID of Arcana
        @return original Arcana's original ability values
        @return currentAbilities Adjusted ability values
        function getArcanaParameters(uint256 tokenId) external view returns (IArcana.Parameters memory original,uint16[] memory currentAbilities)

Get the ability values of Persona (original + adjusted values) (TenebraeHost.sol)::

        @notice Get the ability values of Persona (original + adjusted values).
        @param tokenId Token ID of Persona
        @return original Persona's original ability values
        @return currentAbilities Adjusted ability values
        function getPersonaParameters(uint256 tokenId) external view returns (uint16[] memory original,uint16[] memory currentAbilities)

Fetching the List of Equipped TENEBRAE
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Get the list of equipped TENEBRAE (TenebraeHost.sol)::

        @notice Get the list of TENEBRAE attached to ARCANA/PERSONA
        @param hostType Type of target ARCANA/PERSONA TenebraeConst.TOKEN_TYPE_XXXX
        @param hostId ID of target ARCANA/PERSONA
        @return Attachment status of attachment slots (0 indicates not attached)
        function getAttached(uint8 hostType,uint256 hostId) public view validType(hostType) returns (uint256[] memory) 

Fetching History
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Get history (TenebraeHost.sol)::

        @param tenebraeId Tenebrae ID
        @return history
        @dev Get history
        function getHistory(uint256 tenebraeId) public override view returns(History[] memory) 

TokenInfo::

        struct History {
                uint8   eventType;      // TenebraeConst.EVENT_XXX
                uint64  timestamp;
                address triggeredBy;    // Executor address msg.sender
        }

Granting and Revoking Access to Ability Value Modification Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Grant access (TenebraeGameIF .sol)::

        function grantAccess(address _addr) public onlyAuthority

Revoke access (TenebraeGameIF .sol)::

        function revokeAccess(address _addr) public onlyAuthority

Manufacturer
============================================

Production of TENEBRAE Tokens
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Mint TENEBRAE (Recipe.sol)::

        @param recipeId
        @param mintTo
        @param shardIds // IDs of consumed shards
        @param amounts  // Quantities of consumed shards
        function produceByShard(uint256 recipeId,address mintTo,uint256[] calldata shardIds,uint256[] calldata amounts) public onlyOwner validToken(recipeId) returns (uint256)

Consumer (TENEBRAE Token Owner)
============================================

Equipping TENEBRAE Tokens
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Attach TENEBRAE to ARCANA/PERSONA (TenebraeHost.sol)::

        @notice Attach TENEBRAE to ARCANA/PERSONA
        @param hostType Type of target ARCANA/PERSONA TenebraeConst.TOKEN_TYPE_XXXX
        @param hostId ID of target ARCANA/PERSONA
        @param tenebraeId Target attachment
        @return Index of the attached slot (0-based)
        @dev Revert with revert message E10 if there are no available slots
        function attach(uint8 hostType,uint256 hostId,uint256 tenebraeId) public override returns (uint256)

Activation of Skill
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Activate Skill (TenebraeToken.sol)::

        @notice active
        @param tenebraeId Target TENEBRAE
        function activate(uint256 tenebraeId) 

Publisher
=====================================

Fetching Metadata Set by Activating TENEBRAE
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Get the list of activation data of SKILL (TenebraeHost.sol)::

        @notice Get the list of activation data of SKILL.
        @param hostType Type of target ARCANA/PERSONA TenebraeConst.TOKEN_TYPE_XXXX
        @param hostId ID of target ARCANA/PERSONA
        @return List of skill activation data
        function getActivatedSkills(uint8 hostType,uint256 hostId) external view validType(hostType) returns (ActivatedSkillInfo[] memory) 

Specify slot (TenebraeHost.sol)::

        @notice Get the activation data of SKILL
        @param hostType Type of target ARCANA/PERSONA TenebraeConst.TOKEN_TYPE_XXXX
        @param hostId ID of target ARCANA/PERSONA
        @param slotIdx Index of target attached slot
        @return Skill activation data
        function getActivatedSkill(uint8 hostType,uint256 hostId,uint8 slotIdx) external view validType(hostType) returns (ActivatedSkillInfo memory)

ActivatedSkillInfo::

        /// @notice Metadata information of the activated skill
        struct ActivatedSkillInfo {
                /// @notice Slot index of attachment
                uint8 slotIdx;
                /// @notice Metadata of the activated SKILL
                string metadata;
        }

Consuming Metadata Set by Activating TENEBRAE
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Consume activation data of SKILL (TenebraeHost.sol)::

        @notice Consume activation data of SKILL (delete - clear).
        @param hostType Type of target ARCANA/PERSONA
        @param hostId ID of target ARCANA/PERSONA
        @param slotIdx Index of target attached slot
        function consumeActivatedData(uint8 hostType,uint256 hostId,uint8 slotIdx) public validType(hostType)

Fetching Ability Value Changes as Game Results
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Reference Operator (RECIPE Owner)

Updating Incremental Values and Ratios of ARCANA/PERSONA Ability Values (Authorization Required)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Consume activation data of SKILL (TenebraeHost.sol)::

        @param hostType Type of target ARCANA/PERSONA
        @param hostId ID of target ARCANA/PERSONA
        @param values Values to set in HostInfo's incrementValues
        @param ratios Values to set in HostInfo's incrementRatios
        function updateAbilities(uint8 hostType,uint256 hostId,int16[6] calldata values,int16[6] calldata ratios) public onlyGranted

