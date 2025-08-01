=======
echoscp
=======

.. code-block:: text

    $ python -m pynetdicom echoscp [options] port

Description
===========
The ``echoscp`` application implements a Service Class Provider (SCP) for the
:dcm:`Verification<part04/chapter_A.html>` service class. It listens for
incoming association requests on the specified *port*, and once an association
is established, responds to incoming C-ECHO requests. The application can be
used to verify basic DICOM connectivity.

The source code for the application can be found :gh:`here
<pynetdicom/tree/main/pynetdicom/apps/echoscp>`

Usage
=====

The following example shows what happens when it's started and receives
a C-ECHO request from a peer:

.. code-block:: text

   $ python -m pynetdicom echoscp 11112


More information is available when running with the ``-v`` option:

.. code-block:: text

    $ python -m pynetdicom echoscp 11112 -v
    I: Accepting Association
    I: Received Echo Request (MsgID 1)
    I: Association Released

When a peer AE attempts to send non C-ECHO message:

.. code-block:: text

    $ python -m pynetdicom echoscp 11112 -v
    I: Accepting Association
    I: Association Aborted

Much more information is available when running with the ``-d`` option:

.. code-block:: text

    $ python -m pynetdicom echoscp 11112 -d
    D: echoscp.py v0.7.0
    D:
    D: Request Parameters:
    D: ======================= INCOMING A-ASSOCIATE-RQ PDU ========================
    D: Their Implementation Class UID:      1.2.276.0.7230010.3.0.3.6.2
    ...
    I: Received Echo Request (MsgID 1)
    D: ========================== INCOMING DIMSE MESSAGE ==========================
    D: Message Type                  : C-ECHO RQ
    D: Presentation Context ID       : 1
    D: Message ID                    : 1
    D: Data Set                      : None
    D: ============================ END DIMSE MESSAGE =============================
    I: Association Released


Options
=======
General Options
---------------
``-q    --quiet``
            quiet mode, prints no warnings or errors
``-v    --verbose``
            verbose mode, prints processing details
``-d    --debug``
            debug mode, prints debugging information
``-ll   --log-level [l]evel (str)``
            One of [``'critical'``, ``'error'``, ``'warning'``, ``'info'``,
            ``'debug'``], prints logging messages with corresponding level
            or lower

Network Options
---------------
``-aet  --ae-title [a]etitle (str)``
            set the local AE title (default: ``ECHOSCP``)
``-ta   --acse-timeout [s]econds (float)``
            timeout for ACSE messages (default: ``30``)
``-td   --dimse-timeout [s]econds (float)``
            timeout for DIMSE messages (default: ``30``)
``-tn   --network-timeout [s]econds (float)``
            timeout for the network (default: ``30``)
``-pdu  --max-pdu [n]umber of bytes (int)``
            set maximum receive PDU bytes to n bytes (default: ``16382``)

Preferred Transfer Syntaxes
---------------------------
``-x=   --prefer-uncompr``
            prefer explicit VR local byte order
``-xe   --prefer-little``
            prefer explicit VR little endian transfer syntax
``-xb   --prefer-big``
            prefer explicit VR big endian transfer syntax
``-xi   --implicit``
            accept implicit VR little endian transfer syntax only

DICOM Conformance
=================
The ``echoscp`` application supports the Verification service as an SCP. The
following SOP classes are supported:

Verification Service
--------------------

SOP Classes
...........

+------------------+------------------------+
| UID              | SOP Class              |
+==================+========================+
|1.2.840.10008.1.1 | Verification SOP Class |
+------------------+------------------------+

Transfer Syntaxes
.................

+---------------------------+-----------------------------------------------------------+
| UID                       | Transfer Syntax                                           |
+===========================+===========================================================+
| 1.2.840.10008.1.2         | Implicit VR Little Endian                                 |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.1       | Explicit VR Little Endian                                 |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.1.99    | Deflated Explicit VR Little Endian                        |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.2       | Explicit VR Big Endian                                    |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.50    | JPEG Baseline (Process 1)                                 |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.51    | JPEG Extended (Process 2 and 4)                           |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.57    | JPEG Lossless, Non-Hierarchical (Process 14)              |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.70    | JPEG Lossless, Non-Hierarchical, First-Order              |
|                           | Prediction (Process 14 [Selection Value 1])               |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.80    | JPEG-LS Lossless Image Compression                        |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.81    | JPEG-LS Lossy (Near-Lossless) Image Compression           |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.90    | JPEG 2000 Image Compression (Lossless Only)               |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.91    | JPEG 2000 Image Compression                               |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.92    | JPEG 2000 Part 2 Multi-component Image Compression        |
|                           | (Lossless Only)                                           |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.93    | JPEG 2000 Part 2 Multi-component Image Compression        |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.94    | JPIP Referenced                                           |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.95    | JPIP Referenced Deflate                                   |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.100   | MPEG2 Main Profile / Main Level                           |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.100.1 | Fragmentable MPEG2 Main Profile / Main Level              |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.101   | MPEG2 Main Profile / High Level                           |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.101.1 | Fragmentable MPEG2 Main Profile / High Level              |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.102   | MPEG-4 AVC/H.264 High Profile / Level 4.1                 |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.102.1 | Fragmentable MPEG-4 AVC/H.264 High Profile / Level 4.1    |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.103   | MPEG-4 AVC/H.264 BD-compatible High Profile               |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.103.1 | Fragmentable MPEG-4 AVC/H.264 BD-compatible High Profile  |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.104   | MPEG-4 AVC/H.264 High Profile For 2D Video                |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.104.1 | Fragmentable MPEG-4 AVC/H.264 High Profile For 2D Video   |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.105   | MPEG-4 AVC/H.264 High Profile For 3D Video                |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.105.1 | Fragmentable MPEG-4 AVC/H.264 High Profile For 3D Video   |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.106   | MPEG-4 AVC/H.264 Stereo High Profile                      |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.106.1 | Fragmentable MPEG-4 AVC/H.264 Stereo High Profile         |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.107   | HEVC/H.265 Main Profile / Level 5.1                       |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.108   | HEVC/H.265 Main 10 Profile / Level 5.1                    |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.110   | JPEG XL Lossless                                          |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.111   | JPEG XL JPEG Recompression                                |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.112   | JPEG XL                                                   |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.201   | High-Throughput JPEG 2000 Lossless                        |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.202   | High-Throughput JPEG 2000 RPCL                            |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.203   | High-Throughput JPEG 2000                                 |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.204   | JPIP HT2K Referenced                                      |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.4.205   | JPIP HTJ2k Referenced Deflate                             |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.5       | RLE Lossless                                              |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.7.1     | SMPTE ST 2110-20 Uncompressed Progressive Active Video    |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.7.2     | SMPTE ST 2110-20 Uncompressed Interlaced Active Video     |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.7.3     | SMPTE ST 2110-30 PCM Digital Audio                        |
+---------------------------+-----------------------------------------------------------+
| 1.2.840.10008.1.2.8.1     | Deflated Image Frame Compression                          |
+---------------------------+-----------------------------------------------------------+
