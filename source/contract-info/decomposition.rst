###########################
ARCANA Extraction
###########################


During the extraction of an ARCANA,

#. Time until extraction is complete
#. Number of resulting SHARDs

Both of these are randomly determined, and their lottery probabilities are as follows.

-------------------------------------------------------------------------------

Duration of ARCANA Extraction
=====================================

The time required for the extraction of an ARCANA token is determined through a hashing process based on the gene and salt (internal constant).
The extraction time ranges from 5 minutes to 48 hours, with 16 possible values, and an expected value of 8.7 hours. The occurrence probabilities are as follows.

.. csv-table::
    :header-rows: 1
    :align: center

    "Duration", "Probability"
    "5.0 min","6.25%"
    "7.6 min","6.25%"
    "11.7 min","6.25%"
    "17.8 min","6.25%"
    "27.2 min","6.25%"
    "41.6 min","6.25%"
    "1.1 hour","6.25%"
    "1.6 hour","6.25%"
    "2.5 hour","6.25%"
    "3.8 hour","6.25%"
    "5.8 hour","6.25%"
    "8.8 hour","6.25%"
    "13.5 hour","6.25%"
    "20.6 hour","6.25%"
    "31.4 hour","6.25%"
    "48.0 hour","6.25%"


-------------------------------------------------------------------------------

Number of ARCANA SHARDs Obtained in ARCANA Extraction
============================================================

The number of SHARDs obtained when extraction an ARCANA token is determined through a hashing process based on the gene and salt (internal constant).
The number of SHARDs ranges from 50 to 2500, with 16 possible values, and an expected value of 300. The occurrence probabilities are as follows.

.. csv-table::
    :header-rows: 1
    :align: center

    "Number Generated", "Probability"
    "50","13.91%"
    "100","13.67%"
    "150","12.97%"
    "200","11.89%"
    "250","10.53%"
    "300","9.00%"
    "350","7.43%"
    "450","5.92%"
    "550","4.56%"
    "700","3.39%"
    "850","2.44%"
    "1050","1.69%"
    "1300","1.13%"
    "1600","0.73%"
    "2000","0.46%"
    "2500","0.28%"

-------------------------------------------------------------------------------

Steps for ARCANA Extraction
=====================================

The extraction of ARCANA is performed following these steps.

| #. Approve the ARCANA Token for the Decomposer.
| 　⇒ Use function: Arcana.approve(to, tokenId)
| #. Initiate the extraction.
| 　⇒ Use function: Decomposer.beginDecompose(tokenId)
| #. Obtain detailed information about the extraction job and confirm the completion time.
| 　⇒ Use function: Decomposer.getState(jobId)
| #. Wait for the extraction to be completed.
| 　
| #. End the extraction and receive the SHARDs.
| 　⇒ Use function: Decomposer.endDecompose(jobId)

- Reference Video

.. raw:: html

   <video controls width="600" height="300" src="../movie/decomport.mp4"></video>
