# Zabbix生产案例实战

## 1、项目规划

### 主机分组

​		交换机

​		Nginx

​		Tomcat

​		MySQL



## 2、监控对象识别

1. 使用SNMP监控交换机
2. 使用IPMI监控服务器硬件
3. 使用Agent监控服务器
4. 使用JMX监控Java
5. 监控MySQL
6. 监控Web状态
7. 监控Nginx状态



### SNMP监控

1、交换机上开启SNMP

```sh
config t
snmp-server community public ro
end
```

2、在Zabbix上添加监控

​		设置SNMP interfaces

3、关联监控模板



### IPMI

​		建议使用自定义item，本地执行IPMItool命令来获取数据。