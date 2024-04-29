include_guard(GLOBAL)
cmake_minimum_required(VERSION 3.19 FATAL_ERROR)
include(FetchContent)
project("thezhe/content_lock")
# Fetch content using `content.lock`
#[[
`content.lock` format:
    <git-url-0>@<hash-0>
    <git-url-1>@<hash-1>
    ...
    <git-url-N>@<hash-N>
]]
function(thezhe_content_lock)
    set(filename "content.lock")
    # Reconfigure on change
    configure_file("${filename}" "_${filename}" COPYONLY)
    file(STRINGS "${filename}" entries)
    foreach(entry IN LISTS entries)
        string(REGEX REPLACE "@" ";" entry_tokens "${entry}")
        list(GET entry_tokens 0 entry_url)
        list(GET entry_tokens 1 entry_hash)
        cmake_path(GET entry_url STEM LAST_ONLY entry_repo_name)
        FetchContent_Declare(
            "${entry_repo_name}"
            GIT_REPOSITORY "${entry_url}"
            GIT_TAG "${entry_hash}"
            GIT_SHALLOW TRUE)
        FetchContent_MakeAvailable("${entry_repo_name}")
    endforeach()
endfunction()
# Test
if(NOT PROJECT_IS_TOP_LEVEL)
    return()
endif()
thezhe_content_lock()
thezhe_templatelists()
