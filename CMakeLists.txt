project(nginx)

SET(CORE_SRCS
	   src/core/nginx.c 
           src/core/ngx_log.c 
           src/core/ngx_palloc.c 
           src/core/ngx_array.c 
           src/core/ngx_list.c 
           src/core/ngx_hash.c 
           src/core/ngx_buf.c 
           src/core/ngx_queue.c 
           src/core/ngx_output_chain.c 
           src/core/ngx_string.c 
           src/core/ngx_parse.c 
           src/core/ngx_inet.c 
           src/core/ngx_file.c 
           src/core/ngx_crc32.c 
           src/core/ngx_murmurhash.c 
           src/core/ngx_md5.c 
           src/core/ngx_rbtree.c 
           src/core/ngx_trie.c
           src/core/ngx_segment_tree.c 
           src/core/ngx_radix_tree.c 
           src/core/ngx_slab.c 
           src/core/ngx_times.c 
           src/core/ngx_shmtx.c 
           src/core/ngx_connection.c 
           src/core/ngx_cycle.c 
           src/core/ngx_spinlock.c 
           src/core/ngx_cpuinfo.c 
           src/core/ngx_conf_file.c 
           src/core/ngx_resolver.c 
           src/core/ngx_open_file_cache.c 
           src/core/ngx_crypt.c 
           src/core/ngx_proxy_protocol.c 
           src/core/ngx_syslog.c
)

set(UNIX_SRCS
${CORE_SRCS} ${EVENT_SRCS}
	    src/os/unix/ngx_time.c 
            src/os/unix/ngx_errno.c 
            src/os/unix/ngx_alloc.c 
            src/os/unix/ngx_files.c 
            src/os/unix/ngx_socket.c 
            src/os/unix/ngx_recv.c 
            src/os/unix/ngx_readv_chain.c 
            src/os/unix/ngx_udp_recv.c 
            src/os/unix/ngx_send.c 
            src/os/unix/ngx_writev_chain.c 
            src/os/unix/ngx_channel.c 
            src/os/unix/ngx_shmem.c 
            src/os/unix/ngx_process.c 
            src/os/unix/ngx_daemon.c 
            src/os/unix/ngx_setproctitle.c 
            src/os/unix/ngx_posix_init.c 
            src/os/unix/ngx_user.c 
            src/os/unix/ngx_pipe.c 
            src/os/unix/ngx_sysinfo.c 
            src/os/unix/ngx_process_cycle.c
)

include_directories(
src/core
src/event 
src/event/modules
src/os/unix
src/proc
objs
)

add_library(libcore ${CORE_SRCS})
# Copyright (C) Igor Sysoev
# Copyright (C) Nginx, Inc.


set(CORE_MODULES ngx_core_module ngx_errlog_module ngx_conf_module)

set(CORE_INCS  src/core)

set(CORE_DEPS src/core/nginx.h 
           src/core/ngx_config.h 
           src/core/ngx_core.h 
           src/core/ngx_log.h 
           src/core/ngx_palloc.h 
           src/core/ngx_array.h 
           src/core/ngx_list.h 
           src/core/ngx_hash.h 
           src/core/ngx_buf.h 
           src/core/ngx_queue.h 
           src/core/ngx_string.h 
           src/core/ngx_parse.h 
           src/core/ngx_inet.h 
           src/core/ngx_file.h 
           src/core/ngx_crc.h 
           src/core/ngx_crc32.h 
           src/core/ngx_murmurhash.h 
           src/core/ngx_md5.h 
           src/core/ngx_sha1.h 
           src/core/ngx_rbtree.h 
           src/core/ngx_trie.h 
           src/core/ngx_segment_tree.h 
           src/core/ngx_radix_tree.h 
           src/core/ngx_slab.h 
           src/core/ngx_times.h 
           src/core/ngx_shmtx.h 
           src/core/ngx_connection.h 
           src/core/ngx_cycle.h 
           src/core/ngx_conf_file.h 
           src/core/ngx_resolver.h 
           src/core/ngx_open_file_cache.h 
           src/core/ngx_crypt.h 
           src/core/ngx_proxy_protocol.h 
           src/core/ngx_syslog.h
)


set(REGEX_MODULE ngx_regex_module)
set(REGEX_DEPS src/core/ngx_regex.h)
set(REGEX_SRCS src/core/ngx_regex.c)


set(DSO_MODULE ngx_dso_module)
set(DSO_SRCS src/core/ngx_dso_module.c)


set(OPENSSL_MODULE ngx_openssl_module)
set(OPENSSL_DEPS src/event/ngx_event_openssl.h)
set(OPENSSL_SRCS src/event/ngx_event_openssl.c 
              src/event/ngx_event_openssl_stapling.c
)


set(EVENT_MODULES ngx_events_module ngx_event_core_module)

#EVENT_INCS src/event src/event/modules)

set(EVENT_DEPS src/event/ngx_event.h 
            src/event/ngx_event_timer.h 
            src/event/ngx_event_posted.h 
            src/event/ngx_event_connect.h 
            src/event/ngx_event_pipe.h
)

set(EVENT_SRCS src/event/ngx_event.c 
            src/event/ngx_event_timer.c 
            src/event/ngx_event_posted.c 
            src/event/ngx_event_accept.c 
            src/event/ngx_event_connect.c 
            src/event/ngx_event_pipe.c
)


set(SELECT_SRCS src/event/modules/ngx_select_module.c)
set(WIN32_SELECT_SRCS src/event/modules/ngx_win32_select_module.c)

set(POLL_SRCS src/event/modules/ngx_poll_module.c)

set(KQUEUE_SRCS src/event/modules/ngx_kqueue_module.c)

set(DEVPOLL_SRCS src/event/modules/ngx_devpoll_module.c)

set(EVENTPORT_SRCS src/event/modules/ngx_eventport_module.c)

set(EPOLL_SRCS src/event/modules/ngx_epoll_module.c)

set(RTSIG_SRCS src/event/modules/ngx_rtsig_module.c)

set(IOCP_SRCS src/event/modules/ngx_iocp_module.c)


set(PROCS_DEPS src/proc/ngx_proc.h)
set(PROCS_INCS src/proc)
set(PROCS_SRCS src/proc/ngx_proc.c)


set(AIO_SRCS src/event/modules/ngx_aio_module.c 
          src/os/unix/ngx_aio_read.c 
          src/os/unix/ngx_aio_write.c 
          src/os/unix/ngx_aio_read_chain.c 
          src/os/unix/ngx_aio_write_chain.c)

set(FILE_AIO_SRCS src/os/unix/ngx_file_aio_read.c)
set(LINUX_AIO_SRCS src/os/unix/ngx_linux_aio_read.c)

set(PIPE_DEPS  src/os/unix/ngx_pipe.h)
set(PIPE_SRCS  src/os/unix/ngx_pipe.c)

set(UNIX_INCS ${CORE_INCS} ${EVENT_INCS} src/os/unix)

set(UNIX_DEPS ${CORE_DEPS} ${EVENT_DEPS}
            src/os/unix/ngx_time.h 
            src/os/unix/ngx_errno.h 
            src/os/unix/ngx_alloc.h 
            src/os/unix/ngx_files.h 
            src/os/unix/ngx_channel.h 
            src/os/unix/ngx_shmem.h 
            src/os/unix/ngx_process.h 
            src/os/unix/ngx_setaffinity.h 
            src/os/unix/ngx_setproctitle.h 
            src/os/unix/ngx_atomic.h 
            src/os/unix/ngx_gcc_atomic_x86.h 
            src/os/unix/ngx_thread.h 
            src/os/unix/ngx_socket.h 
            src/os/unix/ngx_os.h 
            src/os/unix/ngx_user.h 
            src/os/unix/ngx_pipe.h 
            src/os/unix/ngx_sysinfo.h 
            src/os/unix/ngx_process_cycle.h
)

# add to UNIX_DEPS
#            src/os/unix/ngx_gcc_atomic_amd64.h 
#            src/os/unix/ngx_gcc_atomic_sparc64.h 
#            src/os/unix/ngx_gcc_atomic_ppc.h 
#            src/os/unix/ngx_sunpro_atomic_sparc64.h 
#            src/os/unix/ngx_sunpro_x86.il 
#            src/os/unix/ngx_sunpro_amd64.il 
#            src/os/unix/ngx_sunpro_sparc64.il 


set(UNIX_SRCS ${CORE_SRCS} ${EVENT_SRCS} 
            src/os/unix/ngx_time.c 
            src/os/unix/ngx_errno.c 
            src/os/unix/ngx_alloc.c 
            src/os/unix/ngx_files.c 
            src/os/unix/ngx_socket.c 
            src/os/unix/ngx_recv.c 
            src/os/unix/ngx_readv_chain.c 
            src/os/unix/ngx_udp_recv.c 
            src/os/unix/ngx_send.c 
            src/os/unix/ngx_writev_chain.c 
            src/os/unix/ngx_channel.c 
            src/os/unix/ngx_shmem.c 
            src/os/unix/ngx_process.c 
            src/os/unix/ngx_daemon.c 
            src/os/unix/ngx_setproctitle.c 
            src/os/unix/ngx_posix_init.c 
            src/os/unix/ngx_user.c 
            src/os/unix/ngx_pipe.c 
            src/os/unix/ngx_sysinfo.c 
            src/os/unix/ngx_process_cycle.c
    )

set(POSIX_DEPS src/os/unix/ngx_posix_config.h)


set(THREAD_POOL_DEPS src/core/ngx_thread_pool.h)
set(THREAD_POOL_SRCS src/core/ngx_thread_pool.c
                  src/os/unix/ngx_thread_cond.c
                  src/os/unix/ngx_thread_mutex.c
                  src/os/unix/ngx_thread_id.c)

set(FREEBSD_DEPS src/os/unix/ngx_freebsd_config.h src/os/unix/ngx_freebsd.h)
set(FREEBSD_SRCS src/os/unix/ngx_freebsd_init.c)
set(FREEBSD_SENDFILE_SRCS src/os/unix/ngx_freebsd_sendfile_chain.c)

set(LINUX_DEPS src/os/unix/ngx_linux_config.h src/os/unix/ngx_linux.h)
set(LINUX_SRCS src/os/unix/ngx_linux_init.c)
set(LINUX_SENDFILE_SRCS src/os/unix/ngx_linux_sendfile_chain.c)


set(SOLARIS_DEPS src/os/unix/ngx_solaris_config.h src/os/unix/ngx_solaris.h)
set(SOLARIS_SRCS src/os/unix/ngx_solaris_init.c)
set(SOLARIS_SENDFILEV_SRCS src/os/unix/ngx_solaris_sendfilev_chain.c)


set(DARWIN_DEPS src/os/unix/ngx_darwin_config.h src/os/unix/ngx_darwin.h)
set(DARWIN_SRCS src/os/unix/ngx_darwin_init.c)
set(DARWIN_SENDFILE_SRCS src/os/unix/ngx_darwin_sendfile_chain.c)


set(WIN32_INCS ${CORE_INCS} ${EVENT_INCS} src/os/win32)

set(WIN32_DEPS ${CORE_DEPS} ${EVENT_DEPS} 
            src/os/win32/ngx_win32_config.h 
            src/os/win32/ngx_time.h 
            src/os/win32/ngx_errno.h 
            src/os/win32/ngx_alloc.h 
            src/os/win32/ngx_files.h 
            src/os/win32/ngx_shmem.h 
            src/os/win32/ngx_process.h 
            src/os/win32/ngx_atomic.h 
            src/os/win32/ngx_thread.h 
            src/os/win32/ngx_socket.h 
            src/os/win32/ngx_os.h 
            src/os/win32/ngx_user.h 
            src/os/win32/ngx_process_cycle.h)

set(WIN32_CONFIG src/os/win32/ngx_win32_config.h)

set(WIN32_SRCS ${CORE_SRCS} ${EVENT_SRCS} 
            src/os/win32/ngx_errno.c 
            src/os/win32/ngx_alloc.c 
            src/os/win32/ngx_files.c 
            src/os/win32/ngx_shmem.c 
            src/os/win32/ngx_time.c 
            src/os/win32/ngx_process.c 
            src/os/win32/ngx_thread.c 
            src/os/win32/ngx_socket.c 
            src/os/win32/ngx_wsarecv.c 
            src/os/win32/ngx_wsarecv_chain.c 
            src/os/win32/ngx_udp_wsarecv.c 
            src/os/win32/ngx_wsasend.c 
            src/os/win32/ngx_wsasend_chain.c 
            src/os/win32/ngx_win32_init.c 
            src/os/win32/ngx_user.c 
            src/os/win32/ngx_event_log.c 
            src/os/win32/ngx_process_cycle.c 
            src/event/ngx_event_acceptex.c)

set(NGX_WIN32_ICONS src/os/win32/nginx.ico)
set(NGX_WIN32_RC src/os/win32/nginx.rc)


# the http modules that have their logging formats
# must be after ngx_http_log_module

set(HTTP_MODULES ngx_http_module 
              ngx_http_core_module 
              ngx_http_log_module 
              ngx_http_upstream_module)

set(HTTP_WRITE_FILTER_MODULE ngx_http_write_filter_module)
set(HTTP_HEADER_FILTER_MODULE ngx_http_header_filter_module)

set(HTTP_POSTPONE_FILTER_MODULE ngx_http_postpone_filter_module)
set(HTTP_COPY_FILTER_MODULE ngx_http_copy_filter_module)

set(HTTP_CHUNKED_FILTER_MODULE ngx_http_chunked_filter_module)
set(HTTP_HEADERS_FILTER_MODULE ngx_http_headers_filter_module)

set(HTTP_RANGE_HEADER_FILTER_MODULE ngx_http_range_header_filter_module)
set(HTTP_RANGE_BODY_FILTER_MODULE ngx_http_range_body_filter_module)

set(HTTP_NOT_MODIFIED_FILTER_MODULE ngx_http_not_modified_filter_module)

set(HTTP_STATIC_MODULE ngx_http_static_module)
set(HTTP_INDEX_MODULE ngx_http_index_module)

set(HTTP_INCS src/http src/http/modules)

set(HTTP_DEPS src/http/ngx_http.h 
           src/http/ngx_http_request.h 
           src/http/ngx_http_config.h 
           src/http/ngx_http_core_module.h 
           src/http/ngx_http_cache.h 
           src/http/ngx_http_variables.h 
           src/http/ngx_http_script.h 
           src/http/ngx_http_upstream.h 
           src/http/ngx_http_upstream_round_robin.h)

set(HTTP_SRCS src/http/ngx_http.c 
           src/http/ngx_http_core_module.c 
           src/http/ngx_http_special_response.c 
           src/http/ngx_http_request.c 
           src/http/ngx_http_parse.c 
           src/http/ngx_http_header_filter_module.c 
           src/http/ngx_http_write_filter_module.c 
           src/http/ngx_http_copy_filter_module.c 
           src/http/modules/ngx_http_log_module.c 
           src/http/ngx_http_request_body.c 
           src/http/ngx_http_variables.c 
           src/http/ngx_http_script.c 
           src/http/ngx_http_upstream.c 
           src/http/ngx_http_upstream_round_robin.c 
           src/http/ngx_http_parse_time.c 
           src/http/modules/ngx_http_static_module.c 
           src/http/modules/ngx_http_index_module.c 
           src/http/modules/ngx_http_chunked_filter_module.c 
           src/http/modules/ngx_http_range_filter_module.c 
           src/http/modules/ngx_http_headers_filter_module.c 
           src/http/modules/ngx_http_not_modified_filter_module.c)

# STUB
set(HTTP_POSTPONE_FILTER_SRCS src/http/ngx_http_postpone_filter_module.c)

set(HTTP_FILE_CACHE_SRCS src/http/ngx_http_file_cache.c)


set(HTTP_V2_MODULE ngx_http_v2_module)
set(HTTP_V2_FILTER_MODULE ngx_http_v2_filter_module)
set(HTTP_V2_INCS src/http/v2)
set(HTTP_V2_DEPS src/http/v2/ngx_http_v2.h 
              src/http/v2/ngx_http_v2_module.h)
set(HTTP_V2_SRCS src/http/v2/ngx_http_v2.c 
              src/http/v2/ngx_http_v2_table.c 
              src/http/v2/ngx_http_v2_huff_decode.c 
              src/http/v2/ngx_http_v2_huff_encode.c 
              src/http/v2/ngx_http_v2_module.c 
              src/http/v2/ngx_http_v2_filter_module.c)


set(HTTP_CHARSET_FILTER_MODULE ngx_http_charset_filter_module)
set(HTTP_CHARSET_SRCS src/http/modules/ngx_http_charset_filter_module.c)


set(HTTP_GZIP_FILTER_MODULE ngx_http_gzip_filter_module)
set(HTTP_GZIP_SRCS src/http/modules/ngx_http_gzip_filter_module.c)


set(HTTP_GUNZIP_FILTER_MODULE ngx_http_gunzip_filter_module)
set(HTTP_GUNZIP_SRCS src/http/modules/ngx_http_gunzip_filter_module.c)


set(HTTP_SSI_FILTER_MODULE ngx_http_ssi_filter_module)
set(HTTP_SSI_DEPS src/http/modules/ngx_http_ssi_filter_module.h)
set(HTTP_SSI_SRCS src/http/modules/ngx_http_ssi_filter_module.c)


set(HTTP_XSLT_FILTER_MODULE ngx_http_xslt_filter_module)
set(HTTP_XSLT_SRCS src/http/modules/ngx_http_xslt_filter_module.c)


set(HTTP_IMAGE_FILTER_MODULE ngx_http_image_filter_module)
set(HTTP_IMAGE_SRCS src/http/modules/ngx_http_image_filter_module.c)


set(HTTP_SUB_FILTER_MODULE ngx_http_sub_filter_module)
set(HTTP_SUB_SRCS src/http/modules/ngx_http_sub_filter_module.c)


set(HTTP_USERID_FILTER_MODULE ngx_http_userid_filter_module)
set(HTTP_USERID_SRCS src/http/modules/ngx_http_userid_filter_module.c)


set(HTTP_REALIP_MODULE ngx_http_realip_module)
set(HTTP_REALIP_SRCS src/http/modules/ngx_http_realip_module.c)


set(HTTP_ADDITION_FILTER_MODULE ngx_http_addition_filter_module)
set(HTTP_ADDITION_SRCS src/http/modules/ngx_http_addition_filter_module.c)

set(HTTP_FOOTER_FILTER_MODULE ngx_http_footer_filter_module)
set(HTTP_FOOTER_FILTER_SRCS src/http/modules/ngx_http_footer_filter_module.c)

set(HTTP_TRIM_FILTER_MODULE ngx_http_trim_filter_module)
set(HTTP_TRIM_FILTER_SRCS src/http/modules/ngx_http_trim_filter_module.c)

set(HTTP_DAV_MODULE ngx_http_dav_module)
set(HTTP_DAV_SRCS src/http/modules/ngx_http_dav_module.c)


set(HTTP_ACCESS_MODULE ngx_http_access_module)
set(HTTP_ACCESS_SRCS src/http/modules/ngx_http_access_module.c)


set(HTTP_AUTH_BASIC_MODULE ngx_http_auth_basic_module)
set(HTTP_AUTH_BASIC_SRCS src/http/modules/ngx_http_auth_basic_module.c)


set(HTTP_CONCAT_MODULE ngx_http_concat_module)
set(HTTP_CONCAT_SRCS src/http/modules/ngx_http_concat_module.c)


set(HTTP_AUTH_REQUEST_MODULE ngx_http_auth_request_module)
set(HTTP_AUTH_REQUEST_SRCS src/http/modules/ngx_http_auth_request_module.c)


set(HTTP_AUTOINDEX_MODULE ngx_http_autoindex_module)
set(HTTP_AUTOINDEX_SRCS src/http/modules/ngx_http_autoindex_module.c)


set(HTTP_RANDOM_INDEX_MODULE ngx_http_random_index_module)
set(HTTP_RANDOM_INDEX_SRCS src/http/modules/ngx_http_random_index_module.c)


set(HTTP_STATUS_MODULE ngx_http_status_module)
set(HTTP_STATUS_SRCS src/http/modules/ngx_http_status_module.c)


set(HTTP_GEO_MODULE ngx_http_geo_module)
set(HTTP_GEO_SRCS src/http/modules/ngx_http_geo_module.c)


set(HTTP_GEOIP_MODULE ngx_http_geoip_module)
set(HTTP_GEOIP_SRCS src/http/modules/ngx_http_geoip_module.c)


set(HTTP_MAP_MODULE ngx_http_map_module)
set(HTTP_MAP_SRCS src/http/modules/ngx_http_map_module.c)


set(HTTP_SPLIT_CLIENTS_MODULE ngx_http_split_clients_module)
set(HTTP_SPLIT_CLIENTS_SRCS src/http/modules/ngx_http_split_clients_module.c)


set(HTTP_REFERER_MODULE ngx_http_referer_module)
set(HTTP_REFERER_SRCS src/http/modules/ngx_http_referer_module.c)


set(HTTP_REWRITE_MODULE ngx_http_rewrite_module)
set(HTTP_REWRITE_SRCS src/http/modules/ngx_http_rewrite_module.c)


set(HTTP_SSL_MODULE ngx_http_ssl_module)
set(HTTP_SSL_DEPS src/http/modules/ngx_http_ssl_module.h)
set(HTTP_SSL_SRCS src/http/modules/ngx_http_ssl_module.c)


set(HTTP_PROXY_MODULE ngx_http_proxy_module)
set(HTTP_PROXY_SRCS src/http/modules/ngx_http_proxy_module.c)


set(HTTP_FASTCGI_MODULE ngx_http_fastcgi_module)
set(HTTP_FASTCGI_SRCS src/http/modules/ngx_http_fastcgi_module.c)


set(HTTP_UWSGI_MODULE ngx_http_uwsgi_module)
set(HTTP_UWSGI_SRCS src/http/modules/ngx_http_uwsgi_module.c)


set(HTTP_SCGI_MODULE ngx_http_scgi_module)
set(HTTP_SCGI_SRCS src/http/modules/ngx_http_scgi_module.c)


set(HTTP_PERL_MODULE ngx_http_perl_module)
set(HTTP_PERL_INCS src/http/modules/perl)
set(HTTP_PERL_DEPS src/http/modules/perl/ngx_http_perl_module.h)
set(HTTP_PERL_SRCS src/http/modules/perl/ngx_http_perl_module.c)


set(HTTP_MEMCACHED_MODULE ngx_http_memcached_module)
set(HTTP_MEMCACHED_SRCS src/http/modules/ngx_http_memcached_module.c)


set(HTTP_LIMIT_CONN_MODULE ngx_http_limit_conn_module)
set(HTTP_LIMIT_CONN_SRCS src/http/modules/ngx_http_limit_conn_module.c)


set(HTTP_LIMIT_REQ_MODULE ngx_http_limit_req_module)
set(HTTP_LIMIT_REQ_SRCS src/http/modules/ngx_http_limit_req_module.c)


set(HTTP_EMPTY_GIF_MODULE ngx_http_empty_gif_module)
set(HTTP_EMPTY_GIF_SRCS src/http/modules/ngx_http_empty_gif_module.c)


set(HTTP_BROWSER_MODULE ngx_http_browser_module)
set(HTTP_BROWSER_SRCS src/http/modules/ngx_http_browser_module.c)


set(HTTP_USER_AGENT_MODULE ngx_http_user_agent_module)
set(HTTP_USER_AGENT_SRCS src/http/modules/ngx_http_user_agent_module.c)


set(HTTP_SECURE_LINK_MODULE ngx_http_secure_link_module)
set(HTTP_SECURE_LINK_SRCS src/http/modules/ngx_http_secure_link_module.c)


set(HTTP_DEGRADATION_MODULE ngx_http_degradation_module)
set(HTTP_DEGRADATION_SRCS src/http/modules/ngx_http_degradation_module.c)


set(HTTP_SYSGUARD_MODULE ngx_http_sysguard_module)
set(HTTP_SYSGUARD_SRCS src/http/modules/ngx_http_sysguard_module.c)


set(HTTP_FLV_MODULE ngx_http_flv_module)
set(HTTP_FLV_SRCS src/http/modules/ngx_http_flv_module.c)


set(HTTP_SLICE_MODULE ngx_http_slice_module)
set(HTTP_SLICE_SRCS src/http/modules/ngx_http_slice_module.c)


set(HTTP_MP4_MODULE ngx_http_mp4_module)
set(HTTP_MP4_SRCS src/http/modules/ngx_http_mp4_module.c)


set(HTTP_GZIP_STATIC_MODULE ngx_http_gzip_static_module)
set(HTTP_GZIP_STATIC_SRCS src/http/modules/ngx_http_gzip_static_module.c)


set(HTTP_UPSTREAM_HASH_MODULE ngx_http_upstream_hash_module)
set(HTTP_UPSTREAM_HASH_SRCS src/http/modules/ngx_http_upstream_hash_module.c)


set(HTTP_UPSTREAM_IP_HASH_MODULE ngx_http_upstream_ip_hash_module)
set(HTTP_UPSTREAM_IP_HASH_SRCS src/http/modules/ngx_http_upstream_ip_hash_module.c)


set(HTTP_UPSTREAM_CHECK_MODULE ngx_http_upstream_check_module)
set(HTTP_UPSTREAM_CHECK_SRCS src/http/ngx_http_upstream_check_module.c)


set(HTTP_UPSTREAM_CONSISTENT_HASH_MODULE ngx_http_upstream_consistent_hash_module)
set(HTTP_UPSTREAM_CONSISTENT_HASH_SRCS src/http/modules/ngx_http_upstream_consistent_hash_module.c)


set(HTTP_UPSTREAM_LEAST_CONN_MODULE ngx_http_upstream_least_conn_module)
set(HTTP_UPSTREAM_LEAST_CONN_SRCS src/http/modules/ngx_http_upstream_least_conn_module.c)


set(HTTP_UPSTREAM_SESSION_STICKY_MODULE ngx_http_upstream_session_sticky_module)
set(HTTP_UPSTREAM_SESSION_STICKY_SRCS src/http/modules/ngx_http_upstream_session_sticky_module.c)


set(HTTP_UPSTREAM_KEEPALIVE_MODULE ngx_http_upstream_keepalive_module)
set(HTTP_UPSTREAM_KEEPALIVE_SRCS src/http/modules/ngx_http_upstream_keepalive_module.c)

set(HTTP_UPSTREAM_DYNAMIC_MODULE ngx_http_upstream_dynamic_module)
set(HTTP_UPSTREAM_DYNAMIC_SRCS src/http/modules/ngx_http_upstream_dynamic_module.c)

set(HTTP_DYUPS_MODULE ngx_http_dyups_module)
set(HTTP_DYUPS_SRCS src/http/modules/ngx_http_dyups_module.c)
set(HTTP_DYUPS_DEPS src/http/modules/ngx_http_dyups.h)
set(HTTP_DYUPS_LUA_SRCS src/http/modules/ngx_http_dyups_lua.c)
set(HTTP_DYUPS_LUA_DEPS src/http/modules/ngx_http_dyups_lua.h)


set(HTTP_REQ_STATUS_MODULE ngx_http_reqstat_module)
set(HTTP_REQ_STATUS_SRCS src/http/modules/ngx_http_reqstat_module.c)
set(HTTP_REQ_STATUS_DEPS src/http/modules/ngx_http_reqstat.h)


set(MAIL_INCS src/mail)

set(MAIL_DEPS src/mail/ngx_mail.h)

set(MAIL_MODULES ngx_mail_module ngx_mail_core_module)

set(MAIL_SRCS src/mail/ngx_mail.c 
           src/mail/ngx_mail_core_module.c 
           src/mail/ngx_mail_handler.c 
           src/mail/ngx_mail_parse.c)

set(MAIL_POP3_MODULE ngx_mail_pop3_module)
set(MAIL_POP3_DEPS src/mail/ngx_mail_pop3_module.h)
set(MAIL_POP3_SRCS src/mail/ngx_mail_pop3_module.c 
                src/mail/ngx_mail_pop3_handler.c)

set(MAIL_IMAP_MODULE ngx_mail_imap_module)
set(MAIL_IMAP_DEPS src/mail/ngx_mail_imap_module.h)
set(MAIL_IMAP_SRCS src/mail/ngx_mail_imap_module.c 
                src/mail/ngx_mail_imap_handler.c)

set(MAIL_SMTP_MODULE ngx_mail_smtp_module)
set(MAIL_SMTP_DEPS src/mail/ngx_mail_smtp_module.h)
set(MAIL_SMTP_SRCS src/mail/ngx_mail_smtp_module.c 
                src/mail/ngx_mail_smtp_handler.c)

set(MAIL_SSL_MODULE ngx_mail_ssl_module)
set(MAIL_SSL_DEPS src/mail/ngx_mail_ssl_module.h)
set(MAIL_SSL_SRCS src/mail/ngx_mail_ssl_module.c)

set(MAIL_AUTH_HTTP_MODULE ngx_mail_auth_http_module)
set(MAIL_AUTH_HTTP_SRCS src/mail/ngx_mail_auth_http_module.c)

set(MAIL_PROXY_MODULE ngx_mail_proxy_module)
set(MAIL_PROXY_SRCS src/mail/ngx_mail_proxy_module.c)

set(NGX_GOOGLE_PERFTOOLS_MODULE ngx_google_perftools_module)
set(NGX_GOOGLE_PERFTOOLS_SRCS src/misc/ngx_google_perftools_module.c)

set(NGX_CPP_TEST_SRCS src/misc/ngx_cpp_test_module.cpp)

set(NGX_BACKTRACE_MODULE ngx_backtrace_module)
set(NGX_BACKTRACE_SRCS src/misc/ngx_backtrace_module.c)

set(NGX_HTTP_LUA_MODULE ngx_http_lua_module)
set(NGX_HTTP_LUA_MODULE_SRCS modules/ngx_http_lua_module/src/ngx_http_lua_script.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_log.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_subrequest.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_ndk.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_control.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_time.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_misc.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_variable.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_string.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_output.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headers.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_req_body.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_uri.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_args.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_ctx.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_regex.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_module.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headers_out.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headers_in.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_directive.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_consts.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_exception.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_util.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_cache.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_contentby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_rewriteby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_accessby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_setby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_capturefilter.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_clfactory.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_pcrefix.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headerfilterby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_shdict.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_socket_tcp.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_api.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_logby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_sleep.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_coroutine.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_bodyfilterby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_initby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_initworkerby.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_socket_udp.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_req_method.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_phase.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_uthread.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_timer.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_config.c 
                          modules/ngx_http_lua_module/src/ngx_http_lua_worker.c)


set(NGX_HTTP_LUA_MODULE_DEPS  modules/ngx_http_lua_module/src/ddebug.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_script.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_log.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_subrequest.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_ndk.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_control.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_time.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_string.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_misc.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_variable.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_output.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headers.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_uri.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_req_body.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_args.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_ctx.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_regex.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_common.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_directive.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headers_out.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headers_in.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_consts.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_exception.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_util.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_cache.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_contentby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_rewriteby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_accessby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_setby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_capturefilter.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_clfactory.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_pcrefix.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_headerfilterby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_shdict.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_socket_tcp.h 
                          modules/ngx_http_lua_module/src/api/ngx_http_lua_api.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_logby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_sleep.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_coroutine.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_bodyfilterby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_initby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_initworkerby.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_socket_udp.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_req_method.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_phase.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_probe.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_uthread.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_timer.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_config.h 
                          modules/ngx_http_lua_module/src/ngx_http_lua_worker.h)


set(NGX_HTTP_TFS_MODULE ngx_http_tfs_module)
set(
NGX_HTTP_TFS_MODULE_DEPS
			  src/http/modules/tfs/ngx_http_tfs.h 
                          src/http/modules/tfs/ngx_http_tfs_errno.h 
                          src/http/modules/tfs/ngx_tfs_common.h 
                          src/http/modules/tfs/ngx_http_tfs_restful.h 
                          src/http/modules/tfs/ngx_http_tfs_restful.h 
                          src/http/modules/tfs/ngx_http_tfs_protocol.h 
                          src/http/modules/tfs/ngx_http_tfs_serialization.h 
                          src/http/modules/tfs/ngx_http_connection_pool.h 
                          src/http/modules/tfs/ngx_http_tfs_json.h 
                          src/http/modules/tfs/ngx_http_tfs_rc_server_info.h 
                          src/http/modules/tfs/ngx_http_tfs_raw_fsname.h 
                          src/http/modules/tfs/ngx_http_tfs_tair_helper.h 
                          src/http/modules/tfs/ngx_http_tfs_duplicate.h 
                          src/http/modules/tfs/ngx_http_tfs_block_cache.h 
                          src/http/modules/tfs/ngx_http_tfs_local_block_cache.h 
                          src/http/modules/tfs/ngx_http_tfs_remote_block_cache.h 
                          src/http/modules/tfs/ngx_http_tfs_timers.h 
                          src/http/modules/tfs/ngx_http_tfs_rc_server_message.h 
                          src/http/modules/tfs/ngx_http_tfs_name_server_message.h 
                          src/http/modules/tfs/ngx_http_tfs_data_server_message.h 
                          src/http/modules/tfs/ngx_http_tfs_root_server_message.h 
                          src/http/modules/tfs/ngx_http_tfs_meta_server_message.h 
                          src/http/modules/tfs/ngx_http_tfs_peer_connection.h 
                          src/http/modules/tfs/ngx_http_tfs_server_handler.h 
)


set(
NGX_HTTP_TFS_MODULE_SRCS
			  src/http/modules/tfs/ngx_tfs_common.c 
                          src/http/modules/tfs/ngx_http_tfs.c 
                          src/http/modules/tfs/ngx_http_tfs_module.c 
                          src/http/modules/tfs/ngx_http_tfs_restful.c 
                          src/http/modules/tfs/ngx_http_tfs_serialization.c 
                          src/http/modules/tfs/ngx_http_connection_pool.c 
                          src/http/modules/tfs/ngx_http_tfs_json.c 
                          src/http/modules/tfs/ngx_http_tfs_rc_server_info.c 
                          src/http/modules/tfs/ngx_http_tfs_raw_fsname.c 
                          src/http/modules/tfs/ngx_http_tfs_tair_helper.c 
                          src/http/modules/tfs/ngx_http_tfs_duplicate.c 
                          src/http/modules/tfs/ngx_http_tfs_block_cache.c 
                          src/http/modules/tfs/ngx_http_tfs_local_block_cache.c 
                          src/http/modules/tfs/ngx_http_tfs_remote_block_cache.c 
                          src/http/modules/tfs/ngx_http_tfs_timers.c 
                          src/http/modules/tfs/ngx_http_tfs_rc_server_message.c 
                          src/http/modules/tfs/ngx_http_tfs_name_server_message.c 
                          src/http/modules/tfs/ngx_http_tfs_data_server_message.c 
                          src/http/modules/tfs/ngx_http_tfs_root_server_message.c 
                          src/http/modules/tfs/ngx_http_tfs_meta_server_message.c 
                          src/http/modules/tfs/ngx_http_tfs_peer_connection.c 
                          src/http/modules/tfs/ngx_http_tfs_server_handler.c 
)

