project('mimalloc', 'c', 'cpp')

srcs = files(
    'src/alloc-aligned.c',
    'src/alloc-posix.c',
    'src/alloc.c',
    'src/arena.c',
    'src/bitmap.c',
    'src/heap.c',
    'src/init.c',
    'src/options.c',
    'src/os.c',
    'src/page.c',
    'src/prim/prim.c',
    'src/random.c',
    'src/segment-map.c',
    'src/segment.c',
    'src/stats.c',
)
fs = import('fs')
tgts = []
foreach file : srcs
    name = fs.stem(file)
    tgts += fs.copyfile(file, name + '.cpp')
endforeach
inc = include_directories('src', 'src/prim', 'include')

mimalloc_lib = static_library(
    'mimalloc',
    tgts,
    pic: true,
    c_args: [
        '-DMI_STATIC_LIB',
        '-ftls-model=initial-exec',
        '-fno-builtin-malloc',
    ],
    include_directories: inc,
    link_language: 'cpp',
    install: false,
)
mimalloc_dep = declare_dependency(
    include_directories: inc,
    link_with: [mimalloc_lib],
)

subdir('test')
