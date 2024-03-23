#####################################################
LEVICA Merchant Management Screen
#####################################################

A screen where users can view payment histories for affiliate stores and payment information from LEVICA to affiliate stores.

Payment History Screen
============================================
User refund amounts and reuse amounts are displayed.

   .. figure:: ../img/levica/SettlementHistoryScreen.png

-----------------------------------------------------------------------------------------------------------

All Billing History Screen
============================================
Total monthly sales, the refund setting upper limit amount for the following month, and the actual deposit amount are displayed. Deposit processing is done from the admin screen.

   .. figure:: ../img/levica/AllBillingHistoryScreen.png

-----------------------------------------------------------------------------------------------------------

Reuse Settings Screen
============================================
ON/OFF for reuse, setting the refund upper limit amount for the next period, and setting the reuse destination wallet address.

About Reuse Functionality
============================================
| A feature that automatically reallocates part of the settlement to the designated levias chain address for reuse instead of refunding it via bank transfer to affiliate stores when settlements are made.
| Reuse can be set by specifying the reuse amount on the management screen (Reuse Settings Screen: Figure 2) and pressing confirm after setting the destination levias chain address (Reuse Settings Screen: Figure 3).

| Reuse Flow:

   .. figure:: ../img/levica/ReuseFlow.png

| Reuse Settings Screen:

   .. figure:: ../img/levica/ReuseSettingScreen.png

| However, the setting timing will be for the refund upper limit amount within the range from the 11th to the next month's 10th.
| Once it reaches the 11th, the setting is confirmed and cannot be changed.

| Example:

   .. figure:: ../img/levica/ReuseSettingExsample.png

| If reuse is ON, the above action will be taken. If it is OFF, everything will continue to be refunded as usual. (Reuse Settings Screen: Figure 1)

| The transfer date is the end of the month. (Example: The transfer date for the refund claim period from 2/11 to 3/10 is 3/31)
| If reuse is ON, it will be sent immediately to the designated levias chain address.
| The app will display "Reuse" in the status.

