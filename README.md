# content_lock

Declaratively fetch content

## Usage

### CMakeLists.txt

```CMake
include(FetchContent)
FetchContent_Declare(
    content_lock
    GIT_REPOSITORY https://github.com/thezhe/content_lock.git
    GIT_TAG <hash>
    GIT_SHALLOW TRUE)
FetchContent_MakeAvailable(content_lock)
thezhe_content_lock()
```

## Versioning

- Tags - stable SemVer
- `main` branch - unstable
