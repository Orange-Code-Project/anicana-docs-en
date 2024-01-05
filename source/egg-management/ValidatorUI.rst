######################################
Validator Management Interface
######################################

Participants who are Validators or have been issued a Square Key by a Validator have access to the Validator Management Interface. 
It is deployed individually for each Validator, so the URL varies for each administrator. 
This interface allows users to apply for node participation, generate EGGs, and perform various operations related to Queens and Knights.

Preparation steps required for content development are as follows:

The Validator Management Interface is mainly used for EGG generation.

.. csv-table::
    :header-rows: 1
    :align: center

    "Step", "Details"
    "Validator Setup", "Refer to :doc:`Validator Setup </validator/procedure>`."
    "Generating Square Key", "Refer to :doc:`Generating Square Key </validator/create-square-key>`."
    "Requesting Matrix Development", "Refer to :doc:`Requesting Matrix Development </egg-management/matrix-development>`."
    "Acquiring ANIMA", "Refer to :doc:`Acquiring ANM(ANIMA) </egg-management/anima>`."
    "Generating EGGs", "Refer to :doc:`Generating EGGs </egg-management/generate-eggs>`."


Obtaining a Private Key
============================================
| You can check the Private Key of the logged-in user.
| Press F12 to display the browser's development tools. Confirm the private key displayed in the console.

   ... figure:: ... /img/ValidatorUI/ValidatorUI-10.png


Additional details for each screen are provided below.

DASHBOARD
============================================

* Queen Tab

You can check the address of the Queen and her term.

#. Queen's Address
#. Queen's Term

   .. figure:: ../img/ValidatorUI/ValidatorUI-1.png

* Knights Tab

You can check the address and number of Knights. Validators need to obtain network participation approval from one of the Knights listed here. 
Approved Validators are linked to the No. of the approving Knight.

#. Knight's Address
#. Knight's Number

   .. figure:: ../img/ValidatorUI/ValidatorUI-2.png

* Pawns

Check the participation status of other Validators. You can see the address, the No. of the approving Knight, and the joining date of the Pawn.

#. Pawn's Address
#. No. of the Knight who approved the Pawn
#. Date of joining the Pawn's node

   .. figure:: ../img/ValidatorUI/ValidatorUI-3.png

-----------------------------------------------------------------------------------------------------------

PROFILE
============================================

Click on the icon of the user on the upper right to access the PROFILE page. 
Here, you can apply to be a Validator, check the status of your application, and confirm your wallet address.

#. Transition icon to PROFILE
#. Check the status of your own application
#. Apply button to Knight. Select the number of the Knight you want to apply to.
#. Your own wallet address

   .. figure:: ../img/ValidatorUI/ValidatorUI-4.png

-----------------------------------------------------------------------------------------------------------

EGG
============================================

For information about EGG generation, refer to `here <../egg-management/generate-eggs.html>`_ .

-----------------------------------------------------------------------------------------------------------

KNIGHT
============================================

You can approve new Validators, hold Queen elections, and vote for Queen removal.

#. Approve a new Validator
#. Queen election
#. Vote for Queen removal

   .. figure:: ../img/ValidatorUI/ValidatorUI-5.png

| - Pawn Requests
| A list of pending approvals is displayed. You can perform approvals or denials from the list. Also, display a list of Validators approved by your Knight number.
| ※The list will be empty if you are not a Knight.

#. Address of the Validator who applied
#. Application date
#. Approve or Deny button

   .. figure:: ../img/ValidatorUI/ValidatorUI-6.png

| - Elect Queen
| This page is used during Queen elections. If elections are in progress, you can select the voting address and cast your vote. 
| Also, display a list of addresses that have voted or been trusted.

| ※You can only view this page if you are a Knight.

#. Select a voting address and cast your vote

   .. figure:: ../img/ValidatorUI/ValidatorUI-7.png

| - Remove Queen
| This page is used to vote for the removal of the Queen. Also, display the current number of votes.
| ※You can only view this page if you are a Knight.

#. Vote for Queen removal

   .. figure:: ../img/ValidatorUI/ValidatorUI-8.png

-----------------------------------------------------------------------------------------------------------

QUEEN
============================================

| This page allows operations for Queens. You can approve and remove Knights, and set the deposit amount. It also displays the current list of Knights.
| ※You can only view this page if you are a Queen.

#. Enter and set the ANIMA quantity
#. Remove a specific Knight. Also, specify the address and Knight number of the new Knight to appoint.

   .. figure:: ../img/ValidatorUI/ValidatorUI-9.png

