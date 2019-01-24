load('//:buckaroo_macros.bzl', 'buckaroo_deps')
load('//:subdir_glob.bzl', 'subdir_glob')

genrule(
  name = 'udfread-version-h',
  out = 'udfread-version.h',
  srcs = [
    'src/udfread-version.h.in',
  ],
  cmd = ''.join([
    'cat $SRCS ',
    ' | sed -e \'s/@UDFREAD_VERSION_MAJOR@/0/g\' ',
    ' | sed -e \'s/@UDFREAD_VERSION_MINOR@/0/g\' ',
    ' | sed -e \'s/@UDFREAD_VERSION_MICRO@/0/g\' ',
    ' > $OUT',
  ]),
)

cxx_library(
  name = 'udfread',
  header_namespace = '',
  exported_headers = {
    'udfread.h': 'src/udfread.h',
  },
  headers = dict(
    subdir_glob([
      ('src', '**/*.h'),
    ]).items() + [
      ('udfread-version.h', ':udfread-version-h')
    ]
  ),
  srcs = glob([
    'src/**/*.c',
  ]),
  deps = buckaroo_deps(),
  visibility = [
    'PUBLIC',
  ],
)
