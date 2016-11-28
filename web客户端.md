## web客户端API

---

### 1. user


1. #### 登录
```
POST /auth
```

    Parameters
```javascript
{      
    username : "string",  
    password : "string"
}
```
    Response
```javascript
{
    status : "success"|"fail"
}
```
#### 2. 获取用户信息
```
GET /users/{username}
```
    Parameters
    ```javascript
    null
    ```
    Response
    ```javascript
    {
        username:"string",
        signUpDate:"yyyy-MM-dd",
        location:"string",
        avatar:"url",
        height:0,
        weight:0,
        gender:"male"|"female",
        BMI:1.2             //BMI健康指数
        description:"string",
        watchedCount:1,
        watchingCount:1,
        goal:0                //每日目标步数
    }
    ```
#### 3. 修改用户信息
```
put /users/{username}
```
Parameters
```javascript
{
    location:"string",
    avatar:"url",
    height:0,
    weight:0,
    gender:"male"|"female",
    description:"string",
    goal:0                //每日目标步数
}
```
Response
```
{
    username:"string",
    signUpDate:"yyyy-MM-dd",
    location:"string",
    avatar:"url",
    height:0,
    weight:0,
    gender:"male"|"female",
    BMI:1.2             //BMI健康指数
    description:"string",
    watchedCount:1,
    watchingCount:1,
    goal:0                //每日目标步数
}
```

    #### 3. 删除用户
>需要管理员权限

    ```
put /users/{username}
```
Parameters
```javascript
{
    location:"string",
    avatar:"url",
    height:0,
    weight:0,
    gender:"male"|"female",
    description:"string",
    goal:0                //每日目标步数
}
```
Response
```
{
    username:"string",
    signUpDate:"yyyy-MM-dd",
    location:"string",
    avatar:"url",
    height:0,
    weight:0,
    gender:"male"|"female",
    BMI:1.2,             //BMI健康指数
    description:"string",
    watchedCount:1,
    watchingCount:1,
    goal:0                //每日目标步数
}
```

### 2. statistics
1. #### 获得总体统计
```
GET /users/{username}/stat
```
Parameters
```javascript
null
```
Response
```javascript
{
    sportDays: 0      //运动总天数
    calories: 0,        //消耗卡路里
    meters: 0,          //运动距离
}
```
    #### 2. 获得运动数据
>默认为一周内的数据

    ```
GET /stat/{username}/sport
```
Parameters
```javascript
{
    intervalUnit:"day"|"hour",      //时间单位
    interval:0,                     //时间
}
```
Response
```javascript
{
    goal: 0,
    data:[
        {
            startTime: "yyyy-MM-dd hh:mm:ss",
            endTime: "yyyy-MM-dd hh:mm:ss",
            step :0,
            meters:0,
            intensity:0 //from 0 to 10
        }
    ]
}
```

    #### 3. 获得睡眠数据
>默认为一周内的数据

    ```
GET /stat/{username}/sleeping
```
Parameters
```javascript
{
    intervalUnit:"day"|"hour",      //时间单位
    interval:0,                     //时间
}
```
Response
```javascript
{
    goal: 0,        //正常睡眠时间
    data:[
        {
            startTime: "yyyy-MM-dd hh:mm:ss",
            endTime: "yyyy-MM-dd hh:mm:ss",
            deepHours:0,
            lightHours:0,
        }
    ]
}
```

### 3. watch
1. #### 获得关注用户
```
GET /users/{username}/watch
```
Parameters
```javascript
null
```
Response
```javascript
[
    {
        username:"string",
        signUpDate:"yyyy-MM-dd",
        location:"string",
        avatar:"url",
        height:0,
        weight:0,
        gender:"male"|"female",
        BMI:1.2             //BMI健康指数
        description:"string",
        watchedCount:"string",
        watchingCount:"string"
        goal:0                //每日目标步数
    }
]
```

    #### 2. 增加关注用户
```
POST /users/{username}/watch/{username}
```
Parameters
```javascript
null
```
Response
```javascript
204 no content
```

    #### 3. 删除关注用户
```
DELETE /users/{username}/watch/{username}
```
Parameters
```javascript
null
```
Response
```javascript
204 no content
```

### 4. activity
1. #### 获得动态
```
GET /users/{username}/activities
```
URL Parameters
```
typy: all|author        
//  all:自己和关注者动态
//  author:自己的动态
//  default: all
```
Parameters
```javascript
null
```
Response
```javascript
[
    {
        id:"string",
        content:"string",
        stars:0,
        datatime:"yyyy-MM-dd",
        author:{
            username:"string",
            location:"string",
            avatar:"url"
        }
    }
]
```

    #### 2. 发布动态
```
POST /users/{username}/activities
```
Parameters
```javascript
{
    content:"string"
}
```
Response
```javascript
{
    id:"string",
    content:"string",
    stars:0,
    datatime:"yyyy-MM-dd",
    author:{
        username:"string",
        location:"string",
        avatar:"url"
    }
}
```

    #### 3. 删除动态
>动态所有者和管理员拥有权限

    ```
DELETE /users/{username}/activities/{id}
```
Parameters
```javascript
null
```
Response
```javascript
{
    id:"string",
    content:"string",
    stars:0,
    datatime:"yyyy-MM-dd",
    author:{
        username:"string",
        location:"string",
        avatar:"url"
    }
}
```

### 5. competition

1. #### 获得用户的竞赛
```
GET /users/{username}/competitions
```
URL Parameters
```
type : all|member|owner     //default: all
```
Parameters
```javascript
null
```
Response
```javascript
[
    {
        id:"string",
        name:"string",
        description:"string",
        type:"single"|"team",       //个人竞赛,团队竞赛
        totalNumber:0,              //总人数
        currentNumber:0,            //当前人数
        startTime:"yyyy-MM-dd",
        endTime:"yyyy-MM-dd",
        score:0,                     //积分
        started:false,               //是否开始
        owner:{
            username:"string",
            location:"string",
            avatar:"url"
        }
    }
]
```

    #### 2. 创建竞赛
```
POST /users/{username}/competitions
```
Parameters
```javascript
{
    name:"string",
    description:"string",
    type:"single"|"team",       //个人竞赛,团队竞赛
    totalNumber:0,              //总人数
    startTime:"yyyy-MM-dd",
    endTime:"yyyy-MM-dd",
    score:0                     //积分
}
```
Response
```javascript
{
    id:"string",
    name:"string",
    description:"string",
    type:"single"|"team",       //个人竞赛,团队竞赛
    totalNumber:0,              //总人数
    currentNumber:0,            //当前人数
    startTime:"yyyy-MM-dd",
    endTime:"yyyy-MM-dd",
    score:0,                     //积分
    started:false,               //是否开始
    owner:{
        username:"string",
        location:"string",
        avatar:"url"
    }
}
```

    #### 3. 删除竞赛
>动态所有者和管理员拥有权限

    ```
DELETE /users/{username}/competitions/{id}
```
Parameters
```javascript
null
```
Response
```javascript
204 no content
```

    #### 4. 参与竞赛
```
POST /competitions/{id}/members/{username}
```
Parameters
```javascript
null
```
Response
```javascript
204 no content
```

### 6. search

1. #### 搜索用户
```
GET /search/users
```
URL Parameters
```
key : string    //关键字
```
Parameters
```javascript
null
```
Response
```javascript
[
    {
        username:"string",
        signUpDate:"yyyy-MM-dd",
        location:"string",
        avatar:"url",
        height:0,
        weight:0,
        gender:"male"|"female",
        BMI:1.2             //BMI健康指数
        description:"string",
        watchedCount:"string",
        watchingCount:"string"
        goal:0                //每日目标步数
    }
]
```
