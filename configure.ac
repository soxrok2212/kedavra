dnl
dnl Copyright (c) 2023
dnl     Andrew LaMarche
dnl
dnl Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([kedavra], [m4_esyscmd_s(cat VERSION)], [andrew@lamarche.me])
AM_INIT_AUTOMAKE
AC_PROG_CC
AC_LANG(C)

dnl
dnl Get pcap include dir

pcap_include_dirs="/usr/include \
    /usr/include/pcap \
    /usr/local/include \
    /usr/local/include/pcap \
    /usr/share/include \
    /usr/share/include/pcap"

AC_ARG_WITH(pcap-include,
[  --with-pcap-include     specify the pcap include directory],
[PCAP_INCLUDE_DIR=$withval],
[PCAP_INCLUDE_DIR=$pcap_include_dirs])

pcap_include_dir=""
for dir in $PCAP_INCLUDE_DIR; do
    if [ -f ${dir}/pcap.h ]; then
        echo "found pcap headers in ${dir}"
        pcap_include_dir=${dir}
        break
    fi
done

if [ -z ${pcap_include_dir} ]; then
    echo "unable to locate pcap headers"
    exit 1
fi

PCAP_INCLUDE="-I$pcap_include_dir"

dnl
dnl Get pcap lib dir

pcap_lib_dirs="/usr/lib"

AC_ARG_WITH(pcap-lib,
[  --with-pcap-lib     specify the pcap lib directory],
[PCAP_LIB_DIR=$withval],
[PCAP_LIB_DIR=$pcap_lib_dirs])

pcap_lib_dir=""
for dir in $PCAP_LIB_DIR; do
    if [ -f ${dir}/*pcap*.so ]; then
        echo "found pcap libs in ${dir}"
        pcap_lib_dir=${dir}
        break
    fi
done

if [ -z ${pcap_lib_dir} ]; then
    echo "unable to locate pcap lib"
    exit 1
fi

PCAP_INCLUDE="-L$pcap_lib_dir"

AC_CONFIG_FILES([Makefile])

AC_OUTPUT
