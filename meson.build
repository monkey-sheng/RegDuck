project('RegDuck', 'c', 'cpp',
  default_options: ['warning_level=1', 'optimization=0']
)

inc_dir = include_directories('/usr/local/include')
re2_dep = meson.get_compiler('cpp').find_library('re2', dirs: '/usr/local/lib', required: true)
absl_dep = meson.get_compiler('cpp').find_library('absl', dirs: '/usr/local/lib', required: true)

# # Find duckdb dependency
# duckdb_lib = declare_dependency(
#   include_directories: include_directories('third-party'),
#   link_args: ['-L/Users/kaiwenzheng/Documents/RegDuck/third-party/duckdb', '-lduckdb']
# )

# Run the right benchmark
which_main = 'src/main.cpp'
is_bench_re2 = get_option('bench_re2')
is_bench_duckdb = get_option('bench_duckdb')
is_test_conn = get_option('test_conn')
if is_bench_re2
  which_main = 'benchmarks/regex_filter_re2.cpp'
elif is_bench_duckdb
  which_main = 'benchmarks/regex_filter_duckdb.cpp'
elif is_test_conn
  which_main = 'test/test_conn.cpp'
endif

executable('run',
  cpp_args: ['-std=c++17'],
  sources: ['src/parser/include/decoder/decoder.cpp',
            'src/parser/block/metadata_block.cpp',
            'src/parser/block/storage_block.cpp',
            'src/parser/statistics/base_statistics.cpp',
            'src/parser/statistics/distinct_statistics.cpp',
            'src/parser/row_group/row_group.cpp',
            'src/parser/schema/schema.cpp',
            'src/parser/table/table.cpp',
            'src/parser/type_info/type_info.cpp',
            'src/parser/header/main_header.cpp',
            'src/parser/header/database_header.cpp',
            'src/parser/database/database.cpp',
            'src/regduck_api.cpp',
            which_main],
  include_directories: inc_dir,
  dependencies: [re2_dep, absl_dep])
