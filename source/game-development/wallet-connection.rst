###########################
Wallet Connection
###########################

API Specification
===========================

------------------------------------
Login Script
------------------------------------

Please refer to the respective environment information pages for environment details.

Sample Generation Script::

    <script src="https://staging.anicana.org/login.js" id="anikana_login_script" data-call-id="9999999" data-sign-text="HELLO"  data-callback="https://staging.anicana.org/test_login.html" data-logout="true" ></script>
    <div style='text-align: center'><button class='' onclick='__open_portal_login()'>Login</button></div>

- Omit unnecessary optional parameters along with the key of the parameter.

.. csv-table::
    :header-rows: 1
    :align: center

    Parameter, required/optional, Type, Description
    id,                 required, String,  anikana_login_script (Do not change)
    src,                required, URL,     {endpoint}/login.js (Refer to the endpoint in the environment information page)
    data-call-id,       required, Number,  "A unique number for each publisher. This is used on the content side to determine where the user is returning from, among other functions. If this information is not specifically needed, 9999999 can be used."
    data-sign-text,     optional, String,  Text to be signed (one-time token)
    data-callback,      required, URL,     "Callback URL. After logging in, callId, sign, and address (user's wallet address) will be added as GET parameters and redirected."
    data-logout,        optional, Boolean, "If true, it forces a re-login. If false, it automatically logs in if there is session information, and forces a re-login if there isn't. If not specified, it is treated as false."
    data-referral-code, optional, String,  Set the referral code passed from the affiliate.Fixed at 64 alphanumeric characters.


| - data-sign-text
|   This can be configured for advanced security implementation.
|   For details, refer to `here <../appendics/data-sign-text.html>`_.