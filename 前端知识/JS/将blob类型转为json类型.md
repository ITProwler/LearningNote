# blob类型转json
## 问题描述
- 前端在处理文件下载失败时，由于在axios里设置了返回类型为blob类型，导致后台返回的json报错信息被转化为blob对象。

    *后台报错之后，将报错信息写入到流内返回前端，http状态码为200，axios会进入then而非catch，通过判断返回的类型type是否为'application/json'来判断是否报错。*
    *如果后台使用setStatus()修改了http状态码（如：500或自定义状态码），则进入catch方法*
           function exportResult(para) {
             axios({
             method: ...,
             data: {...},
             headers: {...},
             responseType: 'bolb',
             }).then(result => {
             //判断是否报错
             if (result.data.type === 'application/json') {
               //将返回结果转化为json对象，处理报错
               new Response(result.data).json().then(res => {
                 //开始处理报错
               })
             }
             }).catch(err => {
               //当后台修改状态码后，进入catch
               //处理自定义报错信息
             })
           }
