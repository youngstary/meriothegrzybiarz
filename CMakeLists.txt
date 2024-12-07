cmake_minimum_required(VERSION 3.10)
project(CrossPlatformGame)

# Ustaw standard C++
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Znajdź SFML (lub użyj lokalnej wersji)
set(SFML_DIR "${CMAKE_SOURCE_DIR}/external/SFML/cmake")
find_package(SFML 2.5 COMPONENTS system window graphics audio REQUIRED)

# Dodaj katalogi z plikami nagłówkowymi
include_directories(${CMAKE_SOURCE_DIR}/include)

# Zbierz pliki źródłowe
file(GLOB_RECURSE SOURCES "src/*.cpp")

# Stwórz główny plik wykonywalny
add_executable(CrossPlatformGame ${SOURCES})

# Połącz z biblioteką SFML
target_link_libraries(CrossPlatformGame sfml-system sfml-window sfml-graphics sfml-audio)

# Dodaj pliki assets do katalogu build po zbudowaniu
add_custom_command(TARGET CrossPlatformGame POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    "${CMAKE_SOURCE_DIR}/assets" "$<TARGET_FILE_DIR:CrossPlatformGame>/assets"
)

