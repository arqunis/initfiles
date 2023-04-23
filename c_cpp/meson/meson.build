project('example', ['cpp'],
  version : '0.0.1',
  default_options : [
    'warning_level=3',
    'cpp_std=c++17',
  ],
)

prefix = get_option('prefix')
libdir = prefix / get_option('libdir')
bindir = prefix / get_option('bindir')

inc = include_directories('include')

sources = files(
    'src/example.cpp',
)

headers = [
    'include/example.hpp',
]

libexample = library('example', sources + files(headers),
  include_directories : inc,
  version : meson.project_version(),
  soversion : '0',
  install : true,
  install_dir : libdir,
)

libexample_dep = declare_dependency(
  link_with : libexample,
  include_directories : inc,
)

program = executable('program', 'src/main.cpp',
    dependencies : [libexample_dep],
    install : true,
    install_dir : bindir,
)

install_headers(headers)

subdir('tests')
