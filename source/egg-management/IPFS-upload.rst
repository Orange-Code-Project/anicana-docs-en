###########################
Uploading to IPFS
###########################

| * Upload the entire set of image data to IPFS for EGG conversion.
|   ⇒ A content hash will be returned.
| * Upload the metadata JSON containing the content hash of the image data to IPFS.
|   ⇒ A content hash will be returned.
| The content hash of the metadata JSON is used for `Matrix construction <../egg-management/matrix-development.html>`_ and `Generating and Distributing PERSONA <../game-development/persona-introduction.html>`_ .

--------------------

.. admonition:: Restrictions on images that can be uploaded

  - The API to retrieve images from the PFS has the following restrictions. If the following restrictions are not met, images cannot be retrieved and therefore cannot be displayed on the portal site.
  - The file format is bmp, jpeg, png, or gif.
  - 20 MiB or less

Environment Information
==========================

Refer to each environment information page.
