# Example 1

Aşağıda örnek bir `CMakeLists.txt` dosyası açıklamaları ile birlikte gösterilmektedir.

~~~CMake

    # Minimum gereken CMake sürümü belirtilir.
    cmake_minimum_required(VERSION 3.24)

    # Proje adı belirtilir.
    project(QStackedWidget)

    # C++ standart sürümü belirtilir.
    set(CMAKE_CXX_STANDARD 17)

    # Otomatik oluşturulacak dosyaların türleri belirtilir.
    set(CMAKE_AUTOMOC ON)
    set(CMAKE_AUTORCC ON)
    set(CMAKE_AUTOUIC ON)

    # İçerik dizinine göre dosya araması yapılmasını sağlar.
    set(CMAKE_INCLUDE_CURRENT_DIR ON)

    # .o uzantılı dosyaların kaydedileceği dizin belirtilir.
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "../include")
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "../include")
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "../include")

    # Qt kurulu olduğu dizin belirtilir.
    set(CMAKE_PREFIX_PATH "C:/Qt/6.4.1/mingw_64/lib/cmake")

    # Qt kütüphaneleri aranır ve bulunur.
    find_package(Qt6 COMPONENTS
            Core
            Gui
            Widgets
            REQUIRED)
    # main.cpp, Page.cpp ve Page.h dosyalarının birleştirilerek bir çalıştırılabilir dosya oluşturulur.
    add_executable(QStackedWidget main.cpp Page.cpp Page.h)

    # Oluşturulan çalıştırılabilir dosyaya gerekli bağımlıklar eklenir.
    target_link_libraries(QStackedWidget
            Qt::Core
            Qt::Gui
            Qt::Widgets
            )
    
    # Eğer proje Windows platformunda çalıştırılıyorsa, gerekli Qt dll dosyalarını proje dizinine kopyalar
    if (WIN32)
        set(DEBUG_SUFFIX)
        if (MSVC AND CMAKE_BUILD_TYPE MATCHES "Debug")
            set(DEBUG_SUFFIX "d")
        endif ()
        set(QT_INSTALL_PATH "${CMAKE_PREFIX_PATH}")
        if (NOT EXISTS "${QT_INSTALL_PATH}/bin")
            set(QT_INSTALL_PATH "${QT_INSTALL_PATH}/..")
            if (NOT EXISTS "${QT_INSTALL_PATH}/bin")
                set(QT_INSTALL_PATH "${QT_INSTALL_PATH}/..")
            endif ()
        endif ()
        if (EXISTS "${QT_INSTALL_PATH}/plugins/platforms/qwindows${DEBUG_SUFFIX}.dll")
            add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
                    COMMAND ${CMAKE_COMMAND} -E make_directory
                    "$<TARGET_FILE_DIR:${PROJECT_NAME}>/plugins/platforms/")
            add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
                    COMMAND ${CMAKE_COMMAND} -E copy
                    "${QT_INSTALL_PATH}/plugins/platforms/qwindows${DEBUG_SUFFIX}.dll"
                    "$<TARGET_FILE_DIR:${PROJECT_NAME}>/plugins/platforms/")
        endif ()
        foreach (QT_LIB Core Gui Widgets)
            add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
                    COMMAND ${CMAKE_COMMAND} -E copy
                    "${QT_INSTALL_PATH}/bin/Qt6${QT_LIB}${DEBUG_SUFFIX}.dll"
                    "$<TARGET_FILE_DIR:${PROJECT_NAME}>")
        endforeach (QT_LIB)
    endif ()

~~~
