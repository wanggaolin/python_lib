### python 公共方法库,方便使用
#### install    
    cd /usr/local/src && git clone https://github.com/wanggaolin/public_lib.git && \
    cd public_lib && python setup.py install || cd public_lib/ && git pull && python setup.py  install

## 1系统模块    
#### 1.0.1 进度条
    import time
    F = public_lib.proging_rate(screen_max=1000,screen_name='1000M',rate_symbol='#')
    for i in range(1000):
        time.sleep(0.1)
        F.update("%sM" % i)
    F.end()
    
#### 1.0.2 漂亮的json        
    In [5]: print public_lib.json_data({'a':'你好'})
    {
        "a": "你好"
    }

#### 1.0.3 方便的time模块
    In [10]: public_lib.CurrTime()
    Out[10]: '2017-07-31 11:04:01'
    
    In [11]: public_lib.CurrDay()
    Out[11]: '2017-07-31'

#### 1.0.4 文件模块
    In [17]: public_lib.all_file('.')
    Out[17]: ['./+~JF1688623560254782582.tmp']

    In [7]: public_lib.dir_name('/a/b/')
    Out[7]: '/a/b'
        
#### 1.0.5 方便的网络模块
    In [6]: public_lib.telnet(ip='1.1.1.1',port=22,timeout=10)
    Out[6]: (False, socket.timeout('timed out'))
           
#### 1.0.6 输出带颜色字体
    In [3]: print public_lib.color('x')
    In [4]: print public_lib.color('x',name='green')    
    In [5]: print public_lib.color('x',number=35)
    
#### 1.0.7 隐藏文本字符替换为*
    In [2]: public_lib.hide_str('nihaoma',start=2,end=4) #隐藏字符
    Out[2]: 'ni**oma'
    
#### 1.0.8参数校验
    In [2]: public_lib.check_bank('6228480402564890018') #银行卡号检查
    Out[2]: True

    In [2]: public_lib.check_card(530826198410209673)   #身份证号检查
    Out[2]: True

    #rule规则列表
        number:True     必须是数字[小数点/整数/负数]
        number_str:True 只能输入字母或数字
        time_day:true	必须输入正确格式的日期（ISO），例如：2009-06-23/1998/01/22。只验证格式，不验证有效性。
        minlength:10	输入长度最小是 10 的字符串（汉字算一个字符）。
        maxlength:5	    输入长度最多是 5 的字符串（汉字算一个字符）。
        rangelength:[5,10]	输入长度必须介于 5 和 10 之间的字符串（汉字算一个字符）。
        max:5	        输入的数字不能大于 5。
        min:10	        输入的数字不能小于 10。
        file:True	    必须是一个文件路径。
        email:True	    必须是一个邮箱
        bank:True	    必须是一个银行卡号
        card:True	    必须是一个身份证号
        ip:True	        必须是一个合法ip地址
        mobile:True	    必须是一个手机号码
        symbols:Ture    不得包含特殊符号:*,%
	
    #用法
    print public_lib.json_data(public_lib.check_req(data={"number":'a'}).rule(rule=
        {
            "number":{                #字典中对应key  
                "alias": "手机号",     #别名
                "number": True,       #规则
                "minlength":5         #规则可以写多个  
                }
        }
    ))
    rule:检查规则
    data:检查对象,必须是字典

    #返回
        {'status':False,'data':self.data,'msg':''}
            #status:验证成功失败,[true/false]
            #data:原验证的数据
            #msg:失败原因

#### 1.1.0　随机获取use-agent
    In [8]: public_lib.user_agent()
    Out[8]: 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (...'

#### 1.1.1　获取随机一个hashid或根据指定字符串返回一个id
    In [5]: public_lib.hash_id()
    Out[5]: '7580a0faf2b11cf149b6f74067a30a974c1eee71'
    
    In [6]: public_lib.hash_id('hello word')
    Out[6]: 'e0738b87e67bbfc9c5b77556665064446430e81c'

#### 1.1.2　获取随机一个hashid或根据指定字符串返回一个id
    In [8]: public_lib.md5_id()
    Out[8]: '9aba2e0c5be39d89842f0cf6ff12a7f5'
    
    In [9]: public_lib.md5_id('hello word')
    Out[9]: '13574ef0d58b50fab38ec841efe39df4'

#### 1.1.3　随机获取use-agent
    In [10]: public_lib.user_agent()
    Out[10]: 'Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/47.0.2526.111 Safari/537.36'

#### 1.1.4　将list切割成n等份
    In [2]: public_lib.list_cut(range(10),4)
    Out[2]: [[0, 1, 2, 3], [4, 5, 6, 7], [8, 9]]
       
#### 1.1.5　检查ip地址是否合法       
    In [5]: public_lib.check_ip('1.1.1.1222')
    Out[5]: False

#### 1.1.6　检查ip地址是私有地址
    In [6]: public_lib.check_ip_private('172.16.5.5')
    Out[6]: True

#### 1.1.７　获取系统版本
    In [5]: public_lib.uname()
    Out[5]: 'Ubuntu 14.04.3 LTS'

#### 1.1.8　检查文本是否包含特殊符号
    In [2]: public_lib.check_symbols('..')
    symbols(status=False, symbols='..')

#### 1.1.8　网络ping
    In [3]: public_lib.ping(ip='www.lssin.com')
    ping(status=True, min='3.407', avg='3.581', max='3.726', mdev='0.131', lost='0%', text='')

## 2邮箱模块
#### 2.0.1　发送邮箱附件,支持多个文件
    print public_lib.send_file(
        smtp='smtp.xxxxx.com',
        user='alert@xxxxx.com',
        passwd='xxxxx',
        subject="test file",
        to_list=['brach@lssin.com'],
        file_list=['/tmp/123','/tmp/456']
    )
    
#### 2.0.2　发送邮箱
    print public_lib.send_mail(
        smtp='smtp.xxxxx.com',
        user='alert@xxxxx.com',
        passwd='xxxxx',
        subject="test mail",
        to_list=['brach@lssin.com'],
        text="hello word",
    )    

#### 2.0.3　解析邮件文本[/var/spool/mail/root]
    In [2]: a="""
       ...: From MAILER-DAEMON  Mon Aug 28 17:49:35 2017
       ...: ....
       ...: Message-Id: <20170828094935.B018E143019@source.localdomain>
       ...: Status: O
       ...: 
       ...: This is test mail.
       ...: """
    In [3]: print public_lib.mail_text(a.strip())
    {'Date': 'Mon, 28 Aug 2017 17:49:35 +0800 (CST)', 'text': 'This is a MIME....

## 3监控模块            
#### 3.0.1　根据某个进程名称获取对应的pid和使用的内存大小
    In [2]: public_lib.pid('java')
    Out[2]: pid(memory=1056864, pid=['6168'])
    
## 4日志模块
#### 4.0.1 记录日志到系统日志中[/var/log/message]
    public_lib.syslog.error("test log")  
        