# node.js类库 v1.2.2
### 安装：npm install TopuNet-node-functions

文件结构：
-------------
        functions.js 放入项目文件夹handle中

方法列表：
-------------

           高京
                *【同步】 过滤表单非法字符
                * str: 需要过滤的字符串
                convers(str)

                *【同步】格式化日期。今天的日期只显示时间。不含秒
                * timestamp：待格式化时间戳
                * show_time：非今天的日期是否显示具体时间（不含秒）。true/false(默认)
                formatTimeStamp(timestamp, show_time) 

                *【同步】生成随机数随机码。返回字符串
                * n: 位数，数字+字母的组合时请键入偶数
                * kind: 生成种类。1-纯数字 2-纯大写字母 3-纯小写字母 4-数字+大写字母 5-数字+小写字母 6-大写字母或小写字母 7-数字+纯大写字母或小写字母
                CreateRandomStr(n,kind)

                *【同步】生成时间戳（世界标准时间）。返回字符串
                * dt: 日期。
                CreateTimeStamp(dt)

                *【同步】对JSON进行字典序排序（如需和.NET的字典序排序作匹配则不建议使用）。返回JSON对象
                * json_o: JSON对象。
                JsonSort(json_o) 

                *【同步】字符串加密。返回字符串
                * str: 要加密字符串。
                * HashKind: 'md5' | 'sha1'
                * UpperLower: 返回字符串大小写。1-小写 | else-大写
                CreateHash(str, HashKind, UpperLower)

                *【异步】文件读取。next(文件内容，或以"err:"开头的错误信息)
                * query.f:文件路径。如：e:\abc.txt | ./npm-debug.log
                routes.get("/ReadFile", functions.ReadFile, function (data, req, res, next) { }

                *【同步】文件读取。返回（文件内容，或以"err:"开头的错误信息）
                * path:文件路径。如：e:\abc.txt | ./npm-debug.log
                ReadFileSync(path)

                *【同步】生成topu签名。
                    返回：
                    {
                        "non_str": "8q0M3i7T4P1S5J9Q3r1l5p6V5G1O7Q0U",
                        "stamp": "1440570767",
                        "signature": "FC5A7F9BC8A7D418209FCC23772B785155FB3D8F"
                    }
                * ParamsJsonObj:要传参数的JSON对象
                * non_str:随机数，不传会自动生成
                * stamp:时间戳，不传会自动生成
                CreateTopuSignatureSync(ParamsJsonObj, non_str, stamp)

                *【异步】生成topu签名。
                * ParamsJsonObj:要传参数的JSON对象
                * CallBack:成功后的回调
                    传入参数：
                    {
                        "non_str": "8q0M3i7T4P1S5J9Q3r1l5p6V5G1O7Q0U",
                        "stamp": "1440570767",
                        "signature": "FC5A7F9BC8A7D418209FCC23772B785155FB3D8F"
                    }
                * non_str:随机数，不传会自动生成
                * stamp:时间戳，不传会自动生成
                CreateTopuSignature(ParamsJsonObj, CallBack, non_str, stamp) 

                *【异步】向API接口发请求。
                * Host:主机地址，如 "www.twedding.cn"
                * Port:端口号，如 "80"。"443"时代表https提交
                * Path:路径，如 "/test/test.ashx"
                * Method:提交方式 "Post" | "Get"
                * PostData:要通过Post方式传递给API接口的参数集，JSON对象
                * CallBackSuccess:调用成功后的回调方法。
                    传入参数：页面返回值
                * CallBackError:调用连接失败后的回调方法
                    传入参数：错误信息
                DoREST(Host, Port, Path, Method, PostData, CallBackSuccess, CallBackError)

                *【同步】省略字符串。返回省略后的字符串
                * Str 判定长度的字符串
                * Length 限定的字节数（一个汉字占2字节）
                * ShowMore 如字符串需要截取，是否显示... true-显示 false-不显示
                ShengLue(Str, Length, ShowMore)

                *【同步】获得字符串长度。返回长度数值
                * Str 字符串
                StrLength(Str) 

                *【同步】根据文件路径，获得文件扩展名。返回扩展名字符串
                * Str 文件路径
                GetExtension(Str)

                *【同步】对JSON对象的值进行escape转码。返回转码后的JSON对象
                * --经DoREST传参的Json字符串需进行escape转码
                * Json_obj 待转码JSON对象
                * split_str 分隔字符串。如不为空(如{$::::::::::})则会转为：{key1:key1{$::::::::::}value1,key2:key2{$::::::::::}value2}。如为空则会转为：{key1:value1,ke2:value2}
                JsonEscape(Json_obj, split_str)

                *【同步】JSON批量转（与.NET端LitJSON库匹配的）unicode码。返回转码后的JSON对象
                * --防止中文及字符经JSON.parse()时报错
                * Json_obj 要转码的Json对象
                JsonUnicode(Json_obj)

                *【同步】根据主外键关系合并JSON。返回：将Parent_keyName添加到Parent中，并返回Parent
                * Parent：父级JSON
                * Child：子级JSON，主外键相同时，添加到父级JSON中
                * Parent_FK：用于比较的父级外键
                * Child_PK：用于比较的子级主键
                * Parent_keyName：在父级JSON中添加的键名
                JsonUnion(Parent, Child, Parent_FK, Child_PK, Parent_keyName)

                *【同步】对字符串进行数字型判断（支持逗号分隔的多值字符串），返回过滤后的字符串（非数字值被过滤）
                * str 逗号分隔的字符串
                filterNoNum(str) 

                *【同步】自动获得地址栏参数集，并拼接返回为地址栏字符串：a=1&b=2&c=3
                * query：req.query
                * Filter_Para：过滤掉的参数名（键），多个用|分隔，区分大小写
                transParameters(query, Filter_Para)

                *【同步】格式化日期时间。返回字符串
                dt：要格式化的日期字符串
                kind：1-标准全日期 2-标准短日期 其他-自定义字符串
                dateFormat(dt, kind)

                *【异步】发送邮件
                * Subject：主题
                * isHtml：true-使用HTML格式(HtmlBody) false-使用纯文本格式(Body，不推荐)
                * Body：纯文本格式内容
                * HtmlBody：HTML格式内容，要有<html><body></body></html>
                * FromName：发件人名称
                * MailTo：收件人。多个用逗号分隔
                * Bcc：秘密抄送。数组。
                * Reply：回复地址。
                * callback_success(err)：回调方法。正确发送时，err="success"
                MailSend(Subject, isHtml, Body, HtmlBody, FromName, MailTo, Bcc, Reply, callback_success)

                *【同步】遮盖姓名，两边各留一个字。返回新字符串
                * str：原字符串
                * mask：遮盖字符
                * length：遮盖字符出现最长次数
                NameMask(str, mask, length)

                *【同步】遮盖手机，根据length决定两边留几位，最少各留一位。返回新字符串
                * str：原字符串
                * mask：遮盖字符
                * length：遮盖字符出现最长次数
                MobileMask(str, mask, length)


                *【同步】图片缩放（不支持定高不定宽）、水印（暂时没做）。返回ERROR或SUCCESS
                * originalImagePath：源图片路径。注意根目录的写法为：./01.jpg
                * outputPath：输出图片路径。要包含后缀，如：./01_output.jpg
                * width：宽。0为不缩放
                * height：高。0为按比例缩放。不为0时，可能会变形
                MakeThumb (originalImagePath, outputPath, width, height) 
             
                *【同步】格式化Textarea输入的字符串，替换空格和回车（注意用<%- %>输出。返回字符串
                * str：要格式化的字符串
                formatTextArea(str)

                *【同步】获取网址的二级域名
                get_domain(req)

                *【同步】根据第一个数组中的值匹配，取出第二个数组中相对应位置的值。
                * arr_source：源数组
                * match：匹配值
                * arr_target：目标数组
                arr_value_match(arr_source, match, arr_target)

                *【异步】解析xml为json
                * xmlString：待解析的xml字符串
                * CallBack_success(json)：成功回调
                xmlToJson(xmlString, CallBack_success)

                *【同步】渲染错误页面
                Error(res, err)

                *【异步】request请求
                * opt: {
                        url: request地址，支持https协议和地址栏参数,
                        method: get|post_json|post_file。 默认get,
                        PostData: method=post_json时有效; json对象,
                        PostData_escape: 对PostData进行unicode和escape编码（针对拓扑接口）。默认"true"，调用微信或其他不需要编码接口时，设为"false"
                        files: method=post_file时有效; 名称1|文件名1||名称2|文件名2||名称3|文件名3...,
                        cert: cert证书文件路径。"d:\cert.crt"||"./cert.crt",
                        cert_key: cert密钥文件路径。"d:\cert.key"||"./cert.key",
                        ca: ca证书路径,
                        pfx：pfx证书,
                        passwd: cert|pfx证书密码
                  }
                * Callback_success(json): 成功回调
                * Callback_error(err): 失败回调
                Request(opt, Callback_success, Callback_error)

            陈斌
                *【同步】中文unicode转码。返回转码后字符串
                * text 要转码的中文
                uniencode(text)

                *【同步】判断逗号分隔的主码中是否含有某一主码。返回true或false
                * str 被比较字符串。可以为逗号分隔的多个主码，也可以是尖括号包围的多个主码
                * Pat 条件主码string类型
                checkHave(str, Pat)

                 *@【同步】生成cookies
                 *@Mid 会员id
                 *@Passwd 密码
                 CreatCookies(id, Passwd, res)

                 *@【同步】获取cookies中的值并返回用户Mid和密码
                GetCookies(req)


                 *@【同步】给图片添加水印
                 *@ watermarkImg_src:水印图片路径
                 *@ sourceImg_src:待加水印图片路径
                 *@ savePath_src:图片保存路径
                 *@ left:水印图片相对于待加水印图片左边的距离(left,top若其中任意一个不传，则默认水印添加在右下方距离底部10px,距离右边10px的位置)
                 *@ top:水印图片相对于待加水印图片上方的距离
                AddWatermark(watermarkImg_src, sourceImg_src, savePath_src, left, top)


更新日志：
-------------
v1.2.2

        1. 修改方法：Error

v1.2.1

        1. 增加方法：formatTimeStamp、convers

v1.1.2

        1. CreateTopuSignatureSync在从文件获取密钥时，加了.trim()

v1.1.1

        1. 增加生成topu签名的同步方法

v1.0.5

        1. 通过jshint

v1.0.4

        1. CreateTopuSignature 的 处理ParamsJsonObj 代码块做了修改，之前写法不科学且有bug

v1.0.3

        1. 修改Request方法关于headers默认值的bug
        2. 增加全局变量subDomain_default // 默认二级域名，没找到主域名或无二级域名时使用
        3. CreateTopuSignature默认拼接params_filter和source

v1.0.2

        1. Request方法增加headers参数

v1.0.1

        1. 创建项目并发布到github
        2. 发布到npm：TopuNet-node-functions
