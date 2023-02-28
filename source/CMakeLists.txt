add_library( freertos_plus_tcp STATIC )

target_sources( freertos_plus_tcp
  PRIVATE
      include/FreeRTOS_ARP.h
      include/FreeRTOS_DHCP.h
      include/FreeRTOS_DNS_Cache.h
      include/FreeRTOS_DNS_Callback.h
      include/FreeRTOS_DNS_Globals.h
      include/FreeRTOS_DNS_Networking.h
      include/FreeRTOS_DNS_Parser.h
      include/FreeRTOS_DNS.h
      include/FreeRTOS_errno_TCP.h
      include/FreeRTOS_ICMP.h
      include/FreeRTOS_IP_Private.h
      include/FreeRTOS_IP_Timers.h
      include/FreeRTOS_IP_Utils.h
      include/FreeRTOS_IP.h
      include/FreeRTOS_Sockets.h
      include/FreeRTOS_Stream_Buffer.h
      include/FreeRTOS_TCP_IP.h
      include/FreeRTOS_TCP_Reception.h
      include/FreeRTOS_TCP_State_Handling.h
      include/FreeRTOS_TCP_Transmission.h
      include/FreeRTOS_TCP_Utils.h
      include/FreeRTOS_TCP_WIN.h
      include/FreeRTOS_UDP_IP.h
      include/FreeRTOSIPConfigDefaults.h
      include/IPTraceMacroDefaults.h
      include/NetworkBufferManagement.h
      include/NetworkInterface.h

      FreeRTOS_ARP.c
      FreeRTOS_DHCP.c
      FreeRTOS_DNS_Cache.c
      FreeRTOS_DNS_Callback.c
      FreeRTOS_DNS_Networking.c
      FreeRTOS_DNS_Parser.c
      FreeRTOS_DNS.c
      FreeRTOS_ICMP.c
      FreeRTOS_IP_Timers.c
      FreeRTOS_IP_Utils.c
      FreeRTOS_IP.c
      FreeRTOS_Sockets.c
      FreeRTOS_Stream_Buffer.c
      FreeRTOS_TCP_IP.c
      FreeRTOS_TCP_Reception.c
      FreeRTOS_TCP_State_Handling.c
      FreeRTOS_TCP_Transmission.c
      FreeRTOS_TCP_Utils.c
      FreeRTOS_TCP_WIN.c
      FreeRTOS_Tiny_TCP.c
      FreeRTOS_UDP_IP.c
)

# Note: Have to make system due to compiler warnings in header files.
target_include_directories( freertos_plus_tcp SYSTEM
  PUBLIC
    include
)

#TODO(phelter): Investigate and fix in freertos_plus_tcp if not already fixed.
target_compile_options( freertos_plus_tcp
  PRIVATE
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-bad-function-cast>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-cast-qual>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-conditional-uninitialized>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-covered-switch-default>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-documentation>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-extra-semi-stmt>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-implicit-int-conversion>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-missing-noreturn>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-reserved-identifier>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-shorten-64-to-32>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-sign-conversion>
    $<$<COMPILE_LANG_AND_ID:C,Clang>:-Wno-unused-macros>
    $<$<COMPILE_LANG_AND_ID:C,GNU>:-Wno-unused-but-set-variable>
    $<$<COMPILE_LANG_AND_ID:C,Clang,GNU>:-Wno-unused-parameter>
    $<$<COMPILE_LANG_AND_ID:C,GNU>:-Wno-unused-variable>
    $<$<COMPILE_LANG_AND_ID:C,GNU>:-Wno-pedantic>
)

target_link_libraries( freertos_plus_tcp
  PUBLIC
    freertos_config
    freertos_plus_tcp_port # for pack_struct_start.h
  PRIVATE
    freertos_kernel
    freertos_plus_tcp_network_if
    freertos_plus_tcp_utilities
)

add_subdirectory(portable)