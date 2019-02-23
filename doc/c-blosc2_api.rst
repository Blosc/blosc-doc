C-Blosc 2 API
=============

This section contains Blosc public API and the structures needed to use it.

Utility variables
+++++++++++++++++
This are enum values which avoid the nuisance of remembering codes and IDs.

Limit related values
--------------------
.. doxygenenumvalue:: BLOSC_MIN_HEADER_LENGTH
   :project: blosc
.. doxygenenumvalue:: BLOSC_EXTENDED_HEADER_LENGTH
   :project: blosc
.. doxygenenumvalue:: BLOSC_MAX_OVERHEAD
   :project: blosc
.. doxygenenumvalue:: BLOSC_MIN_BUFFERSIZE
   :project: blosc
.. doxygenenumvalue:: BLOSC_MAX_BUFFERSIZE
   :project: blosc
.. doxygenenumvalue:: BLOSC_MAX_TYPESIZE
   :project: blosc
.. doxygenenumvalue:: BLOSC_MAX_FILTERS
   :project: blosc

Codes for filters
-----------------
.. doxygenenumvalue:: BLOSC_NOSHUFFLE
   :project: blosc
.. doxygenenumvalue:: BLOSC_NOFILTER
   :project: blosc
.. doxygenenumvalue:: BLOSC_SHUFFLE
   :project: blosc
.. doxygenenumvalue:: BLOSC_BITSHUFFLE
   :project: blosc
.. doxygenenumvalue:: BLOSC_DELTA
   :project: blosc
.. doxygenenumvalue:: BLOSC_TRUNC_PREC
   :project: blosc
.. doxygenenumvalue:: BLOSC_LAST_FILTER
   :project: blosc

Internal flags (blosc_cbuffer_metainfo)
---------------------------------------
.. doxygenenumvalue:: BLOSC_DOSHUFFLE
   :project: blosc
.. doxygenenumvalue:: BLOSC_MEMCPYED
   :project: blosc
.. doxygenenumvalue:: BLOSC_DOBITSHUFFLE
   :project: blosc
.. doxygenenumvalue:: BLOSC_DODELTA
   :project: blosc

Compression dictionaries
------------------------
.. doxygenenumvalue:: BLOSC2_USEDICT
   :project: blosc
.. doxygenenumvalue:: BLOSC2_MAXDICTSIZE
   :project: blosc

Compressor codes
----------------
.. doxygenenumvalue:: BLOSC_BLOSCLZ
   :project: blosc
.. doxygenenumvalue:: BLOSC_LZ4
   :project: blosc
.. doxygenenumvalue:: BLOSC_LZ4HC
   :project: blosc
.. doxygenenumvalue:: BLOSC_SNAPPY
   :project: blosc
.. doxygenenumvalue:: BLOSC_ZLIB
   :project: blosc
.. doxygenenumvalue:: BLOSC_ZSTD
   :project: blosc
.. doxygenenumvalue:: BLOSC_LIZARD
   :project: blosc

Compressor names
----------------
.. doxygendefine:: BLOSC_BLOSCLZ_COMPNAME
   :project: blosc
.. doxygendefine:: BLOSC_LZ4_COMPNAME
   :project: blosc
.. doxygendefine:: BLOSC_LZ4HC_COMPNAME
   :project: blosc
.. doxygendefine:: BLOSC_SNAPPY_COMPNAME
   :project: blosc
.. doxygendefine:: BLOSC_ZLIB_COMPNAME
   :project: blosc
.. doxygendefine:: BLOSC_ZSTD_COMPNAME
   :project: blosc
.. doxygendefine:: BLOSC_LIZARD_COMPNAME
   :project: blosc

Classic API
+++++++++++
This is the classic API from Blosc 1 with 32-bit limited containers
and single threaded.

Main API
--------
.. doxygenfunction:: blosc_init
   :project: blosc
.. doxygenfunction:: blosc_destroy
   :project: blosc
.. doxygenfunction:: blosc_compress
   :project: blosc

Environment variables
_____________________

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

.. doxygenfunction:: blosc_decompress
   :project: blosc

Environment variables
_____________________

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
   :project: blosc
.. doxygenfunction:: blosc_get_nthreads
   :project: blosc
.. doxygenfunction:: blosc_set_nthreads
   :project: blosc
.. doxygenfunction:: blosc_get_compressor
   :project: blosc
.. doxygenfunction:: blosc_set_compressor
   :project: blosc
.. doxygenfunction:: blosc_set_delta
   :project: blosc
.. doxygenfunction:: blosc_free_resources
   :project: blosc

Compressed buffer information
-----------------------------
.. doxygenfunction:: blosc_cbuffer_sizes
   :project: blosc
.. doxygenfunction:: blosc_cbuffer_metainfo
   :project: blosc
.. doxygenfunction:: blosc_cbuffer_versions
   :project: blosc
.. doxygenfunction:: blosc_cbuffer_complib
   :project: blosc

Utility functions
-----------------
.. doxygenfunction:: blosc_compcode_to_compname
   :project: blosc
.. doxygenfunction:: blosc_compname_to_compcode
   :project: blosc
.. doxygenfunction:: blosc_list_compressors
   :project: blosc
.. doxygenfunction:: blosc_get_version_string
   :project: blosc
.. doxygenfunction:: blosc_get_complib_info
   :project: blosc

Context API
+++++++++++
In Blosc 2 there is a special struct blosc2_context that is created from
compression and decompression parameters. This blosc2_context allows the
compression in multithreaded scenarios without using the global lock.

.. doxygenstruct:: blosc2_cparams
   :project: blosc
   :members:
.. doxygenvariable:: BLOSC_CPARAMS_DEFAULTS
   :project: blosc
.. doxygenstruct:: blosc2_dparams
   :project: blosc
   :members:
.. doxygenvariable:: BLOSC_DPARAMS_DEFAULTS
   :project: blosc
.. doxygenfunction:: blosc2_create_cctx
   :project: blosc
.. doxygenfunction:: blosc2_create_dctx
   :project: blosc
.. doxygenfunction:: blosc2_free_ctx
   :project: blosc
.. doxygenfunction:: blosc2_compress_ctx
   :project: blosc
.. doxygenfunction:: blosc2_decompress_ctx
   :project: blosc
.. doxygenfunction:: blosc2_getitem_ctx
   :project: blosc

Super Chunk API
+++++++++++++++
This API describes the new Blosc 2 container, the Super Chunk, which breaks
the 32 bit limitation of Blosc 1.

**typedef blosc2_schunk**

.. doxygenstruct:: blosc2_schunk
   :project: blosc
   :members:
.. doxygenfunction:: blosc2_new_schunk
   :project: blosc
.. doxygenfunction:: blosc2_free_schunk
   :project: blosc
.. doxygenfunction:: blosc2_schunk_append_buffer
   :project: blosc
.. doxygenfunction:: blosc2_schunk_decompress_chunk
   :project: blosc
.. doxygenfunction:: blosc2_schunk_get_chunk
   :project: blosc
.. doxygenfunction:: blosc2_get_cparams
   :project: blosc
.. doxygenfunction:: blosc2_get_dparams
   :project: blosc

Frame API
+++++++++
The Blosc 2 Frame struct is essentially a Super Chunk contiguous in memory,
providing the possibility of serialization on disk and adding metadata.

**typedef blosc2_frame_metalayer**

.. doxygenstruct:: blosc2_frame_metalayer
   :project: blosc
   :members:
.. doxygenstruct:: blosc2_frame
   :project: blosc
   :members:
.. doxygenvariable:: BLOSC_EMPTY_FRAME
   :project: blosc
.. doxygenfunction:: blosc2_schunk_to_frame
   :project: blosc
.. doxygenfunction:: blosc2_schunk_from_frame
   :project: blosc
.. doxygenfunction:: blosc2_free_frame
   :project: blosc
.. doxygenfunction:: blosc2_frame_to_file
   :project: blosc
.. doxygenfunction:: blosc2_frame_from_file
   :project: blosc
.. doxygenfunction:: blosc2_frame_append_chunk
   :project: blosc
.. doxygenfunction:: blosc2_frame_get_chunk
   :project: blosc
.. doxygenfunction:: blosc2_frame_decompress_chunk
   :project: blosc

Namespaces functions
--------------------
.. doxygenfunction:: blosc2_frame_has_metalayer
   :project: blosc
.. doxygenfunction:: blosc2_frame_add_metalayer
   :project: blosc
.. doxygenfunction:: blosc2_frame_update_metalayer
   :project: blosc
.. doxygenfunction:: blosc2_frame_get_metalayer
   :project: blosc

Low level functions
+++++++++++++++++++
Use them only if you are an expert!

.. doxygenfunction:: blosc_get_blocksize
   :project: blosc
.. doxygenfunction:: blosc_set_blocksize
   :project: blosc
.. doxygenfunction:: blosc_set_schunk
   :project: blosc
