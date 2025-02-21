cmake_minimum_required(VERSION 3.24)
project(slowmokit C CXX)

# If we are not using Visual Studio, use the GNU install directories module.
# Otherwise set the values manually.
if (NOT MSVC)
    include(GNUInstallDirs)
else ()
    set(CMAKE_INSTALL_BINDIR ${CMAKE_INSTALL_PREFIX}/bin)
    set(CMAKE_INSTALL_LIBDIR ${CMAKE_INSTALL_PREFIX}/lib)
    set(CMAKE_INSTALL_MANDIR ${CMAKE_INSTALL_PREFIX}/man)
    set(CMAKE_INSTALL_DOCDIR ${CMAKE_INSTALL_PREFIX}/share/doc/slowmokit)
    set(CMAKE_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_PREFIX}/include)
endif ()

# Ensure that GCC is new enough, if the compiler is GCC.
if (CMAKE_COMPILER_IS_GNUCC AND CMAKE_CXX_COMPILER_VERSION VERSION_LESS 5)
    message(FATAL_ERROR "GCC version (${CMAKE_CXX_COMPILER_VERSION}) is too old! 5.x or newer is required.")
endif ()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(src/slowmokit)

add_library(slowmokit
        src/slowmokit.hpp


        # base files
        src/slowmokit/base.hpp
        src/slowmokit/core.hpp
        src/slowmokit/prereqs.hpp

        # ducks
        src/slowmokit/ducks/ducks.hpp
        src/slowmokit/ducks/io/io.hpp
        src/slowmokit/ducks/io/io.cpp
        src/slowmokit/ducks/matrix/matrix.hpp
        src/slowmokit/ducks/matrix/matrix_main.cpp
        src/slowmokit/ducks/matrix/matrix_free.cpp

        # methods
        src/slowmokit/models/model.hpp
        src/slowmokit/methods/neighbors/knn/knn.cpp
        src/slowmokit/methods/neighbors/knn/knn.hpp
        src/slowmokit/methods/linear_model/linear_regression.hpp
        src/slowmokit/methods/linear_model/linear_regression/linear_regression.hpp
        src/slowmokit/methods/linear_model/linear_regression/linear_regression.cpp
        src/slowmokit/methods/cluster/kMeans/kMeans.cpp
        src/slowmokit/methods/cluster/kMeans/kMeans.hpp
        src/slowmokit/methods/cluster/kMeans.hpp
        src/slowmokit/methods/metrics/accuracy.hpp
        src/slowmokit/methods/metrics/accuracy.cpp
        src/slowmokit/methods/preprocessing/normalization.hpp
        src/slowmokit/methods/preprocessing/normalization.cpp
        src/slowmokit/methods/preprocessing/standardization.hpp
        src/slowmokit/methods/preprocessing/standardization.cpp
        src/slowmokit/methods/neighbors/bernoulli_nb.hpp
        src/slowmokit/methods/neighbors/bernoulli_nb/bernoulli_nb.hpp
        src/slowmokit/methods/neighbors/bernoulli_nb/bernoulli_nb.cpp
        src/slowmokit/methods/linear_model/logistic_regression.hpp
        src/slowmokit/methods/linear_model/logistic_regression/logistic_regression.hpp
        src/slowmokit/methods/linear_model/logistic_regression/logistic_regression.cpp
        src/slowmokit/methods/preprocessing/label_encoder.cpp
        src/slowmokit/methods/preprocessing/label_encoder.hpp
        src/slowmokit/methods/metrics/classification_report.hpp
        src/slowmokit/methods/metrics/classification_report.cpp
        src/slowmokit/methods/neighbors/gaussian_nb.hpp
        src/slowmokit/methods/neighbors/gaussian_nb/gaussian_nb.cpp
        src/slowmokit/methods/neighbors/gaussian_nb/gaussian_nb.hpp
        src/slowmokit/methods/neighbors/knn.hpp
        src/slowmokit/methods/neighbors/knn/knn.hpp
        src/slowmokit/methods/neighbors/knn/knn.cpp
        src/slowmokit/methods/preprocessing/one_hot_encoder.hpp
        src/slowmokit/methods/preprocessing/one_hot_encoder.cpp
        src/slowmokit/methods/metrics/precision.hpp
        src/slowmokit/methods/metrics/precision.cpp
        src/slowmokit/methods/metrics/recall.hpp
        src/slowmokit/methods/metrics/recall.cpp
        src/slowmokit/methods/metrics/f1score.hpp
        src/slowmokit/methods/metrics/f1score.cpp
        src/slowmokit/methods/metrics/mean_squared_error.hpp
        src/slowmokit/methods/metrics/mean_squared_error.cpp
        src/slowmokit/methods/metrics/silhouette_score.cpp
        src/slowmokit/methods/metrics/silhouette_score.hpp)

