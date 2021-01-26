## Tomcat 8.5.61源码
### 用途
学习源码

### JVM配置
VM options: -Dcatalina.home="/Users/liuyunyang/work/projects/idea/apache-tomcat-8.5.61"

// -D 是java设置参数的固定写法

// catalina.home 是参数名

// =的后面是tomcat源码项目的catalina-home的路径，当这个路径包含空格是需要使用引号括起来

### 源码下载地址
https://archive.apache.org/dist/tomcat/

### 配置过程参考文章
https://www.tqwba.com/x_d/jishu/6220.html

### 控制台乱码问题
org.apache.tomcat.util.res.StringManager类
public String getString(final String key, final Object... args) {
        String value = getString(key);
        if (value == null) {
            value = key;
        }
        try{
            value = new String(value.getBytes("ISO-8859-1"),"UTF-8");
        }catch (Exception e ){
            e.printStackTrace();
        }
 
        MessageFormat mf = new MessageFormat(value);
        mf.setLocale(locale);
        return mf.format(args, new StringBuffer(), null).toString();
    }

org.apache.jasper.compiler.Localizer类

public static String getMessage(String errCode) {
        String errMsg = errCode;
        try {
            if (bundle != null) {
                errMsg = bundle.getString(errCode);
            }
        } catch (MissingResourceException e) {
        }
        try{
            errMsg = new String(errMsg.getBytes("ISO-8859-1"),"UTF-8");
        }catch (Exception e ){
            e.printStackTrace();
        }
        return errMsg;
    }