unix_common = [
  'src/unix/async.c',
  'src/unix/core.c',
  'src/unix/dl.c',
  'src/unix/fs.c',
  'src/unix/fsevents.c',
  'src/unix/getaddrinfo.c',
  'src/unix/getnameinfo.c',
  'src/unix/kqueue.c',
  'src/unix/loop-watcher.c',
  'src/unix/loop.c',
  'src/unix/pipe.c',
  'src/unix/poll.c',
  'src/unix/process.c',
  'src/unix/proctitle.c',
  'src/unix/pthread-barrier.c',
  'src/unix/pthread-fixes.c',
  'src/unix/signal.c',
  'src/unix/stream.c',
  'src/unix/tcp.c',
  'src/unix/thread.c',
  'src/unix/timer.c',
  'src/unix/tty.c',
  'src/unix/udp.c'
]

cxx_library(
  name = 'uv',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('include', '*.h'),
  ]),
  headers = subdir_glob([
    ('src', '*.h'),
  ]),
  platform_headers = [
    ('.*', subdir_glob([('src/unix', '**/*.h')])),
    ('macosx', glob(['src/unix/darwin.h'])),
    ('linux', subdir_glob([('src/unix', '**/*.h')])),
    ('windows', glob(['src/win/**/*.h'])),
  ],
  srcs = glob([
    'src/*.c',
  ]),
  platform_srcs = [
    ('.*', unix_common + ['src/unix/darwin.c', 'src/unix/darwin-proctitle.c']),
    ('macos', unix_common + ['src/unix/darwin.c', 'src/unix/darwin-proctitle.c']),
    ('linux', glob(['src/unix/**/*.c'])),
    ('windows', glob(['src/win/**/*.c'])),
  ],
  compiler_flags = [
    '-std=c11',
  ],
  visibility = [
    'PUBLIC',
  ],
)

cxx_binary(
  name = 'tests',
  header_namespace = '',
  headers = subdir_glob([
    ('test', 'runner.h'),
  ]),
  platform_headers = [
    ('.*', glob(['test/*-unix.h'])),
    ('macos', glob(['test/*-unix.h'])),
    ('linux', glob(['test/*-unix.h'])),
    ('windows', glob(['test/*-win.h'])),
  ],
  srcs = glob([
    'test/run-tests.c',
    'test/runner.c',
    'test/echo-server.c',
    'test/test-*.c',
  ], 
  excludes = glob([
    'test/*-unix.c',
    'test/*-win.c',
  ])),
  platform_srcs = [
    ('.*', glob(['test/*-unix.c'])),
    ('macos', glob(['test/*-unix.c'])),
    ('linux', glob(['test/*-unix.c'])),
    ('windows', glob(['test/*-win.c'])),
  ],
  deps = [
    ':uv',
  ],
)

cxx_binary(
  name = 'benchmarks',
  header_namespace = '',
  headers = subdir_glob([
    ('test', 'runner.h'),
  ]),
  platform_headers = [
    ('.*', glob(['test/*-unix.h'])),
    ('macos', glob(['test/*-unix.h'])),
    ('linux', glob(['test/*-unix.h'])),
    ('windows', glob(['test/*-win.h'])),
  ],
  srcs = glob([
    'test/run-benchmarks.c',
    'test/runner.c',
    'test/blackhole-server.c',
    'test/echo-server.c',
    'test/benchmark-*.c',
  ], 
  excludes = glob([
    'test/*-unix.c',
    'test/*-win.c',
  ])),
  platform_srcs = [
    ('.*', glob(['test/*-unix.c'])),
    ('macos', glob(['test/*-unix.c'])),
    ('linux', glob(['test/*-unix.c'])),
    ('windows', glob(['test/*-win.c'])),
  ],
  deps = [
    ':uv',
  ],
)
