set(CHTTRANS_SOURCES
    chttrans.cpp chttrans-native.cpp
)
if (ENABLE_OPENCC)
    set(CHTTRANS_SOURCES ${CHTTRANS_SOURCES} chttrans-opencc.cpp)
endif()
add_library(chttrans MODULE ${CHTTRANS_SOURCES})
target_link_libraries(chttrans Fcitx5::Core Fcitx5::Config Fcitx5::Module::Notifications)
if (ENABLE_OPENCC)
    target_link_libraries(chttrans OpenCC::OpenCC)
endif()
set_target_properties(chttrans PROPERTIES PREFIX "")
install(TARGETS chttrans DESTINATION "${CMAKE_INSTALL_LIBDIR}/fcitx5")
install(FILES chttrans.conf DESTINATION "${CMAKE_INSTALL_DATADIR}/fcitx5/addon")
install(FILES gbks2t.tab DESTINATION "${CMAKE_INSTALL_DATADIR}/fcitx5/data")
