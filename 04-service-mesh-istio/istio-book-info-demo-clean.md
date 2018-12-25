##  BookInfo配置清理

### 流量控制规则清理

* 获得 destinationrule [目的路由规则]

  ```
  kubectl get destinationrule
  ```
  显示：
  ```
  NAME      AGE
  reviews   18m
  ```
  
  删除可以使用命令
  
  ```
  kubectl delete destinationrule reviews
  ```

* 获得 virtualservices [虚拟服务]

  ```
  kubectl get virtualservices
  ```
    
  显示
  
  ```
  NAME      AGE
  ratings   16m
  reviews   27m
  ```
  
  删除可以使用命令  
  ```
  kubectl delete virtualservices ratings reviews
  ```
  
### 部署应用清理


删除ingress访问入口


```
kubectl delete ingress bootinfo
```


删除bookinfo所有部署


```
kubectl delete -f https://raw.githubusercontent.com/mxnavi/devops-study/master/04-service-mesh-istio/mxnavi-istio-yaml/bookinfo/samples/bookinfo/platform/kube/bookinfo.yaml
```