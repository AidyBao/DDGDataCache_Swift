
## DDGDataCache
或许有这样的需求，要求页面在无网状态先显示上一次显示的数据，这就涉及到缓存，
但是缓存又分为文件缓存，归档等，realm 太过笨重，归档太麻烦，最后选择了文件缓存，
看了很多博客，在参考了别人的缓存开源项目，功能太过简单单一化，
比如：我想删除某一个文件下的缓存信息，大部分是只提供了删除所有缓存，
不可以按目录删除。我总结了一个库，可以异步按照目录删除。
简单方便，快捷神速，是居家iOS码农必备之利器，先看功能效果
。简单方便，快捷神速，是居家iOS码农必备之利器，具体功能模块如下。

![image](https://raw.githubusercontent.com/dudongge/DDGDataCache_Swift/master/DDGDataCache_Swift/gif/DDGDataCache.gif)
    
  ```  
    //构建模拟数据
     /**
     *  模拟数据请求URL
     */
     let URLString = "https://github.com/dudongge"
     let URLString1 = "https://github.com/dudongge/DDGScreenShot"
     let URLString2 = "https://github.com/dudongge/DDGMeiTuan"
     let URLString3 = "https://github.com/dudongge/DGKVO"
    
    /**
     *  模拟服务器请求数据
     */
    let responseObject = [ "sex" : "男",
                           "city" : "上海",
                           "logintime" : "1445267749",
                           "name" : "东阁堂主",
                           "group" : "3",
                           "loginhit" : "4",
                           "id" : "234328",
                           "QQ" : "532835032" ]
```
1，同步写入
     ```        
         写入/更新缓存(同步) [按APP版本号缓存,不同版本APP,同一接口缓存数据互不干扰]
         - parameter jsonResponse: 要写入的数据(JSON)
         - parameter URL:          数据请求URL
         - parameter path:         一级文件夹路径path（必须设置）
         - parameter subPath:      二级文件夹路径subPath（可设置-可不设置）
         - returns: 是否写入成功
        if DDGDataCache.saveJsonResponseToCacheFile(self.responseObject as AnyObject,
                                                        URL: self.URLString,
                                                        path: "appCache") {
                print("😆(同步)保存/更新成功")
        } else {
                print("😤(同步)保存/更新失败")
        }
        ```
 1，异步写入
 ```
     写入/更新缓存(异步) [按APP版本号缓存,不同版本APP,同一接口缓存数据互不干扰]
     - parameter jsonResponse: 要写入的数据(JSON)
     - parameter URL:          数据请求URL
     - parameter subPath:      二级文件夹路径subPath（可设置-可不设置）
     - parameter completed:    异步完成回调(主线程回调)
     
     DDGDataCache.save_asyncJsonResponseToCacheFile(self.responseObject as AnyObject,
                                                           URL: self.URLString3,
                                                           path: "appCache",
                                                           subPath: "userInfo") { (succ) in
             if  succ {
                print("😆(异步)保存/更新成功")
                 } else {
                print("😤(异步)保存/更新失败")
             }
    }
```
2.获取已经缓存的数据
 ```
     获取缓存的对象(同步)
     - parameter URL: 数据请求URL
     - parameter subPath:      二级文件夹路径subPath（可设置-可不设置）
     - returns: 缓存对象
    
     if let json = DDGDataCache.cacheJsonWithURL(URLString)  {
            print(json)
      }
      //获取指定缓存数据
      if let json = DDGDataCache.cacheJsonWithURL(URLString,subPath: "userInfo")  {
           print(json)
     }
```
3.获取缓存数据的大小
```
    //获取总的缓存大小
    let allSize =  DDGDataCache.cacheAllSize()
    let size =  String(format: "%.6f", allSize)
    print("缓存大小(M)=\(size)")
    //获取制定路径的缓存大小（传入二级路径）
    let allSize =  DDGDataCache.cacheSizeWithUrl("userInfo")
    print("缓存大小(M)=\(allSize)")
```
4，删除缓存
```
    //清除全部缓存
    if DDGDataCache.clearAllCache() {
        print("😆清除缓存成功")
    } else {
        print("😤清除缓存失败")
    }
    //清除指定缓存
    if DDGDataCache.clearCacheWithUrl("userInfo") {
        print("😆清除缓存成功")
    } else {
        print("😤清除缓存失败")
    }
```

## 直接把代码拖入
```
    直接将DDGDataCache文件夹下的文件拖入即可
   
```
## 注意点（决定成功的关键）
```
    注意: 使用前请在'-Bridging-Header.h' 桥接文件中导入    #import<CommonCrypto/CommonCrypto.h>
        因为要用到MD5加密的东西
```


## License

DDGDataCache is available under the MIT license. See the LICENSE file for more info.
如果有问题欢迎提出，QQ：532835032 ，如果对您有帮助，希望您动动鼠标，不吝给个star.!


## instructions （备注）

鉴于还有部分童鞋还在OC上开发，本库相同功能翻译成OC，大家多了一个选择，附上链接，希望可以帮到你：


  
