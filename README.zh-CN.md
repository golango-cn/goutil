# Go Util

![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/gookit/goutil?style=flat-square)
[![GitHub tag (latest SemVer)](https://img.shields.io/github/tag/gookit/goutil)](https://github.com/gookit/goutil)
[![GoDoc](https://godoc.org/github.com/gookit/goutil?status.svg)](https://pkg.go.dev/github.com/gookit/goutil)
[![Go Report Card](https://goreportcard.com/badge/github.com/gookit/goutil)](https://goreportcard.com/report/github.com/gookit/goutil)
[![Unit-Tests](https://github.com/gookit/goutil/workflows/Unit-Tests/badge.svg)](https://github.com/gookit/goutil/actions)
[![Build Status](https://travis-ci.org/gookit/goutil.svg?branch=master)](https://travis-ci.org/gookit/goutil)
[![Coverage Status](https://coveralls.io/repos/github/gookit/goutil/badge.svg?branch=master)](https://coveralls.io/github/gookit/goutil?branch=master)

Go一些常用的工具函数收集、实现和整理

> **[EN README](README.md)**

- `arrutil` array/slice util
- `dump`  简单的变量打印工具，打印 slice, map 会自动换行显示每个元素，同时会显示打印调用位置
- `cliutil` CLI util
- `envutil` ENV util
- `fmtutil` format data tool
- `fsutil` filesystem util
- `jsonutil` JSON util
- `maputil` map util
- `mathutil` math util
- `netutil` network util
- `strutil` string util
- `testutil` test help util

## GoDoc

- [godoc for github](https://pkg.go.dev/github.com/gookit/goutil)

## Util Packages

### Array/Slice

> Package `github.com/gookit/goutil/arrutil`

```go
// source at arrutil/slice.go
func Reverse(ss []string)
func StringsRemove(ss []string, s string) []string
func StringsToInts(ss []string) (ints []int, err error)
func TrimStrings(ss []string, cutSet ...string) (ns []string)
func IntsHas(ints []int, val int) bool
func Int64sHas(ints []int64, val int64) bool
func StringsHas(ss []string, val string) bool
func Contains(arr, val interface{}) bool
func NotContains(arr, val interface{}) bool
```

### CLI

> Package `github.com/gookit/goutil/cliutil`

```go
// source at cliutil/cliutil.go
func QuickExec(cmdLine string, workDir ...string) (string, error)
func ExecCmd(binName string, args []string, workDir ...string) (string, error)
func ExecCommand(binName string, args []string, workDir ...string) (string, error)
func ShellExec(cmdLine string, shells ...string) (string, error)
func CurrentShell(onlyName bool) (path string)
func HasShellEnv(shell string) bool
```

### Dump

> Package `github.com/gookit/goutil/dump`

```go
// source at dump/dump.go
func Std() *Dumper
func Reset()
func Config(fn func(*Dumper))
func Print(vs ...interface{})
func Println(vs ...interface{})
func Fprint(w io.Writer, vs ...interface{})
// source at dump/dumper.go
func NewDumper(out io.Writer, skip int) *Dumper
```

### ENV

> Package `github.com/gookit/goutil/envutil`

```go
// source at envutil/envutil.go
func ParseEnvValue(val string) (newVal string)
// source at envutil/get.go
func Getenv(name string, def ...string) string
// source at envutil/info.go
func IsWin() bool
func IsMac() bool
func IsLinux() bool
func IsConsole(out io.Writer) bool
func IsMSys() bool
func HasShellEnv(shell string) bool
func IsSupportColor() bool
func IsSupport256Color() bool
func IsSupportTrueColor() bool
```

### Formatting

> Package `github.com/gookit/goutil/fmtutil`

```go
// source at fmtutil/format.go
func DataSize(bytes uint64) string
func PrettyJSON(v interface{}) (string, error)
func StringsToInts(ss []string) (ints []int, err error)
// source at fmtutil/time.go
func HowLongAgo(sec int64) string
```

### FileSystem

> Package `github.com/gookit/goutil/fsutil`

```go
// source at fsutil/filesystem.go
func PathExists(path string) bool
func IsDir(path string) bool
func FileExists(path string) bool
func IsFile(path string) bool
func IsAbsPath(filepath string) bool
func Mkdir(dirPath string, perm os.FileMode) error
func MustReadFile(filePath string) []byte
func OpenFile(filepath string, flag int, perm int) (*os.File, error)
func CreateFile(fpath string, filePerm, dirPerm os.FileMode) (*os.File, error)
func MimeType(path string) (mime string)
func ReaderMimeType(r io.Reader) (mime string)
func IsImageFile(path string) bool
func IsZipFile(filepath string) bool
func Unzip(archive, targetDir string) (err error)
func DeleteIfFileExist(fpath string) error
// source at fsutil/finder.go
```

### JSON

> Package `github.com/gookit/goutil/jsonutil`

```go
// source at jsonutil/jsonutil.go
func WriteFile(filePath string, data interface{}) error
func ReadFile(filePath string, v interface{}) error
func Encode(v interface{}) ([]byte, error)
func Decode(json []byte, v interface{}) error
func Pretty(v interface{}) (string, error)
func StripComments(src string) string
```

### Map

> Package `github.com/gookit/goutil/maputil`

```go
// source at maputil/map.go
func MergeStringMap(src, dst map[string]string, ignoreCase bool) map[string]string
func KeyToLower(src map[string]string) map[string]string
func GetByPath(key string, mp map[string]interface{}) (val interface{}, ok bool)
func Keys(mp interface{}) (keys []string)
func Values(mp interface{}) (values []interface{})
```

### Math/Number

> Package `github.com/gookit/goutil/mathutil`

```go
// source at mathutil/convert.go
func Int(in interface{}) (int, error)
func MustInt(in interface{}) int
func ToInt(in interface{}) (iVal int, err error)
func Uint(in interface{}) (uint64, error)
func MustUint(in interface{}) uint64
func ToUint(in interface{}) (u64 uint64, err error)
func Int64(in interface{}) (int64, error)
func MustInt64(in interface{}) int64
func ToInt64(in interface{}) (i64 int64, err error)
func Float(in interface{}) (float64, error)
func ToFloat(in interface{}) (f64 float64, err error)
func MustFloat(in interface{}) float64
// source at mathutil/number.go
func Percent(val, total int) float64
func ElapsedTime(startTime time.Time) string
func DataSize(size uint64) string
func HowLongAgo(sec int64) string
// source at mathutil/random.go
func RandomInt(min, max int) int
```

### String

> Package `github.com/gookit/goutil/strutil`

```go
// source at strutil/encode.go
func Base64(str string) string
func B64Encode(str string) string
func URLEncode(s string) string
func URLDecode(s string) string
// source at strutil/find_similar.go
func NewComparator(src, dst string) *SimilarComparator
func Similarity(s, t string, rate float32) (float32, bool)
// source at strutil/format.go
func Lowercase(s string) string
func Uppercase(s string) string
func UpperWord(s string) string
func LowerFirst(s string) string
func UpperFirst(s string) string
func Snake(s string, sep ...string) string
func SnakeCase(s string, sep ...string) string
func Camel(s string, sep ...string) string
func CamelCase(s string, sep ...string) string
// source at strutil/id.go
func MicroTimeID() string
func MicroTimeHexID() string
// source at strutil/random.go
func Md5(src interface{}) string
func GenMd5(src interface{}) string
func RandomChars(ln int) string
func RandomCharsV2(ln int) string
func RandomCharsV3(ln int) string
func RandomBytes(length int) ([]byte, error)
func RandomString(length int) (string, error)
// source at strutil/strconv.go
func String(val interface{}) (string, error)
func MustString(in interface{}) string
func ToString(val interface{}) (str string, err error)
func ToBool(s string) (bool, error)
func MustBool(s string) bool
func Bool(s string) (bool, error)
func Int(s string) (int, error)
func ToInt(s string) (int, error)
func MustInt(s string) int
func ToInts(s string, sep ...string) ([]int, error)
func ToIntSlice(s string, sep ...string) (ints []int, err error)
func ToArray(s string, sep ...string) []string
func ToSlice(s string, sep ...string) []string
func ToTime(s string, layouts ...string) (t time.Time, err error)
// source at strutil/strutil.go
func IsAlphabet(char uint8) bool
func Trim(s string, cutSet ...string) string
func TrimLeft(s string, cutSet ...string) string
func TrimRight(s string, cutSet ...string) string
func FilterEmail(s string) string
func Split(s, sep string) (ss []string)
func Substr(s string, pos, length int) string
func Padding(s, pad string, length int, pos uint8) string
func PadLeft(s, pad string, length int) string
func PadRight(s, pad string, length int) string
func Repeat(s string, times int) string
func RepeatRune(char rune, times int) (chars []rune)
func Replaces(str string, pairs map[string]string) string
func PrettyJSON(v interface{}) (string, error)
func RenderTemplate(input string, data interface{}, fns template.FuncMap, isFile ...bool) string
func RenderText(input string, data interface{}, fns template.FuncMap, isFile ...bool) string
```

### System

> Package `github.com/gookit/goutil/sysutil`

```go
// source at sysutil/exec.go
func QuickExec(cmdLine string, workDir ...string) (string, error)
func ExecCmd(binName string, args []string, workDir ...string) (string, error)
func ShellExec(cmdStr string, shells ...string) (string, error)
// source at sysutil/sysutil.go
func CurrentShell(onlyName bool) (path string)
func HasShellEnv(shell string) bool
func IsWin() bool
func IsWindows() bool
func IsMac() bool
func IsLinux() bool
func IsMSys() bool
func IsConsole(out io.Writer) bool
// source at sysutil/sysutil_nonwin.go
func Kill(pid int, signal syscall.Signal) error
func ProcessExists(pid int) bool
// source at sysutil/sysutil_windows.go
func Kill(pid int, signal syscall.Signal) error
func ProcessExists(pid int) bool
```

### Testing

> Package `github.com/gookit/goutil/testutil`

```go
// source at testutil/httpmock.go
func NewHttpRequest(method, path string, data *MD) *http.Request
func MockRequest(h http.Handler, method, path string, data *MD) *httptest.ResponseRecorder
// source at testutil/testutil.go
func DiscardStdout() error
func ReadOutput() (s string)
func RewriteStdout()
func RestoreStdout() (s string)
func RewriteStderr()
func RestoreStderr() (s string)
func MockEnvValue(key, val string, fn func(nv string))
func MockEnvValues(kvMap map[string]string, fn func())
```

## Gookit packages

  - [gookit/ini](https://github.com/gookit/ini) Go config management, use INI files
  - [gookit/rux](https://github.com/gookit/rux) Simple and fast request router for golang HTTP 
  - [gookit/gcli](https://github.com/gookit/gcli) Build CLI application, tool library, running CLI commands
  - [gookit/slog](https://github.com/gookit/slog) Lightweight, easy to extend, configurable logging library written in Go
  - [gookit/color](https://github.com/gookit/color) A command-line color library with true color support, universal API methods and Windows support
  - [gookit/event](https://github.com/gookit/event) Lightweight event manager and dispatcher implements by Go
  - [gookit/cache](https://github.com/gookit/cache) Generic cache use and cache manager for golang. support File, Memory, Redis, Memcached.
  - [gookit/config](https://github.com/gookit/config) Go config management. support JSON, YAML, TOML, INI, HCL, ENV and Flags
  - [gookit/filter](https://github.com/gookit/filter) Provide filtering, sanitizing, and conversion of golang data
  - [gookit/validate](https://github.com/gookit/validate) Use for data validation and filtering. support Map, Struct, Form data
  - [gookit/goutil](https://github.com/gookit/goutil) Some utils for the Go: string, array/slice, map, format, cli, env, filesystem, test and more
  - More, please see https://github.com/gookit

## License

[MIT](LICENSE)
