C-Blosc 2 API
=============

This section contains Blosc public API and the structures needed to use it.

Utility variables
+++++++++++++++++
This are enum values which avoid the nuisance of remembering codes and IDs.

Limits for different features
-----------------------------
.. doxygenenumvalue:: BLOSC_MIN_HEADER_LENGTH
   :project: blosc2
.. doxygenenumvalue:: BLOSC_EXTENDED_HEADER_LENGTH
   :project: blosc2
.. doxygenenumvalue:: BLOSC_MAX_OVERHEAD
   :project: blosc2
.. doxygenenumvalue:: BLOSC_MIN_BUFFERSIZE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_MAX_BUFFERSIZE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_MAX_TYPESIZE
   :project: blosc2
.. doxygenenumvalue:: BLOSC2_MAX_FILTERS
   :project: blosc2

Codes for filters
-----------------
.. doxygenenumvalue:: BLOSC_NOSHUFFLE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_NOFILTER
   :project: blosc2
.. doxygenenumvalue:: BLOSC_SHUFFLE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_BITSHUFFLE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_DELTA
   :project: blosc2
.. doxygenenumvalue:: BLOSC_TRUNC_PREC
   :project: blosc2
.. doxygenenumvalue:: BLOSC_LAST_FILTER
   :project: blosc2

Internal flags (blosc_cbuffer_metainfo)
---------------------------------------
.. doxygenenumvalue:: BLOSC_DOSHUFFLE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_MEMCPYED
   :project: blosc2
.. doxygenenumvalue:: BLOSC_DOBITSHUFFLE
   :project: blosc2
.. doxygenenumvalue:: BLOSC_DODELTA
   :project: blosc2

Compression dictionaries
------------------------
.. doxygenenumvalue:: BLOSC2_USEDICT
   :project: blosc2
.. doxygenenumvalue:: BLOSC2_MAXDICTSIZE
   :project: blosc2

Compressor codecs
-----------------
.. doxygenenumvalue:: BLOSC_BLOSCLZ
   :project: blosc2
.. doxygenenumvalue:: BLOSC_LZ4
   :project: blosc2
.. doxygenenumvalue:: BLOSC_LZ4HC
   :project: blosc2
.. doxygenenumvalue:: BLOSC_SNAPPY
   :project: blosc2
.. doxygenenumvalue:: BLOSC_ZLIB
   :project: blosc2
.. doxygenenumvalue:: BLOSC_ZSTD
   :project: blosc2
.. doxygenenumvalue:: BLOSC_LIZARD
   :project: blosc2

Compressor names
----------------
.. doxygendefine:: BLOSC_BLOSCLZ_COMPNAME
   :project: blosc2
.. doxygendefine:: BLOSC_LZ4_COMPNAME
   :project: blosc2
.. doxygendefine:: BLOSC_LZ4HC_COMPNAME
   :project: blosc2
.. doxygendefine:: BLOSC_SNAPPY_COMPNAME
   :project: blosc2
.. doxygendefine:: BLOSC_ZLIB_COMPNAME
   :project: blosc2
.. doxygendefine:: BLOSC_ZSTD_COMPNAME
   :project: blosc2
.. doxygendefine:: BLOSC_LIZARD_COMPNAME
   :project: blosc2

Blosc1 API
++++++++++
This is the classic API from Blosc1 with 32-bit limited containers.

Main API
--------
.. doxygenfunction:: blosc_init
   :project: blosc2
.. doxygenfunction:: blosc_destroy
   :project: blosc2

blosc_compress()
________________
.. doxygenfunction:: blosc_compress
   :project: blosc2

*blosc_compress()* honors different environment variables to control
internal parameters without the need of doing that programatically.
Here are the ones supported:

**BLOSC_CLEVEL=(INTEGER)**: This will overwrite the @p clevel parameter
before the compression process starts.

**BLOSC_SHUFFLE=[NOSHUFFLE | SHUFFLE | BITSHUFFLE]**: This will
overwrite the *doshuffle* parameter before the compression process
starts.

**BLOSC_DELTA=(1|0)**: This will call *blosc_set_delta()^* before the
compression process starts.

**BLOSC_TYPESIZE=(INTEGER)**: This will overwrite the *typesize*
parameter before the compression process starts.

**BLOSC_COMPRESSOR=[BLOSCLZ | LZ4 | LZ4HC | LIZARD | SNAPPY | ZLIB]**:
This will call *blosc_set_compressor(BLOSC_COMPRESSOR)* before the
compression process starts.

**BLOSC_NTHREADS=(INTEGER)**: This will call
*blosc_set_nthreads(BLOSC_NTHREADS)* before the compression process
starts.

**BLOSC_BLOCKSIZE=(INTEGER)**: This will call
*blosc_set_blocksize(BLOSC_BLOCKSIZE)* before the compression process
starts.  *NOTE:* The blocksize is a critical parameter with
important restrictions in the allowed values, so use this with care.

**BLOSC_NOLOCK=(ANY VALUE)**: This will call *blosc2_compress_ctx()* under
the hood, with the *compressor*, *blocksize* and
*numinternalthreads* parameters set to the same as the last calls to
*blosc_set_compressor*, *blosc_set_blocksize* and
*blosc_set_nthreads*. *BLOSC_CLEVEL*, *BLOSC_SHUFFLE*, *BLOSC_DELTA* and
*BLOSC_TYPESIZE* environment vars will also be honored.

blosc_decompress()
__________________

.. doxygenfunction:: blosc_decompress
   :project: blosc2

*blosc_decompress* honors different environment variables to control
internal parameters without the need of doing that programatically.
Here are the ones supported:

**BLOSC_NTHREADS=(INTEGER)**: This will call
*blosc_set_nthreads(BLOSC_NTHREADS)* before the proper decompression
process starts.

**BLOSC_NOLOCK=(ANY VALUE)**: This will call *blosc2_decompress_ctx*
under the hood, with the *numinternalthreads* parameter set to the
same value as the last call to *blosc_set_nthreads*.

.. doxygenfunction:: blosc_getitem
   :project: blosc2
.. doxygenfunction:: blosc_get_nthreads
   :project: blosc2
.. doxygenfunction:: blosc_set_nthreads
   :project: blosc2
.. doxygenfunction:: blosc_get_compressor
   :project: blosc2
.. doxygenfunction:: blosc_set_compressor
   :project: blosc2
.. doxygenfunction:: blosc_set_delta
   :project: blosc2
.. doxygenfunction:: blosc_free_resources
   :project: blosc2

Compressed buffer information
-----------------------------
.. doxygenfunction:: blosc_cbuffer_sizes
   :project: blosc2
.. doxygenfunction:: blosc_cbuffer_metainfo
   :project: blosc2
.. doxygenfunction:: blosc_cbuffer_versions
   :project: blosc2
.. doxygenfunction:: blosc_cbuffer_complib
   :project: blosc2

Utility functions
-----------------
.. doxygenfunction:: blosc_compcode_to_compname
   :project: blosc2
.. doxygenfunction:: blosc_compname_to_compcode
   :project: blosc2
.. doxygenfunction:: blosc_list_compressors
   :project: blosc2
.. doxygenfunction:: blosc_get_version_string
   :project: blosc2
.. doxygenfunction:: blosc_get_complib_info
   :project: blosc2

Context API
+++++++++++
In Blosc 2 there is a special `blosc2_context` struct that is created from
compression and decompression parameters. This allows the compression and
decompression to happen in multithreaded scenarios, without the need for
using the global lock.

.. doxygenstruct:: blosc2_cparams
   :project: blosc2
   :members:
.. doxygenvariable:: BLOSC_CPARAMS_DEFAULTS
   :project: blosc2
.. doxygenstruct:: blosc2_dparams
   :project: blosc2
   :members:
.. doxygenvariable:: BLOSC_DPARAMS_DEFAULTS
   :project: blosc2
.. doxygenfunction:: blosc2_create_cctx
   :project: blosc2
.. doxygenfunction:: blosc2_create_dctx
   :project: blosc2
.. doxygenfunction:: blosc2_free_ctx
   :project: blosc2
.. doxygenfunction:: blosc2_compress_ctx
   :project: blosc2
.. doxygenfunction:: blosc2_decompress_ctx
   :project: blosc2
.. doxygenfunction:: blosc2_getitem_ctx
   :project: blosc2

Super-chunk API
+++++++++++++++
This API describes the new Blosc 2 container, the super-chunk (or `schunk` for
short), that is typically stored sparsely in-memory (see the `frames` section
below for other storage methods, including on-disk ones).

**typedef blosc2_schunk**

.. doxygenstruct:: blosc2_schunk
   :project: blosc2
   :members:
.. doxygenfunction:: blosc2_new_schunk
   :project: blosc2
.. doxygenfunction:: blosc2_free_schunk
   :project: blosc2
.. doxygenfunction:: blosc2_schunk_append_buffer
   :project: blosc2
.. doxygenfunction:: blosc2_schunk_decompress_chunk
   :project: blosc2
.. doxygenfunction:: blosc2_schunk_get_chunk
   :project: blosc2
.. doxygenfunction:: blosc2_schunk_get_cparams
   :project: blosc2
.. doxygenfunction:: blosc2_schunk_get_dparams
   :project: blosc2

Frame API
+++++++++
The Blosc 2 Frame struct is essentially a store for a super-chunk that
can be contiguous in memory, or serialized to disk.

**typedef blosc2_frame_metalayer**

.. doxygenstruct:: blosc2_frame_metalayer
   :project: blosc2
   :members:
.. doxygenstruct:: blosc2_frame
   :project: blosc2
   :members:
.. doxygenfunction:: blosc2_schunk_to_frame
   :project: blosc2
.. doxygenfunction:: blosc2_schunk_from_frame
   :project: blosc2
.. doxygenfunction:: blosc2_free_frame
   :project: blosc2
.. doxygenfunction:: blosc2_frame_to_file
   :project: blosc2
.. doxygenfunction:: blosc2_frame_from_file
   :project: blosc2

Metalayer functions
-------------------
Metalayers are meta-information that can be attached to frames.  They can
also be serialized to disk.

.. doxygenfunction:: blosc2_frame_has_metalayer
   :project: blosc2
.. doxygenfunction:: blosc2_frame_add_metalayer
   :project: blosc2
.. doxygenfunction:: blosc2_frame_update_metalayer
   :project: blosc2
.. doxygenfunction:: blosc2_frame_get_metalayer
   :project: blosc2

Timing functions
++++++++++++++++
Time measurement utilities.

.. doxygenfunction:: blosc_set_timestamp
   :project: blosc2
.. doxygenfunction:: blosc_elapsed_nsecs
   :project: blosc2
.. doxygenfunction:: blosc_elapsed_secs
   :project: blosc2

Low level functions
+++++++++++++++++++
Use them only if you are an expert!

.. doxygenfunction:: blosc_get_blocksize
   :project: blosc2
.. doxygenfunction:: blosc_set_blocksize
   :project: blosc2
.. doxygenfunction:: blosc_set_schunk
   :project: blosc2
