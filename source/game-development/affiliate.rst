###########################
Affiliate Functionality
###########################

By using the affiliate functionality, it becomes possible to track the registration and settlements of Levias IDs from the target service through referral codes.

The issuer can perform service registration on the affiliate screen and invite affiliates. Affiliates can then disseminate URLs with referral codes attached, such as through social media, and monitor the registrations and settlements made through the issued URLs on the affiliate screen.

-----------------------------------------------------------------------------------

Implementation Flow - Issuance of Referral Code
==================================================

1. Issuance of Levias ID Account

|   * Registration is required for Levias ID accounts for invitations, proceed to register via the following link:
|   * stagingURL: "https://staging.anicana.org/login/idms?f=true"

2. Registration of Issuer Account

|   * Using the account registered in 1. (hereinafter referred to as the issuer account), log in and register via the issuer registration screen.
|   * ※ Please contact the ANICANA technical support team for the registration URL for the issuer account, as it changes each time.

   .. figure:: ../img/affiliate/1.png
      :scale: 30%

3. Approval of Issuer Account Registration

|   * The ANICANA technical support team approves the registration details.
|   * Upon approval, a confirmation email will be sent to the registered email address. Log in via the URL provided in the email.

4. Product Registration

|   * After approval, log in with the issuer account and proceed with product registration.
|   * ※ In the case of staging, images, URLs, etc., can be arbitrary if unavailable.

   .. |affi-img2| image:: ../img/affiliate/2.png
          :scale: 30%
   .. |affi-img3| image:: ../img/affiliate/3.png
          :scale: 30%
   .. |affi-img4| image:: ../img/affiliate/4.png
          :scale: 30%

   |affi-img2| |affi-img3| |affi-img4|

5. Affiliate Request

|   * Create an affiliate after product registration.
|   * Create a separate Levias ID account for the affiliate (refer to 1.).
|   * Log in with the issuer account, send an invitation to the affiliate account via the affiliate addition screen.
|   * Upon receiving the invitation email, log in and register with the affiliate account.

   .. |affi-img5| image:: ../img/affiliate/5.png
          :scale: 30%
   .. |affi-img6| image:: ../img/affiliate/6.png
          :scale: 30%
   .. |affi-img7| image:: ../img/affiliate/7.png
          :scale: 30%

   |affi-img5| |affi-img6| |affi-img7|

6. Approval of Request

|   * After completing the affiliate registration, log in with the issuer account. Press the request menu and approve the affiliate.

   .. |affi-img8| image:: ../img/affiliate/8.png
          :scale: 30%
   .. |affi-img9| image:: ../img/affiliate/9.png
          :scale: 30%
   .. |affi-img10| image:: ../img/affiliate/10.png
          :scale: 30%
   .. |affi-img11| image:: ../img/affiliate/11.png
          :scale: 30%
   .. |affi-img12| image:: ../img/affiliate/12.png
          :scale: 30%

   |affi-img8| |affi-img9| |affi-img10| |affi-img11| |affi-img12|

7. Issuance of Referral Code

|   * Log in with the affiliate account, select the registered product, and copy the link.
|   * The hash at the end of the URL becomes the referral code.

   .. |affi-img13| image:: ../img/affiliate/13.png
          :scale: 30%
   .. |affi-img14| image:: ../img/affiliate/14.png
          :scale: 30%
   .. |affi-img15| image:: ../img/affiliate/15.png
          :scale: 30%

   |affi-img13| |affi-img14| |affi-img15|

Implementation Flow - Use of Referral Code
==================================================

To associate registration and settlement with Levias ID, it's necessary to include the issued referral code in the registration URL and payment request.

| To count Levias ID registrations, include the referral code in the generated login URL. (Counts are based on registrations, not logins)
| Refer to `Wallet Connection </game-development/wallet-connection.html>`_.

| To associate payment information, attach the referral code to Levica's Transaction Request API.
| Refer to `LEVICA Payments </game-development/levica.html>`_.

.. admonition:: About Aggregation

   Batch aggregation occurs once daily, so numerical data for settlements, registrations, etc., will be reflected from the next day.
