*// api 封装 post和get 方法*

*import* axios *from* 'axios'

*// 请求超时报错*

**if** (process**.***env***.**NODE_ENV **===** 'development') {

 console**.**log(1)

 axios**.***defaults***.***baseURL* **=**

  'https://mobile-ms.uat.homecreditcfc.cn/mock/6191ba34e84308001da33bed/vue'

} **else** **if** (process**.***env***.**NODE_ENV **===** 'producation') {

 console**.**log(2)

 axios**.***defaults***.***baseURL* **=** ''

} **else** {

 console**.**log(3)

 axios**.***defaults***.***baseURL* **=** ''

}

const instance **=** axios**.**create({

 *// 请求头类型携带token*

 timeout: 3000

})

*/***

 ****@description* *请求前拦截判断是否存在token*

 **/*

instance**.***interceptors***.***request***.**use(

 (**config**) **=>** {

  *// 判断是否存在tokenconfig.headers.Authorization = window.sessionStorage.token 返回config*

  **return** config

 },

 (**error**) **=>** {

  **return** Promise**.**reject(error)

 }

)

*/***

 *** *@description* *返回拦截 判断响应是否成功*

 **/*

instance**.***interceptors***.***response***.**use(

 (**res**) **=>** {

  **return** Promise**.**resolve(res**.***data*)

 },

 (**error**) **=>** {

  **return** Promise**.**reject(error)

 }

)

*export* default instance