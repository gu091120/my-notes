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
  apps : [

    // First application
    {
      name      : 'API',
      script    : 'app.js',
      env: {
        COMMON_VARIABLE: 'true'
      },
      env_production : {
        NODE_ENV: 'production'
      }
    },

    // Second application
    {
      name      : 'WEB',
      script    : 'web.js'
    }
  ],

  /**
   * Deployment section
   * http://pm2.keymetrics.io/docs/usage/deployment/
   */
  deploy : {
    production : {
      user : 'node',
      host : '212.83.163.1',
      ref  : 'origin/master',
      repo : 'git@github.com:repo.git',
      path : '/var/www/production',
      'post-deploy' : 'npm install && pm2 reload ecosystem.config.js --env production'
    },
    dev : {
      user : 'node',
      host : '212.83.163.1',
      ref  : 'origin/master',
      repo : 'git@github.com:repo.git',
      path : '/var/www/development',
      'post-deploy' : 'npm install && pm2 reload ecosystem.config.js --env dev',
      env  : {
        NODE_ENV: 'dev'
      }
    }
  }
};

```

[更多内容](http://pm2.keymetrics.io/docs/usage/application-declaration/)
