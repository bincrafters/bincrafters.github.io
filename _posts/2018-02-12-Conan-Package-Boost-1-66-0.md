---
layout: post
title: 'Conan Packages - Boost v1.66.0'
tags: [C++, Conan.io, Boost, Bintray]
---

After much delay, the Bincrafters team has completed the Boost 1.66.0 modular packages, and they're finally ready for consumption.  In case you're new to Bincrafters, you can find the link to the repository here:  [Bincrafters Public Conan Repository on Bintray](https://bintray.com/bincrafters/public-conan).  Along with this release, we're also announcing a general request for assistance from the Conan user community.  Please read on for more details.  

## Call to Action
If you want to help support the Bincrafters team and the modular Boost packages, now is your chance.  We have a very simple need, and so the contributions we are looking for are extremely small.  In short, we need tests. Boost has ~35 libraries which require compilation and we've written tests for each of those.  However, there are 100 header-only libraries, and so far we've only created `test_packages` for a few of them.   So, if you want to contribute and know how to write a `test_package` for Conan, please choose a library from the list at the bottom of this post. 

## Conan Center
We've been asked about Conan Center many times, and the answer is Yes!  We do plan on submitting to Conan Center in the near future, and we have the support of the Conan team.  In the meantime, the more usage feedback we get in our github issues list and slack channel the better: 
https://github.com/bincrafters/community/issues

## Usage Notes
There are ~135 libraries in Boost, so obviously there are a few nuances related to the packages which users might want to know.  We've created a page in our documentation to capture all these usage details, and will continue to add to it over time.  

[Usage Notes for Boost Packages](http://bincrafters.readthedocs.io/en/latest/package_notes.html#boost)

Here are some highlights: 
- `FindBoost.cmake` : CMake refs to Boost::xyz and Boost_FOUND now work
- `all` : bugfixes... bugs and important flags fixed everywhere
- `all` : packages now built with both libcxx options (libstdc and libstdc++11)
- `boost_iostreams` : zlib, bzip2, and lzma compressors are enabled by default 
- `boost_python` : improved version and python path detection. better override options.
- `misc` : C++11 Only Libraries include: `log`, `context`, `coroutine`, `fiber`

## Backporting
We are currently in the process of rebuilding 1.65.1 and 1.64.0 with the new changes.  We hope this will be ready by 2/20/2018.   

## List of Header-Only Libraries Which Need Testing
Please feel free to fork and add a `test_package`, and submit a PR back.  

### Notes: 
- Please submit the PR back to `testing/1.66.0` branch.
- Please do not use the example from the libraries documentation. 
- Please write some minimum amount of code to instantiate some class from the library. 
Example: [Boost Random test_package](https://github.com/bincrafters/conan-boost_random/blob/stable/1.66.0/test_package/test_package.cpp)

[https://github.com/bincrafters/conan-boost_callable_traits](https://github.com/bincrafters/conan-boost_callable_traits)
[https://github.com/bincrafters/conan-boost_compatibility](https://github.com/bincrafters/conan-boost_compatibility)
[https://github.com/bincrafters/conan-boost_config](https://github.com/bincrafters/conan-boost_config)
[https://github.com/bincrafters/conan-boost_predef](https://github.com/bincrafters/conan-boost_predef)
[https://github.com/bincrafters/conan-boost_preprocessor](https://github.com/bincrafters/conan-boost_preprocessor)
[https://github.com/bincrafters/conan-boost_assert](https://github.com/bincrafters/conan-boost_assert)
[https://github.com/bincrafters/conan-boost_io](https://github.com/bincrafters/conan-boost_io)
[https://github.com/bincrafters/conan-boost_mp11](https://github.com/bincrafters/conan-boost_mp11)
[https://github.com/bincrafters/conan-boost_static_assert](https://github.com/bincrafters/conan-boost_static_assert)
[https://github.com/bincrafters/conan-boost_vmd](https://github.com/bincrafters/conan-boost_vmd)
[https://github.com/bincrafters/conan-boost_winapi](https://github.com/bincrafters/conan-boost_winapi)
[https://github.com/bincrafters/conan-boost_core](https://github.com/bincrafters/conan-boost_core)
[https://github.com/bincrafters/conan-boost_throw_exception](https://github.com/bincrafters/conan-boost_throw_exception)
[https://github.com/bincrafters/conan-boost_align](https://github.com/bincrafters/conan-boost_align)
[https://github.com/bincrafters/conan-boost_array](https://github.com/bincrafters/conan-boost_array)
[https://github.com/bincrafters/conan-boost_bind](https://github.com/bincrafters/conan-boost_bind)
[https://github.com/bincrafters/conan-boost_integer](https://github.com/bincrafters/conan-boost_integer)
[https://github.com/bincrafters/conan-boost_logic](https://github.com/bincrafters/conan-boost_logic)
[https://github.com/bincrafters/conan-boost_move](https://github.com/bincrafters/conan-boost_move)
[https://github.com/bincrafters/conan-boost_type_traits](https://github.com/bincrafters/conan-boost_type_traits)
[https://github.com/bincrafters/conan-boost_crc](https://github.com/bincrafters/conan-boost_crc)
[https://github.com/bincrafters/conan-boost_smart_ptr](https://github.com/bincrafters/conan-boost_smart_ptr)
[https://github.com/bincrafters/conan-boost_tuple](https://github.com/bincrafters/conan-boost_tuple)
[https://github.com/bincrafters/conan-boost_level5group](https://github.com/bincrafters/conan-boost_level5group)
[https://github.com/bincrafters/conan-boost_concept_check](https://github.com/bincrafters/conan-boost_concept_check)
[https://github.com/bincrafters/conan-boost_conversion](https://github.com/bincrafters/conan-boost_conversion)
[https://github.com/bincrafters/conan-boost_detail](https://github.com/bincrafters/conan-boost_detail)
[https://github.com/bincrafters/conan-boost_function](https://github.com/bincrafters/conan-boost_function)
[https://github.com/bincrafters/conan-boost_function_types](https://github.com/bincrafters/conan-boost_function_types)
[https://github.com/bincrafters/conan-boost_functional](https://github.com/bincrafters/conan-boost_functional)
[https://github.com/bincrafters/conan-boost_fusion](https://github.com/bincrafters/conan-boost_fusion)
[https://github.com/bincrafters/conan-boost_iterator](https://github.com/bincrafters/conan-boost_iterator)
[https://github.com/bincrafters/conan-boost_mpl](https://github.com/bincrafters/conan-boost_mpl)
[https://github.com/bincrafters/conan-boost_optional](https://github.com/bincrafters/conan-boost_optional)
[https://github.com/bincrafters/conan-boost_type_index](https://github.com/bincrafters/conan-boost_type_index)
[https://github.com/bincrafters/conan-boost_typeof](https://github.com/bincrafters/conan-boost_typeof)
[https://github.com/bincrafters/conan-boost_utility](https://github.com/bincrafters/conan-boost_utility)
[https://github.com/bincrafters/conan-boost_any](https://github.com/bincrafters/conan-boost_any)
[https://github.com/bincrafters/conan-boost_endian](https://github.com/bincrafters/conan-boost_endian)
[https://github.com/bincrafters/conan-boost_format](https://github.com/bincrafters/conan-boost_format)
[https://github.com/bincrafters/conan-boost_gil](https://github.com/bincrafters/conan-boost_gil)
[https://github.com/bincrafters/conan-boost_hana](https://github.com/bincrafters/conan-boost_hana)
[https://github.com/bincrafters/conan-boost_intrusive](https://github.com/bincrafters/conan-boost_intrusive)
[https://github.com/bincrafters/conan-boost_lambda](https://github.com/bincrafters/conan-boost_lambda)
[https://github.com/bincrafters/conan-boost_multi_array](https://github.com/bincrafters/conan-boost_multi_array)
[https://github.com/bincrafters/conan-boost_numeric_conversion](https://github.com/bincrafters/conan-boost_numeric_conversion)
[https://github.com/bincrafters/conan-boost_numeric_interval](https://github.com/bincrafters/conan-boost_numeric_interval)
[https://github.com/bincrafters/conan-boost_polygon](https://github.com/bincrafters/conan-boost_polygon)
[https://github.com/bincrafters/conan-boost_qvm](https://github.com/bincrafters/conan-boost_qvm)
[https://github.com/bincrafters/conan-boost_rational](https://github.com/bincrafters/conan-boost_rational)
[https://github.com/bincrafters/conan-boost_scope_exit](https://github.com/bincrafters/conan-boost_scope_exit)
[https://github.com/bincrafters/conan-boost_tokenizer](https://github.com/bincrafters/conan-boost_tokenizer)
[https://github.com/bincrafters/conan-boost_tti](https://github.com/bincrafters/conan-boost_tti)
[https://github.com/bincrafters/conan-boost_local_function](https://github.com/bincrafters/conan-boost_local_function)
[https://github.com/bincrafters/conan-boost_range](https://github.com/bincrafters/conan-boost_range)
[https://github.com/bincrafters/conan-boost_ratio](https://github.com/bincrafters/conan-boost_ratio)
[https://github.com/bincrafters/conan-boost_circular_buffer](https://github.com/bincrafters/conan-boost_circular_buffer)
[https://github.com/bincrafters/conan-boost_foreach](https://github.com/bincrafters/conan-boost_foreach)
[https://github.com/bincrafters/conan-boost_lexical_cast](https://github.com/bincrafters/conan-boost_lexical_cast)
[https://github.com/bincrafters/conan-boost_proto](https://github.com/bincrafters/conan-boost_proto)
[https://github.com/bincrafters/conan-boost_unordered](https://github.com/bincrafters/conan-boost_unordered)
[https://github.com/bincrafters/conan-boost_algorithm](https://github.com/bincrafters/conan-boost_algorithm)
[https://github.com/bincrafters/conan-boost_phoenix](https://github.com/bincrafters/conan-boost_phoenix)
[https://github.com/bincrafters/conan-boost_variant](https://github.com/bincrafters/conan-boost_variant)
[https://github.com/bincrafters/conan-boost_xpressive](https://github.com/bincrafters/conan-boost_xpressive)
[https://github.com/bincrafters/conan-boost_multiprecision](https://github.com/bincrafters/conan-boost_multiprecision)
[https://github.com/bincrafters/conan-boost_parameter](https://github.com/bincrafters/conan-boost_parameter)
[https://github.com/bincrafters/conan-boost_heap](https://github.com/bincrafters/conan-boost_heap)
[https://github.com/bincrafters/conan-boost_lockfree](https://github.com/bincrafters/conan-boost_lockfree)
[https://github.com/bincrafters/conan-boost_metaparse](https://github.com/bincrafters/conan-boost_metaparse)
[https://github.com/bincrafters/conan-boost_pool](https://github.com/bincrafters/conan-boost_pool)
[https://github.com/bincrafters/conan-boost_spirit](https://github.com/bincrafters/conan-boost_spirit)
[https://github.com/bincrafters/conan-boost_convert](https://github.com/bincrafters/conan-boost_convert)
[https://github.com/bincrafters/conan-boost_dll](https://github.com/bincrafters/conan-boost_dll)
[https://github.com/bincrafters/conan-boost_dynamic_bitset](https://github.com/bincrafters/conan-boost_dynamic_bitset)
[https://github.com/bincrafters/conan-boost_geometry](https://github.com/bincrafters/conan-boost_geometry)
[https://github.com/bincrafters/conan-boost_icl](https://github.com/bincrafters/conan-boost_icl)
[https://github.com/bincrafters/conan-boost_interprocess](https://github.com/bincrafters/conan-boost_interprocess)
[https://github.com/bincrafters/conan-boost_msm](https://github.com/bincrafters/conan-boost_msm)
[https://github.com/bincrafters/conan-boost_multi_index](https://github.com/bincrafters/conan-boost_multi_index)
[https://github.com/bincrafters/conan-boost_numeric_ublas](https://github.com/bincrafters/conan-boost_numeric_ublas)
[https://github.com/bincrafters/conan-boost_ptr_container](https://github.com/bincrafters/conan-boost_ptr_container)
[https://github.com/bincrafters/conan-boost_sort](https://github.com/bincrafters/conan-boost_sort)
[https://github.com/bincrafters/conan-boost_statechart](https://github.com/bincrafters/conan-boost_statechart)
[https://github.com/bincrafters/conan-boost_units](https://github.com/bincrafters/conan-boost_units)
[https://github.com/bincrafters/conan-boost_uuid](https://github.com/bincrafters/conan-boost_uuid)
[https://github.com/bincrafters/conan-boost_accumulators](https://github.com/bincrafters/conan-boost_accumulators)
[https://github.com/bincrafters/conan-boost_assign](https://github.com/bincrafters/conan-boost_assign)
[https://github.com/bincrafters/conan-boost_coroutine2](https://github.com/bincrafters/conan-boost_coroutine2)
[https://github.com/bincrafters/conan-boost_flyweight](https://github.com/bincrafters/conan-boost_flyweight)
[https://github.com/bincrafters/conan-boost_poly_collection](https://github.com/bincrafters/conan-boost_poly_collection)
[https://github.com/bincrafters/conan-boost_property_tree](https://github.com/bincrafters/conan-boost_property_tree)
[https://github.com/bincrafters/conan-boost_signals](https://github.com/bincrafters/conan-boost_signals)
[https://github.com/bincrafters/conan-boost_asio](https://github.com/bincrafters/conan-boost_asio)
[https://github.com/bincrafters/conan-boost_bimap](https://github.com/bincrafters/conan-boost_bimap)
[https://github.com/bincrafters/conan-boost_compute](https://github.com/bincrafters/conan-boost_compute)
[https://github.com/bincrafters/conan-boost_disjoint_sets](https://github.com/bincrafters/conan-boost_disjoint_sets)
[https://github.com/bincrafters/conan-boost_property_map](https://github.com/bincrafters/conan-boost_property_map)
[https://github.com/bincrafters/conan-boost_beast](https://github.com/bincrafters/conan-boost_beast)
[https://github.com/bincrafters/conan-boost_numeric_odeint](https://github.com/bincrafters/conan-boost_numeric_odeint)
[https://github.com/bincrafters/conan-boost_process](https://github.com/bincrafters/conan-boost_process)
