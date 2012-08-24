# Copyright (C) 2012 LuaDist.
# Created by Peter Drahoš
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

project ( numlua C )
cmake_minimum_required ( VERSION 2.8 )
include ( cmake/dist.cmake )
include ( lua )

find_path ( LAPACKE_INCLUDE_DIR lapacke.h )
include_directories ( ${LAPACKE_INCLUDE_DIR} )

find_library ( LAPACK_LIBRARY NAMES lapack )
find_library ( BLAS_LIBRARY NAMES blas )
find_library ( HDF5_LIBRARY NAMES hdf5 )
find_library ( FFTW3_LIBRARY NAMES fftw3 )
set ( LIBS ${LAPACK_LIBRARY} ${BLAS_LIBRARY} ${HDF5_LIBRARY} ${FFTW3_LIBRARY} )

install_lua_module ( numlua numlua.c complex.c fft.c msort.c lmatrix.c mt.c ranlib.c rng.c dcdflib.c ipmpar.c stat.c amos.c mathx.c LINK ${LIBS} )
install_doc ( docs/ )
install_example ( examples/ )

# lhp files are considered documentation and are install into lmod dirs.
install ( DIRECTORY lhp DESTINATION ${INSTALL_LMOD} COMPONENT Documentation )