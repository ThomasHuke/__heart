# lean [beego](https://www.github.com/astaxie/beego)
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

所以说我们也学会了一些方法那就是：
嵌套式的struct使用，当然你可以直接不写变量直接将一个struct丢进另一个里面，但是，并不美观和直观，所以我个人是喜欢有这种变量的方式的。

```go
这样我们的执行器执行的逻辑是这样的，首先执行 Prepare，这个就是 Go 语言中 struct 中寻找方法的顺序，依次往父类寻找。执行 BaseAdminRouter 时，查找他是否有 Prepare 方法，没有就寻找 baseRouter，找到了，那么就执行逻辑，然后在 baseRouter 里面的 this.AppController 即为当前执行的控制器 BaseAdminRouter，因为会执行 BaseAdminRouter.NestPrepare 方法。然后开始执行相应的 Get 方法或者 Post 方法。
```
上面这段话我们可以看出，如果执行一个函数，在本struct中没有定义，系统就会找寻它是父struct。
