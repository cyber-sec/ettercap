set(EC_TEXT_SRC
            text/ec_text.c
            text/ec_text_conn.c
            text/ec_text_display.c
            text/ec_text_plugin.c
            text/ec_text_profile.c
)
include_directories(text)

set(EC_DAEMON_SRC daemon/ec_daemon.c)

if(ENABLE_CURSES)
    set(EC_CURSES_SRC 
                curses/ec_curses.c
                curses/ec_curses_filters.c
                curses/ec_curses_help.c
                curses/ec_curses_hosts.c
                curses/ec_curses_live.c
                curses/ec_curses_logging.c
                curses/ec_curses_mitm.c
                curses/ec_curses_offline.c
                curses/ec_curses_plugins.c
                curses/ec_curses_start.c
                curses/ec_curses_targets.c
                curses/ec_curses_view.c
                curses/ec_curses_view_connections.c
                curses/ec_curses_view_profiles.c
    )
    include_directories(curses)
    set(EC_WDG_SRC
                curses/widgets/wdg.c
                curses/widgets/wdg_compound.c
                curses/widgets/wdg_debug.c
                curses/widgets/wdg_dialog.c
                curses/widgets/wdg_dynlist.c
                curses/widgets/wdg_error.c
                curses/widgets/wdg_file.c
                curses/widgets/wdg_input.c
                curses/widgets/wdg_list.c
                curses/widgets/wdg_menu.c
                curses/widgets/wdg_panel.c
                curses/widgets/wdg_percentage.c
                curses/widgets/wdg_scroll.c
                curses/widgets/wdg_window.c
    )
    include_directories(curses/widgets)
    add_library(ec_wdg STATIC ${EC_WDG_SRC})
    target_link_libraries(ec_wdg ${EC_LIBS})
endif(ENABLE_CURSES)

if(ENABLE_GTK)
    set(EC_GTK_SRC
                gtk/ec_gtk.c
                gtk/ec_gtk_conf.c
                gtk/ec_gtk_filters.c
                gtk/ec_gtk_help.c
                gtk/ec_gtk_hosts.c
                gtk/ec_gtk_live.c
                gtk/ec_gtk_logging.c
                gtk/ec_gtk_menus.c
                gtk/ec_gtk_mitm.c
                gtk/ec_gtk_offline.c
                gtk/ec_gtk_plugins.c
                gtk/ec_gtk_start.c
                gtk/ec_gtk_targets.c
                gtk/ec_gtk_view.c
                gtk/ec_gtk_view_connections.c
                gtk/ec_gtk_view_profiles.c
    )
    include_directories(gtk)
endif(ENABLE_GTK)


add_library(ec_interfaces STATIC ../ec_interfaces.c ${EC_TEXT_SRC} ${EC_DAEMON_SRC} ${EC_WDG_SRC} ${EC_CURSES_SRC} ${EC_GTK_SRC})
SET_TARGET_PROPERTIES(ec_interfaces PROPERTIES COMPILE_FLAGS -fPIC)
target_link_libraries(ec_interfaces ${EC_LIBS})
set_target_properties(ec_interfaces PROPERTIES 
  ENABLE_EXPORTS On
  LINK_INTERFACE_LIBRARIES ""
  #  INSTALL_RPATH ${INSTALL_LIBDIR}
  OUTPUT_NAME ec_interfaces 
  )

