import os

VariantDir('build', 'src')
GTEST_HOME = '/home/limjh/oss/gtest-1.7.0'
GTEST_INCLUDE = os.path.join(GTEST_HOME, 'include')

testEnv = Environment(
    ENV = os.environ,
    CCFLAGS='-O0 -ggdb -Wall -I %s' % (GTEST_INCLUDE), 
    CFLAGS='-fprofile-arcs -ftest-coverage -std=c99',
    LINKFLAGS='-fprofile-arcs -ftest-coverage',
    LIBPATH=GTEST_HOME,
    LIBS=['pthread', 'libgtest']
)

uninitialized01Prog = testEnv.Program(
    'uninitialized01.ut',
    ['build/uninitialized01.c', 'build/uninitialized01_test.cc']
)

illegalAccess01Prog = testEnv.Program(
    'illegalAccess01.ut',
    ['build/illegal_access01.c', 'build/illegal_access01_test.cc']
)

memoryLeak01Prog = testEnv.Program(
    'memoryLeak01.ut',
    ['build/memory_leak01.c', 'build/memory_leak01_test.cc']
)

strcpy01Prog = testEnv.Program(
    'strcpy01.ut',
    ['build/strcpy01.c', 'build/strcpy01_test.cc']
)

uninittestReport= testEnv.Command('unit_report.xml', uninitialized01Prog, "./uninitialized01.ut --gtest_output=xml:${TARGET}")

illegaltestReport= testEnv.Command('illegal_report.xml', illegalAccess01Prog, "./illegalAccess01.ut --gtest_output=xml:${TARGET}")

memleaktestReport= testEnv.Command('memleak_report.xml', memoryLeak01Prog, "./memoryLeak01.ut --gtest_output=xml:${TARGET}")

artifacts = [
    uninitialized01Prog,
    illegalAccess01Prog,
    memoryLeak01Prog,
    strcpy01Prog,
    uninittestReport
]

testEnv.Clean(artifacts, 'build')
Default(artifacts)

