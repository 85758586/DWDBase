
Android 编码规范
=======

#### 说明：
- 红色条目代表需要执行，黑色条目代表建议执行；
- 已有代码，在修改到该处功能时再更改；
- 新增代码，需执行此规范；
- 为保持和已有代码兼容，本规范对其他常见规范做了大量的取舍；
		  
## 一、工程规范
---------------

目标：保持代码的整洁。
原则：随时随地处理产生提示的代码。

### `1.1 AndroidStudio的xlint工具对一些常见的问题给出了提示，需按提示完成修改，比如：`

`- 无用的import需要去掉；`

`- XML空标签直接是用“/>”结尾；`

`- 成员变量可以转换为局部变量；`

`- 变量没有被使用到；`

`- 拼写错误，非拼写错误添加到词典；`

`- 等等。。。。。。`

### 1.2 代码大部分能通过CheckStyle检查（进阶）

### 1.3 代码大部分能通过FindBugs检查  （最高）

## 二、文件规范
---------------

目标：保持代码风格统一

### `2.1 空行：`
`- 方法之间空一行；`

`- 类的变量定义开始处空一行；`

`- 不同修饰符的变量间空一行；`

`- 执行一个功能的执行语句之间不空行，执行不同功能的语句间空一行；`

`- 变量定义和方法实现之间空两行；`

`- 去掉没用的空行。`

例如：
```
         public Class User {
                                                      //常量定义开始，空一行
            public static final int LENGTH = 10;
                                                      //常量作用域不同，空一行
            private static final int sex = 0;       
                                                      //变量定义开始，空一行
            public String userName;
                                                      //变量作用域不同， 空一行
            private String password;
            
                                                      //方法区块开始， 空两行
            @Override
            public void onCreate(){
            
            }
                                                      //方法之间，空一行
            @Override
            public void onResume(){
            }
        
        }
```

### `2.2 一个类不超过2000行`

### `2.3 匿名类不超过30行`
例如： 
```
someButton.setOnClickListener(new OnClickListener {
    ...//some code, 不超过30行
})
```

### `2.4 方法不超过40行`

### `2.5 纯工具类放到Base或Utils下`

### `2.6 代码顺序：`
    
	@Bind(R.layout.id)                       //控件
	public static final…                     //常量
	private static final…                    //常量
	public …                                 //变量
	private …                                //变量
	@Override public void onCreate() {}      //生命周期方法
	@Override public void onPostCreate() {}
	public void doSomething() {}             //自定义共有方法
	private void doSomething() {}            //自定义私有方法
	
## 三、命名规范
---------------
目标：保持代码风格的统一和易读性。
原则：类名、方法名、字段名要能体现出实际意义，避免出现生僻词，命名可以适当的长一些以说明含义。

### `3.1 驼峰式命名准则`
   例如： userName; 
   String getUserName();

### `3.2类名`
	xxxActivity	            必须和功能相关
	xxxService
	xxxReceiver
	xxxFragment
	xxxListener
	xxxCallBack
	xxxUtils
	xxxHelper
	xxxTools                相关工具类的定义
	xxxAdapter              和Activity和Fragment绑定，一般保持一致
	
### `3.3 XML中的控件ID：`

`- 控件名称缩写_逻辑名，例如：btn_upload`

`- 全部小写，中间加下划线分割`

`- 缩写列表：`
    
    控件名称	           缩写    
	TextView                 tv
	EditText                 et
	ImageView                iv
	Button                   btn
	LinearLayout             ll
	SwipeRefreshLayout       spl
	RecyclerView             rv
	
	
原则上采用该控件单词首字母作为缩写

### `3.4 类中的控件变量：`
`用控件名称缩写加逻辑名的形式，例如：btnUpload;`

### `3.5 常量（Constants）全部大写,采用下划线命名法.例如：MIN_WIDTH`

## 四、注释规范
-------------
原则：增强代码的易读性。

### `4.1 去掉注释掉的代码`
程序中不要保留已经注释掉的代码，如果确实有重要作用，不适于删除的，可以打个TODO标签，方便查找。

### `4.2 每个类文件开头包含不少于30字的注释，格式如：`
```
/**
 * @Description：此类的功能说明
 * Created by who on 2015/5/28.
 */
```
### `4.3 工具类中的方法要加注释，格式如：`
```
  /**  
  * 方法概述 
  * @param  说明参数含义
    * @return 说明返回值含义 
  * @throws IOException 说明发生此异常的条件 
  * @throws NullPointerException 说明发生此异常的条件
   */
```

### `4.4关键字段后附加注释，说明该字段的作用  ,格式如：`
```
private Map<String, String> requestMap = new HashMap<>();             //记录数据有变更的cell，用来构建POST参数体
private Map<String,TextView> widgetMap = new HashMap<>();          //记录当前点击的控件，用来更改当前cell的显示内容
```
## 五、注意事项
---------------

### 5.1 Log类统一封装，注意Log的等级，调试信息不要使用e
log等级可以方便我们进行程序的调试和查找错误，因此，不要定义log等级不要过于随意，要根据log的重要性，使用相应的等级。

### 5.2 界面端catch的异常，产品有没有要求弹出提示的，打Log.e
        try {
            if ("start_time".equals(key)) {
                start = finalDMin;
                end = mSelectEndDate.after(finalDMax);
            } else {
                start = mSelectStartDate.before(finalDMin);
                end = finalDMax;
            }
        }catch (ParseException e){
            ...   //other code
            
            Log.e("date time compute error");    //错误信息
        }

### 5.3 实体类使用getter和setter。如：

    class User {
        private String userName;
        private String password;
        
        public String getUserName(){
            return userName;
        }
        
        public void setUserName(String userName){
            this.userName = userName;
        }
        
        public String getPassWord(){
            return passWord;
        }
        
        public void setPassword(String password){
            this.password = password;
        }
    }

### 5.4 Adapter一般不要在网络返回结果时重新创建
    @Override
    public void onSuccess(EnvelopeList<ItemTitled> data) {
        ...//other code
        SomeAdapter adapter = new SomeAdapter();
        listView.setAdapter(adapter);
    }  //这是在我们工程中会见到的一种不太好的用法

### 5.5 可以不使用异步任务的情况就不用异步任务
爱抢购的代码中使用了较多的异步任务，会造成代码低效，新增加的代码要酌情使用。
### 5.6 尽量使用RecyclerView替代ListView
随着android系统版本的更新，ListView终将退出历史的舞台。使用系统推荐的RecyclerView可以避免将来进行大范围的升级。
