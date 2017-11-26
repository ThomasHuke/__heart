# lean [beego](https://www.github.com/ThomasHuke/astaxie/beego)
> 学习谢神的beego web 框架。

关键的几个配置文件：

```go
var (
    // BConfig is the default config for Application
    BConfig *Config
    // AppConfig is the instance of Config, store the config information from file
    AppConfig *beegoAppConfig
    // AppPath is the absolute path to the app
    AppPath string
    // GlobalSessions is the instance for the session manager
    GlobalSessions *session.Manager
)
```

其中 ：

BConfig:

```go
AppName             string //Application name
   RunMode             string //Running Mode: dev | prod
   RouterCaseSensitive bool
   ServerName          string
   RecoverPanic        bool
   RecoverFunc         func(*context.Context)
   CopyRequestBody     bool
   EnableGzip          bool
   MaxMemory           int64
   EnableErrorsShow    bool
   EnableErrorsRender  bool
   Listen              Listen
   WebConfig           WebConfig
   Log                 LogConfig
}

```
其中后面三个 listen webconfig logconfig 都是另一些struct：

listen:
```go
type Listen struct {
    Graceful      bool // Graceful means use graceful module to start the server
    ServerTimeOut int64
    ListenTCP4    bool
    EnableHTTP    bool
    HTTPAddr      string
    HTTPPort      int
    EnableHTTPS   bool
    HTTPSAddr     string
    HTTPSPort     int
    HTTPSCertFile string
    HTTPSKeyFile  string
    EnableAdmin   bool
    AdminAddr     string
    AdminPort     int
    EnableFcgi    bool
    EnableStdIo   bool // EnableStdIo works with EnableFcgi Use FCGI via standard I/O
}

```

WebConfig:

```go

type WebConfig struct {
    AutoRender             bool
    EnableDocs             bool
    FlashName              string
    FlashSeparator         string
    DirectoryIndex         bool
    StaticDir              map[string]string
    StaticExtensionsToGzip []string
    TemplateLeft           string
    TemplateRight          string
    ViewsPath              string
    EnableXSRF             bool
    XSRFKey                string
    XSRFExpire             int
    Session                SessionConfig
}

```

其中 SessionConfig是：
```go
type SessionConfig struct {
    SessionOn                    bool
    SessionProvider              string
    SessionName                  string
    SessionGCMaxLifetime         int64
    SessionProviderConfig        string
    SessionCookieLifeTime        int
    SessionAutoSetCookie         bool
    SessionDomain                string
    SessionDisableHTTPOnly       bool // used to allow for cross domain cookies/javascript cookies.
    SessionEnableSidInHTTPHeader bool //	enable store/get the sessionId into/from http headers
    SessionNameInHTTPHeader      string
    SessionEnableSidInURLQuery   bool //	enable get the sessionId from Url Query params
}

```

LogConfig:

```go
type LogConfig struct {
    AccessLogs  bool
    FileLineNum bool
    Outputs     map[string]string // Store Adaptor : config
}

```
