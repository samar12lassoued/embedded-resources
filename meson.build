project('Embedded Resources',
	[
		'cpp',
		'c'
	],
	default_options : [
		'cpp_std=c++17',
		'c_std=c11'
	])

#########################
# Process Build Options #
#########################

# Pick up our common compiler variables + desired_*_flags variables
subdir('build/compiler')
subdir('build/compiler/c')
subdir('build/compiler/cpp')

add_project_arguments('-Wno-unknown-pragmas', language: ['cpp', 'c'])

if get_option('disable-rtti') == true
	add_project_arguments('-fno-rtti', language : 'cpp')
endif

if get_option('disable-exceptions') == true
	add_project_arguments(['-fno-exceptions', '-fno-unwind-tables'], language : 'cpp')
endif

if get_option('enable-werror') == true
	add_project_arguments('-Werror', language : ['cpp', 'c'])
endif

if get_option('enable-pedantic-error') == true
	add_project_arguments('-pedantic-error', language : ['cpp', 'c'])
endif

#################
# Build Modules #
#################

subdir('build/linker/linker-map')
subdir('build/test/cmocka')

# Pre-declare these variables here so that we can add files to the list
# throughout the source tree, passing them to the test tree later.
cmocka_test_deps = []
catch2_tests_dep = []

#######################
# Process source tree #
#######################s

subdir('examples')
subdir('interview')
subdir('test')

# Defined after source folders so catch2_dep is fully populated
# when creating the built-in targets
subdir('build/test/catch2')

###################
# Tooling Modules #
###################

clangformat_targets = [
	meson.source_root() / 'examples',
	meson.source_root() / 'interview',
	meson.source_root() / 'test',
]

clangformat_excludes = [
	meson.source_root() / 'examples/cpp/etl',
	meson.source_root() / 'examples/rtos',
	meson.source_root() / 'examples/libcpp',
]

subdir('build/analysis/clang-tidy')
subdir('build/analysis/complexity')
subdir('build/analysis/cppcheck')
subdir('build/analysis/sloccount')
subdir('build/format')
