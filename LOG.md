# Log
- logging模块提供模块级别的函数记录日志
- 四大组件

## 1. 日志相关概念
- 日志的级别(level):
    - 不同的用户关注不同信息
    - Debug, Info, Notice, Warning, Error, Critical, Alert, Emergency
- 写日志是I/O操作,速度缓慢,尽量减少此类操作(但不能缺少)
- log作用
    - 调试
    - 了解软件的运行情况
    - 分析定位问题
- log内容
    - time
    - place
    - level
    - 问题信息
- 第三方日志
    - log4j
    - log4php
    - log4ing
 
## 2. logging模块
- logging日志级别
    - Debug, Info, Warning, Error, Critical
    - 可自定义
- 初始化/写日志需要制定级别,只有级别大于等于设定的才记录
- 使用
    - 直接使用logging(综合四组件,但功能不全)
    - 使用四大组件定制
    
### 2.1 logging模块级别的日志
- 使用以下函数
    - logging.debug(msg, *args, **kwargs)
    - logging.info(msg, *args, **kwargs)
    - logging.warning(msg, *args, **kwargs)
    - logging.error(msg, *args, **kwargs)
    - logging.critical(msg, *args, **kwargs)
    - logging.log(level, msg, *args, **kwargs) 创建一个严重级别为level的日志(他可以代替上面所有)
    - logging.basicConfig(**kwargs)
- logging.basicConfig(**kwargs)
    - 对root logger进行一次性配置
    - 只在第一次调用时起作用
    - 不配置logger,则使用默认值
        - 输出: sys.stderr
        - 级别: warning
        - 格式: level:log_name:content
    - 案例p01
        - 默认级别为warning
        - basicConfig(filename--> 指定输出到哪个文件, level--> 要大写)
        - format参数
        
## 2.2 logging模块的处理流程
- 四大组件
    - 日志器(logger):产生日志的一个接口
    - 处理器(handler):把产生的日志发送到相应的目的地
    - 过滤器(filter):更精细的控制信息
    - 格式器(formatter):对输出的信息格式化
- Logger
    - 产生一个日志
    - 操作
                
                Logger.setLevel()     设置最低严重信息
                Logger.addHandler()   为对象添加处理器
                Logger.removeHandler
                Logger.addFilter()    为对象添加过滤器
                Logger.debug():       产生一条debug级别的日志,其他级别类似
                Logger.exception():   创建类似error的日志消息
                Logger.log():         同
    - 如何得到一个logger对象
        - 实例化
        - logging.getLogger()
        
- Handler
    - 把log发送到指定位置
    - 方法:
        - setLevel
        - setFormat
        - addFilter, removeFilter
        - 不能直接用,Handler只是基类
            - logging.StreamHandler
            - logging.FileHandler
            - logging.handlers.RotatingFileHandler
            - logging.handlers.TimedRotatingFileHandler
            - logging.handlers.HTTPHandler
            - logging.HullHandler

- Format类
    - 直接实例化
    - 三个参数
        - fmt: 指定消息格式化字符串,如果不指定该参数则默认使用message的原始值
        - datefmt: 指定日期格式字符串,如果不指定默认"%Y-%m-%d %H:%M:%S"
        - style: 新增参数, 可取值为%,{,$,默认为%
        
- Filter类
    - 可以被Handler和Logger使用
    - 控制传递过来的信息和集体内容