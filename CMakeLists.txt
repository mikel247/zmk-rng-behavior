# Copyright (c) 2024
# SPDX-License-Identifier: MIT

cmake_minimum_required(VERSION 3.20)

if(CONFIG_ZMK_BEHAVIOR_RNG_TYPER)
    zephyr_include_dirs(behaviors/rng_typer/include)
    target_sources(app PRIVATE behaviors/rng_typer/src/rng_typer.c)
endif()
