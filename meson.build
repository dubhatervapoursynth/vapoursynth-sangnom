project('SangNom', 'cpp',
    default_options: ['buildtype=release', 'warning_level=2', 'b_lto=true', 'b_ndebug=if-release', 'cpp_std=c++17'],
    license: 'MIT',
    license_files: 'LICENSE',
    meson_version: '>=1.2.3',
    version: '45.0',
)

cflags = [
]

host_cpu_family = host_machine.cpu_family()

if host_cpu_family.startswith('x86')
    cflags += ['-DVS_TARGET_CPU_X86=1']
endif

incdir = include_directories(
    run_command(
        find_program('python', 'python3'),
        '-c',
        'import vapoursynth as vs; print(vs.get_include())',
        check: true,
    ).stdout().strip(),
)

py = import('python').find_installation(pure: false)

shared_module('sangnom',
    files('src/sangnom.cpp'),
    gnu_symbol_visibility: 'hidden',
    include_directories: incdir,
    cpp_args: cflags,
    install: true,
    install_dir: py.get_install_dir() / 'vapoursynth/plugins',
    name_prefix: '',
)