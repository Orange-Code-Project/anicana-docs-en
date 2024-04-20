###########################
Bloodline
###########################

Overview
============================================
Bloodline is the lineage to which ARCANA belongs, and every ARCANA belongs to one of the 100 Bloodlines. 
Each Bloodline has an ancestor, and it is inherited as shown in the diagram below, through the cycle of Egg -> ARCANA -> Shard, originating from the ancestor's Shard. 
Newly generated ARCANA randomly inherit one of the two Bloodlines of the Shards used in the birth Egg.

.. image:: ../img/bloodline/bloodline.png

Information Retrieval
============================================
Bloodline information can be obtained by referencing the Bloodline contract. 
The Bloodline contract has the following interfaces.

Retrieving information about a Bloodline (Bloodline.sol)::

    // Returns the ID, name, and number of ARCANA belonging to the specified bloodline
    // @param bloodlineID
    // @return origin ID of the bloodline
    //         nArcanas number of ARCANA belonging to it
    //         name name of the bloodline
    function bloodlineInfo(uint256 bloodlineID) public view returns(
        uint256 origin,
        uint256 nArcanas,
        string memory name
    )



Retrieving the Bloodline to which an ARCANA belongs(Bloodline.sol)::

    // Returns the bloodlineID to which the ARCANA belongs using getBloodline[arcanaID]
    // @param arcanaID
    // @return bloodlineID
    function getBloodline (uint256 arcanaID) public view returns(uint256 bloodlineID)


Retrieving a list of ARCANA belonging to a specific Bloodline (including already burned ARCANA)(Bloodline.sol)::

    // Returns an array of arcanaID belonging to the specified bloodlineID
    // @param bloodlineID
    // @param idx start index
    // @param limit number of items to retrieve
    // @return uint256[] memory array of arcanaID
    function getBelongings(uint256 bloodlineID,uint256 idx, uint256 limit) public view returns(uint256[] memory)


List of Bloodlines
============================================

.. csv-table::
    :header-rows: 1
    :align: center

    "id", "name", "origin"
    "1","Zeus","Greek Mythology"
    "2","Indra","Hinduism"
    "3","Allah","Islam"
    "4","Odin","Norse Mythology"
    "5","Heracles","Greek Mythology"
    "6","Vishnu","Hinduism"
    "7","Hera","Greek Mythology"
    "8","Ganesha","Hinduism"
    "9","Osiris","Ancient Egyptian Mythology"
    "10","Apollo","Greek Mythology"
    "11","Persephone","Greek Mythology"
    "12","Anubis","Ancient Egyptian Mythology"
    "13","Loki","Norse Mythology"
    "14","Medusa","Greek Mythology"
    "15","Krishna","Hinduism"
    "16","Shiva","Hinduism"
    "17","Athena","Greek Mythology"
    "18","Dionysus","Greek Mythology"
    "19","Varuna","Hinduism"
    "20","Isis","Ancient Egyptian Mythology"
    "21","Nut","Ancient Egyptian Mythology"
    "22","Pele","Hawaiian Mythology"
    "23","Freya","Norse Mythology"
    "24","Balder","Norse Mythology"
    "25","Tezcatlipoca","Aztec Mythology"
    "26","Izanami","Japanese Mythology"
    "27","Ma'at","Ancient Egyptian Mythology"
    "28","Hachiman","Shintoism"
    "29","Pan","Greek Mythology"
    "30","Manu","Hinduism"
    "31","Hephaestus","Greek Mythology"
    "32","Inti","Incan Mythology"
    "33","Vayu","Hinduism"
    "34","Gukumatz","Mayan Mythology"
    "35","Frigg","Norse Mythology"
    "36","Hestia","Greek Mythology"
    "37","Saraswati","Hinduism"
    "38","Olokun","Yoruba Mythology"
    "39","Agni","Hinduism"
    "40","K'an","Mayan Mythology"
    "41","Izanagi","Japanese Mythology"
    "42","Ta'aroa","Polynesian Mythology"
    "43","Anu","Sumerian Mythology"
    "44","Tyche","Greek Mythology"
    "45","Bellona","Roman Mythology"
    "46","Ishtar","Babylonian Mythology"
    "47","Utu","Sumerian Mythology"
    "48","Hecate","Greek Mythology"
    "49","Hades","Greek Mythology"
    "50","Set","Ancient Egyptian Mythology"
    "51","Mithra","Persian Mythology"
    "52","Amaterasu","Japanese Mythology"
    "53","Thor","Norse Mythology"
    "54","Enki","Sumerian Mythology"
    "55","Morrigan","Celtic Mythology"
    "56","Pachamama","Incan Mythology"
    "57","Baron Samedi","Voodoo"
    "58","Artemis","Greek Mythology"
    "59","Bennu","Ancient Egyptian Mythology"
    "60","Aphrodite","Greek Mythology"
    "61","Ra","Ancient Egyptian Mythology"
    "62","Brigid","Celtic Mythology"
    "63","Tiamat","Babylonian Mythology"
    "64","Rama","Hinduism"
    "65","Susanoo","Japanese Mythology"
    "66","Cronus","Greek Mythology"
    "67","Dagda","Celtic Mythology"
    "68","Quetzalcoatl","Aztec Mythology"
    "69","Parvati","Hinduism"
    "70","Bastet","Ancient Egyptian Mythology"
    "71","Demeter","Greek Mythology"
    "72","Fortuna","Roman Mythology"
    "73","Narasimha","Hinduism"
    "74","Yama","Hinduism"
    "75","Sekhmet","Ancient Egyptian Mythology"
    "76","Phobos","Greek Mythology"
    "77","Lakshmi","Hinduism"
    "78","Silvanus","Roman Mythology"
    "79","Brahma","Hinduism"
    "80","Nephthys","Ancient Egyptian Mythology"
    "81","Tyr","Norse Mythology"
    "82","Tsukuyomi","Japanese Mythology"
    "83","Poseidon","Greek Mythology"
    "84","Durga","Hinduism"
    "85","Forseti","Norse Mythology"
    "86","Eros","Greek Mythology"
    "87","Thoth","Ancient Egyptian Mythology"
    "88","Idun","Norse Mythology"
    "89","Kali","Hinduism"
    "90","Hermes","Greek Mythology"
    "91","Viracocha","Incan Mythology"
    "92","Inanna","Sumerian Mythology"
    "93","Enlil","Sumerian Mythology"
    "94","Ahura Mazda","Zoroastrianism"
    "95","Janus","Roman Mythology"
    "96","Nuada","Celtic Mythology"
    "97","Oshun","Yoruba Mythology"
    "98","Chaac","Mayan Mythology"
    "99","Mictlantecuhtli","Aztec Mythology"
    "100","Prometheus","Greek Mythology"
    
