###########################
Gene Calculation
###########################


Gene Overview
=====================================

ARCANA, EGG, and SHARD each have unique "gene information" for every token. Gene information changes and is inherited as tokens transform from SHARD to EGG to ARCANA and back to SHARD.

.. csv-table::
    :header-rows: 1
    :align: center

    "Process", "Gene Changes"
    "SHARD → EGG", "The gene information synthesized from two different SHARDs becomes the gene of the EGG"
    "EGG → ARCANA", "The gene information possessed by the EGG is directly inherited as the gene of the ARCANA"
    "ARCANA → SHARD", "The gene information carried by the ARCANA is directly inherited as the gene of the SHARD"

-----------------------------------------------------------------------------------


Data Structure of Gene Information
=====================================

Gene information is represented as a 32-dimensional vector, with each vector having a value range of 8 bits (-128 to +127).
In the contract, it is stored in a single 256-bit field::

      |-------------------------256bit[hex]--------------------------|
    0xffeeddccbbaa99887766554433221100ffeeddccbbaa99887766554433221100
      ^^                                                            ^^
      Dimension 1                                                   Dimension 32



-----------------------------------------------------------------------------------


Gene Calculation for EGG Generation from SHARD
================================================


Let the gene vectors for two SHARDs X and Y, which are the basis for synthesis, be GX and GY.
Let the number of X be a and the number of Y be b.
The gene vector for the newly generated EGG is denoted as GZ.

The gene dimensions for the gene vectors are denoted as GXn, GYn, and GZn (n = 1 to 32).

Genes are calculated using the following formula.::

    GZi = (aGXi + bGYi) / (a+b)
    ※ a + b is always 100


-----------------------------------------------------------------------------------

About Mutation
=====================================

Even for EGG generation between SHARDs of the same type and the same quantity, it is not guaranteed that the EGGs will have the same genes.
There is a certain "mutation" logic in gene calculation.

For each of the 32 dimensions, with a 5% probability for each, the inherited value may be overwritten with a completely different new value.

