# content.lock

Fetch content using a content-lock file

## Usage

```CMake
# CMakeLists.txt

include(FetchContent)
FetchContent_Declare(
    contents
    GIT_REPOSITORY https://github.com/thezhe/content.lock.git
    GIT_TAG <hash>
    GIT_SHALLOW TRUE)
FetchContent_MakeAvailable(contents)

thezhe_content_lock("contents.txt")
```

`contents.txt` includes newline-delimited repos in the following formats:

- `<owner>/<repo>@<hash>`
- `<url>.git@<hash>`

## Versioning

- Tags - stable SemVer
- `main` branch - unstable
