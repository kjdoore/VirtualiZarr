Release notes
=============

.. _v1.2.1:

v1.2.1 (unreleased)
-------------------

New Features
~~~~~~~~~~~~

Breaking changes
~~~~~~~~~~~~~~~~

Deprecations
~~~~~~~~~~~~

Bug fixes
~~~~~~~~~

Documentation
~~~~~~~~~~~~~

Internal Changes
~~~~~~~~~~~~~~~~

.. _v1.2.0:

v1.2.0 (5th Dec 2024)
---------------------

This release brings a stricter internal model for manifest paths,
support for appending to existing icechunk stores,
an experimental non-kerchunk-based HDF5 reader,
handling of nested groups in DMR++ files,
as well as many other bugfixes and documentation improvements.

New Features
~~~~~~~~~~~~

- Add a ``virtual_backend_kwargs`` keyword argument to file readers and to ``open_virtual_dataset``, to allow reader-specific options to be passed down.
  (:pull:`315`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Added append functionality to `to_icechunk` (:pull:`272`) By `Aimee Barciauskas <https://github.com/abarciauskas-bgse>`_.

Breaking changes
~~~~~~~~~~~~~~~~

- Minimum required version of Xarray is now v2024.10.0.
  (:pull:`284`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Opening kerchunk-formatted references from disk which contain relative paths now requires passing the ``fs_root`` keyword argument via ``virtual_backend_kwargs``.
  (:pull:`243`) By `Tom Nicholas <https://github.com/TomNicholas>`_.

Deprecations
~~~~~~~~~~~~

Bug fixes
~~~~~~~~~

- Handle root and nested groups with ``dmrpp`` backend (:pull:`265`)
  By `Ayush Nag <https://github.com/ayushnag>`_.
- Fixed bug with writing of `dimension_names` into zarr metadata.
  (:pull:`286`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Fixed bug causing CF-compliant variables not to be identified as coordinates (:pull:`191`)
  By `Ayush Nag <https://github.com/ayushnag>`_.

Documentation
~~~~~~~~~~~~~

- FAQ answers on Icechunk compatibility, converting from existing Kerchunk references to Icechunk, and how to add a new reader for a custom file format.
  (:pull:`266`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Clarify which readers actually currently work in FAQ, and temporarily remove tiff from the auto-detection.
  (:issue:`291`, :pull:`296`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Minor improvements to the Contributing Guide.
  (:pull:`298`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- More minor improvements to the Contributing Guide.
  (:pull:`304`) By `Doug Latornell <https://github.com/DougLatornell>`_.
- Correct some links to the API.
  (:pull:`325`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Added links to recorded presentations on VirtualiZarr.
  (:pull:`313`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Added links to existing example notebooks.
  (:issue:`329`, :pull:`331`) By `Tom Nicholas <https://github.com/TomNicholas>`_.

Internal Changes
~~~~~~~~~~~~~~~~

- Added experimental new HDF file reader which doesn't use kerchunk, accessible by importing ``virtualizarr.readers.hdf.HDFVirtualBackend``.
  (:pull:`87`) By `Sean Harkins <https://github.com/sharkinsspatial>`_.
- Support downstream type checking by adding py.typed marker file.
  (:pull:`306`) By `Max Jones <https://github.com/maxrjones>`_.
- File paths in chunk manifests are now always stored as abolute URIs.
  (:pull:`243`) By `Tom Nicholas <https://github.com/TomNicholas>`_.

.. _v1.1.0:

v1.1.0 (22nd Oct 2024)
----------------------

New Features
~~~~~~~~~~~~

- Can open `kerchunk` reference files with ``open_virtual_dataset``.
  (:pull:`251`, :pull:`186`) By `Raphael Hagen <https://github.com/norlandrhagen>`_ & `Kristen Thyng <https://github.com/kthyng>`_.
- Adds defaults for `open_virtual_dataset_from_v3_store` in (:pull:`234`)
  By `Raphael Hagen <https://github.com/norlandrhagen>`_.
- New ``group`` option on ``open_virtual_dataset`` enables extracting specific HDF Groups.
  (:pull:`165`) By `Scott Henderson <https://github.com/scottyhq>`_.
- Adds `decode_times` to open_virtual_dataset (:pull:`232`)
  By `Raphael Hagen <https://github.com/norlandrhagen>`_.
- Add parser for the OPeNDAP DMR++ XML format and integration with open_virtual_dataset (:pull:`113`)
  By `Ayush Nag <https://github.com/ayushnag>`_.
- Load scalar variables by default. (:pull:`205`)
  By `Gustavo Hidalgo <https://github.com/ghidalgo3>`_.
- Support empty files (:pull:`260`)
  By `Justus Magin <https://github.com/keewis>`_.
- Can write virtual datasets to Icechunk stores using `vitualize.to_icechunk` (:pull:`256`)
  By `Matt Iannucci <https://github.com/mpiannucci>`_.

Breaking changes
~~~~~~~~~~~~~~~~

- Serialize valid ZarrV3 metadata and require full compressor numcodec config (for :pull:`193`)
  By `Gustavo Hidalgo <https://github.com/ghidalgo3>`_.
- VirtualiZarr's `ZArray`, `ChunkEntry`, and `Codec` no longer subclass
  `pydantic.BaseModel` (:pull:`210`)
- `ZArray`'s `__init__` signature has changed to match `zarr.Array`'s (:pull:`210`)

Deprecations
~~~~~~~~~~~~

- Depreciates cftime_variables in open_virtual_dataset in favor of decode_times. (:pull:`232`)
  By `Raphael Hagen <https://github.com/norlandrhagen>`_.

Bug fixes
~~~~~~~~~

- Exclude empty chunks during `ChunkDict` construction. (:pull:`198`)
  By `Gustavo Hidalgo <https://github.com/ghidalgo3>`_.
- Fixed regression in `fill_value` handling for datetime dtypes making virtual
  Zarr stores unreadable (:pull:`206`)
  By `Timothy Hodson <https://github.com/thodson-usgs>`_

Documentation
~~~~~~~~~~~~~

- Adds virtualizarr + coiled serverless example notebook (:pull:`223`)
  By `Raphael Hagen <https://github.com/norlandrhagen>`_.

Internal Changes
~~~~~~~~~~~~~~~~

- Refactored internal structure significantly to split up everything to do with reading references from that to do with writing references.
  (:issue:`229`) (:pull:`231`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Refactored readers to consider every filetype as a separate reader, all standardized to present the same `open_virtual_dataset` interface internally.
  (:pull:`261`) By `Tom Nicholas <https://github.com/TomNicholas>`_.

.. _v1.0.0:

v1.0.0 (9th July 2024)
----------------------

This release marks VirtualiZarr as mostly feature-complete, in the sense of achieving feature parity with kerchunk's logic for combining datasets, providing an easier way to manipulate kerchunk references in memory and generate kerchunk reference files on disk.

Future VirtualiZarr development will focus on generalizing and upstreaming useful concepts into the Zarr specification, the Zarr-Python library, Xarray, and possibly some new packages. See the roadmap in the documentation for details.

New Features
~~~~~~~~~~~~

- Now successfully opens both tiff and FITS files. (:issue:`160`, :pull:`162`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Added a `.rename_paths` convenience method to rename paths in a manifest according to a function.
  (:pull:`152`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- New ``cftime_variables`` option on ``open_virtual_dataset`` enables encoding/decoding time.
  (:pull:`122`) By `Julia Signell <https://github.com/jsignell>`_.

Breaking changes
~~~~~~~~~~~~~~~~

- Requires numpy 2.0 (for :pull:`107`).
  By `Tom Nicholas <https://github.com/TomNicholas>`_.

Deprecations
~~~~~~~~~~~~


Bug fixes
~~~~~~~~~

- Ensure that `_ARRAY_DIMENSIONS` are dropped from variable `.attrs`. (:issue:`150`, :pull:`152`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Ensure that `.attrs` on coordinate variables are preserved during round-tripping. (:issue:`155`, :pull:`154`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Ensure that non-dimension coordinate variables described via the CF conventions are preserved during round-tripping. (:issue:`105`, :pull:`156`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.

Documentation
~~~~~~~~~~~~~

- Added example of using cftime_variables to usage docs. (:issue:`169`, :pull:`174`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Updated the development roadmap in preparation for v1.0. (:pull:`164`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Warn if user passes `indexes=None` to `open_virtual_dataset` to indicate that this is not yet fully supported.
  (:pull:`170`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Clarify that virtual datasets cannot be treated like normal xarray datasets. (:issue:`173`)
  By `Tom Nicholas <https://github.com/TomNicholas>`_.

Internal Changes
~~~~~~~~~~~~~~~~

- Refactor `ChunkManifest` class to store chunk references internally using numpy arrays.
  (:pull:`107`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Mark tests which require network access so that they are only run when `--run-network-tests` is passed a command-line argument to pytest.
  (:pull:`144`) By `Tom Nicholas <https://github.com/TomNicholas>`_.
- Determine file format from magic bytes rather than name suffix
  (:pull:`143`) By `Scott Henderson <https://github.com/scottyhq>`_.

.. _v0.1:

v0.1 (17th June 2024)
---------------------

v0.1 is the first release of VirtualiZarr!! It contains functionality for using kerchunk to find byte ranges in netCDF files,
constructing an xarray.Dataset containing ManifestArray objects, then writing out such a dataset to kerchunk references as either json or parquet.

New Features
~~~~~~~~~~~~


Breaking changes
~~~~~~~~~~~~~~~~


Deprecations
~~~~~~~~~~~~


Bug fixes
~~~~~~~~~


Documentation
~~~~~~~~~~~~~


Internal Changes
~~~~~~~~~~~~~~~~
