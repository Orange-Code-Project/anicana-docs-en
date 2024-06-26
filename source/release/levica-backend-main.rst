###########################################
LEVICA API（Production）
###########################################

release information
=====================================

.. csv-table::
    :header-rows: 1
    :align: center

    "No", "Version", "Release Date", "Release Notes"
    "4.", "1.3.3", "2024/06/27", "
    | Fixed a problem with stripe causing double payment.
    | Heavy areas, added logs for investigation.
    | "
    "3.", "1.3.1", "2024/05/01","| <New Feature>
    | Create an API to reuse all past payments.
    | Re-enable the API, all past payments for that merchant will be treated as reused, and the levica for all payments will be sent to the specified wallet address.
    | Create an API to reuse all past payments made by the merchant."
    "2.", "1.3.0", "2024/05/01", "| <New Feature>
    | LEVICA merchant management screen will be released.
    | User payment history for merchants and payment information from LEVICA to merchants can be viewed.
    | Also, a portion of the user payment is not reimbursed by bank transfer,
    | We will also add the ability to set up the automatic transfer of a portion of a user's payment to another LEVICA account for re-use.
    | For more information, please refer to the :doc:`here </egg-management/LEVICA-MerchantManagement>` page.
    | 
    | <Merchant Management Screen>
    | Settlement history screen:
    | User refund amount and reused amount are displayed.
    | 
    | All billing history screen:
    | Displays the total sales for each month, as well as the maximum amount set for refunds for the following month, and the actual amount deposited. The deposit process is performed from the admin screen.
    | 
    | Reuse setting screen:
    | Enable/Disable re-use, set the maximum amount of refund for the next term, and set the wallet address of the re-use destination.
    | 　"
    "1.", "1.2.10", "", "Latest version as of 2024/03/15"
