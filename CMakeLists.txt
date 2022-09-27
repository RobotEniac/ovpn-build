cmake_minimum_required(VERSION 3.1)
project(openvpn)
set(CMAKE_C_STANDARD 99)

SET(THIRDPARTY_PATH "/usr/local/opt")
SET(OPENSSL_PATH "${THIRDPARTY_PATH}/openssl")

include_directories("${OPENSSL_PATH}/include")
include_directories("/usr/local/include")

link_directories("${OPENSSL_PATH}/lib")
link_directories("/usr/local/lib/")

set(openvpn_srcs
    src/compat/compat-basename.c
    src/compat/compat-daemon.c
    src/compat/compat-dirname.c
    src/compat/compat-gettimeofday.c
    src/compat/compat-inet_ntop.c
    src/compat/compat-inet_pton.c
    src/compat/compat-lz4.c
    src/openvpn/argv.c
    src/openvpn/base64.c
    src/openvpn/block_dns.c
    src/openvpn/buffer.c
    src/openvpn/clinat.c
    src/openvpn/comp-lz4.c
    src/openvpn/comp.c
    src/openvpn/compstub.c
    src/openvpn/console.c
    src/openvpn/console_builtin.c
    src/openvpn/console_systemd.c
    src/openvpn/crypto.c
    src/openvpn/crypto_mbedtls.c
    src/openvpn/crypto_openssl.c
    src/openvpn/cryptoapi.c
    src/openvpn/dhcp.c
    src/openvpn/error.c
    src/openvpn/event.c
    src/openvpn/fdmisc.c
    src/openvpn/forward.c
    src/openvpn/fragment.c
    src/openvpn/gremlin.c
    src/openvpn/helper.c
    src/openvpn/httpdigest.c
    src/openvpn/init.c
    src/openvpn/interval.c
    src/openvpn/list.c
    src/openvpn/lladdr.c
    src/openvpn/lzo.c
    src/openvpn/manage.c
    src/openvpn/mbuf.c
    src/openvpn/misc.c
    src/openvpn/mroute.c
    src/openvpn/mss.c
    src/openvpn/mstats.c
    src/openvpn/mtcp.c
    src/openvpn/mtu.c
    src/openvpn/mudp.c
    src/openvpn/multi.c
    src/openvpn/ntlm.c
    src/openvpn/occ.c
    src/openvpn/openvpn.c
    src/openvpn/options.c
    src/openvpn/otime.c
    src/openvpn/packet_id.c
    src/openvpn/perf.c
    src/openvpn/pf.c
    src/openvpn/ping.c
    src/openvpn/pkcs11.c
    src/openvpn/pkcs11_mbedtls.c
    src/openvpn/pkcs11_openssl.c
    src/openvpn/platform.c
    src/openvpn/plugin.c
    src/openvpn/pool.c
    src/openvpn/proto.c
    src/openvpn/proxy.c
    src/openvpn/ps.c
    src/openvpn/push.c
    src/openvpn/reliable.c
    src/openvpn/route.c
    src/openvpn/schedule.c
    src/openvpn/session_id.c
    src/openvpn/shaper.c
    src/openvpn/sig.c
    src/openvpn/socket.c
    src/openvpn/socks.c
    src/openvpn/ssl.c
    src/openvpn/ssl_mbedtls.c
    src/openvpn/ssl_openssl.c
    src/openvpn/ssl_verify.c
    src/openvpn/ssl_verify_mbedtls.c
    src/openvpn/ssl_verify_openssl.c
    src/openvpn/status.c
    src/openvpn/tls_crypt.c
    src/openvpn/tun.c
    src/plugins/down-root/down-root.c
    )

add_executable(openvpn ${openvpn_srcs})

target_include_directories(openvpn PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/src/compat
    ${CMAKE_SOURCE_DIR}/src/plugins/down-root
    ${CMAKE_SOURCE_DIR}/src/datacloak
    ${CMAKE_SOURCE_DIR}/src/openvpn
    )

target_link_libraries(openvpn PRIVATE
    resolv
    lzo2
    lz4
    ssl
    crypto
    dl
    )

target_compile_definitions(openvpn PRIVATE
    -DHAVE_CONFIG_H
    -DENABLE_CRYPTO_OPENSSL=1
    -DPLUGIN_LIBDIR="/usr/local/lib/openvpn/plugins"
    )

install (TARGETS openvpn DESTINATION bin)
