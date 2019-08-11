# pm2 使用

## 常用的功能

-   启用多进程，充分利用多 cpu
-   多进程的负载均衡
-   0 秒重启
-   后台运行
-   提供进程交互（例如：监控）接口

## 常用命令

-   pm2 [start|restart][ecosystem.config.js | app.js ] 启动 app
-   pm2 list : 列表显示应用
-   pm2 monit: 在终端展示运行监控 ui
-   pm2 logs 时时日志

## ecosystem.config.js

```javascript
module.exports = {
    /**
     * Application configuration section
     * http://pm2.keymetrics.io/docs/usage/application-declaration/
     */
    apps: [
        // First application
        {
            name: "API",
            script: "app.js",
            env: {
                COMMON_VARIABLE: "true"
            },
            env_production: {
                NODE_ENV: "production"
            }
        },

        // Second application
        {
            name: "WEB",
            script: "web.js"
        }
    ],

    /**
     * Deployment section
     * http://pm2.keymetrics.io/docs/usage/deployment/
     */
    deploy: {
        production: {
            user: "node",
            host: "212.83.163.1",
            ref: "origin/master",
            repo: "git@github.com:repo.git",
            path: "/var/www/production",
            "post-deploy":
                "npm install && pm2 reload ecosystem.config.js --env production"
        },
        dev: {
            user: "node",
            host: "212.83.163.1",
            ref: "origin/master",
            repo: "git@github.com:repo.git",
            path: "/var/www/development",
            "post-deploy":
                "npm install && pm2 reload ecosystem.config.js --env dev",
            env: {
                NODE_ENV: "dev"
            }
        }
    }
};
```

### 配置字段

-   name: 应用进程名称；

-   script: 启动脚本路径；

-   cwd: 应用启动的路径，关于 script 与 cwd 的区别举例说明：在/home/polo/目录下运行/data/release/node/index.js，此处 script 为/data/release/node/index.js，cwd 为/home/polo/；

-   args: 传递给脚本的参数；

-   interpreter: 指定的脚本解释器；

-   interpreter_args: 传递给解释器的参数；

-   instances: 应用启动实例个数，仅在 cluster 模式有效，默认为 fork；

-   exec_mode: 应用启动模式，支持 fork 和 cluster 模式；

-   watch: 监听重启，启用情况下，文件夹或子文件夹下变化应用自动重启；

-   ignore_watch: 忽略监听的文件夹，支持正则表达式；

-   max_memory_restart: 最大内存限制数，超出自动重启；

-   env: 环境变量，object 类型，如{"NODE_ENV":"production", "ID": "42"}；

-   log_date_format: 指定日志日期格式，如 YYYY-MM-DD HH:mm:ss；

-   error_file: 记录标准错误流，\$HOME/.pm2/logs/XXXerr.log)，代码错误可在此文件查找；

-   out_file: 记录标准输出流，\$HOME/.pm2/logs/XXXout.log)，如应用打印大量的标准输出，会导致 pm2 日志过大；

-   min_uptime: 应用运行少于时间被认为是异常启动；

-   max_restarts: 最大异常重启次数，即小于 min_uptime 运行时间重启次数；

-   autorestart: 默认为 true, 发生异常的情况下自动重启；

-   cron_restart: crontab 时间格式重启应用，目前只支持 cluster 模式；

-   force: 默认 false，如果 true，可以重复启动一个脚本。pm2 不建议这么做；

-   restart_delay: 异常重启情况下，延时重启时间；

[更多内容](http://pm2.keymetrics.io/docs/usage/application-declaration/)
