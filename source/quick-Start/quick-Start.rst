######################################
Quick Start for Publishers
######################################

| This guide introduces the necessary steps to participate as a Validator in the ANICANA network and perform ARCANA generation.
| Items marked with ★ are to be carried out by the publisher, while the ANICANA technical support team handles the rest.

-----------------------------------------------------------------------------------

Initial Setup
=======================================
Steps to Join the ANICANA Network
-----------------------------------------------------------------------------------

#. Perform registration in the ★wallet to obtain a wallet address.
#. Prepare an ★AWS account.
#. Set up the Validator.

   .. figure:: ../img/quickStart/QuickStartGuideSetup.png

Reference Pages

.. csv-table::
    :header-rows: 1
    :align: center

    "Content", "Reference Page"
    "Obtain Validator Blockchain Address in ANICANA Wallet", ":doc:`Register in ANICANA Wallet </validator/wallet-registration>`"
    "Prepare AWS (Amazon Web Services) Account", ":doc:`Prepare AWS Account </validator/aws-preparation>`"
    "Set Up Validator Components on AWS", ":doc:`Validator Setup </validator/validator-setup>`"
    "Apply as a Participating Node in Knights of the Round Table", ":doc:`Apply as Validator Candidate </validator/validator-application>`"
	"About Knights of the Round Table", ":doc:`Knights of the Round Table </mechanism/knights-of-the-round-table>`; :doc:`Roles in Knights of the Round Table </mechanism/rounds-of-logic>`"


Content Development
=======================================
Steps to Build Matrix
-----------------------------------------------------------------------------------

#. Implement and deploy the Matrix.
#. Generate the SquareKey.
#. Obtain ★ANIMA.
#. Set pricing for Egg generation in Matrix, configure SquareKey, and register.
#. Obtain MatrixID through the above steps.

   .. figure:: ../img/quickStart/QuickStartGuideDevContents.png

Reference Pages

.. csv-table::
    :header-rows: 1
    :align: center

    "Content", "Reference Page"
    "Obtain Square Key for EGG Management", ":doc:`Generate Square Key </validator/create-square-key>`"
    "Request Development of Matrix for EGG Generation", ":doc:`Request Matrix Development </egg-management/matrix-development>`"
    "Obtain ANM (ANIMA) for Registering Matrix", ":doc:`Get ANM (ANIMA) </egg-management/anima>`"
    "Explanation of Shard, EGG, ANIMA, and ARCANA", ":doc:`ARCANA life cycle </mechanism/ARCANA-life-cycle>`; :doc:`ANICANA life cycle </mechanism/ANICANA-life-cycle>`"


.. admonition:: Obtaining ANIMA

  ANIMA may be provided by the Technical Support Team.

Operations
======================================
Steps to Generate EGGs
-----------------------------------------------------------------------------------

#. Obtain ★Shard and transfer it to Matrix.
#. Obtain ★ANIMA.
#. Generate Egg via ★Validator management panel.

   .. figure:: ../img/quickStart/QuickStartGuideMintEgg.png

Reference Pages

.. csv-table::
    :header-rows: 1
    :align: center

    "Content", "Reference Page"
    "★Collect Shard", ":doc:`Decompose ARCANA </contract-info/decomposition>`"
    "Obtain ANM (ANIMA) for EGG Generation", ":doc:`Get ANM (ANIMA) </egg-management/anima>`"
    "Perform EGG Generation", ":doc:`Generate EGGs </egg-management/generate-eggs>`"
    "Explanation of Shard, EGG, ANIMA, and ARCANA", ":doc:`ARCANA life cycle </mechanism/ARCANA-life-cycle>`; :doc:`ANICANA life cycle </mechanism/ANICANA-life-cycle>`"


.. admonition:: Obtaining Shard and ANIMA

  Shard and ANIMA may be provided by our technical support team.

Steps to Generate ARCANA
-----------------------------------------------------------------------------------

#. Determine the EGG to be used for ★ARCANA generation.
#. Determine the wallet address of the user to whom ARCANA will be granted.
#. Create ★signature data.
#. Generate ARCANA via the generation API.

   .. figure:: ../img/quickStart/QuickStartGuideArcana.png

Reference Pages

.. csv-table::
    :header-rows: 1
    :align: center

    "Content", "Reference Page"
    "Obtain Information of EGGs for ARCANA Generation", ":doc:`Get Owned EGGs </game-development/egg-balance>`"
    "Link User Information and Wallet Address", ":doc:`Get User Wallet </game-development/user-registration>`; :doc:`Wallet Connection </game-development/wallet-connection>`"
    "Create Signature Data for ARCANA Generation", ":doc:`Generate Signature Steps </game-development/generate-signature>`"
    "Interact with ARCANA Generation API", ":doc:`ARCANA Generation Steps </game-development/call-arcana-generator>`; :doc:`ARCANA Generation API </game-development/generate-arcana>`"
    "Mechanism of ARCANA Generation", ":doc:`ARCANA Generation Mechanism </mechanism/arcana-generate>`"
