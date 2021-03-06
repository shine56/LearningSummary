```
apply plugin: 'org.greenrobot.greendao'
```

```
//数据库
implementation 'org.greenrobot:greendao:3.2.2'
```
```
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }

        /**
         * 对greendao的generator生成文件进行配置
         */
        greendao {
            schemaVersion 1//数据库版本号
            daoPackage 'com.study.help.db.dao'//设置DaoMaster、DaoSession、Dao包名
            targetGenDir 'src/main/java'//设置DaoMaster、DaoSession、Dao目录
            generateTests false       //设置自动生成单元测试用例
            targetGenDirTests "src/androidTest/java"       //设置生成单元测试目录
        }
    }
```    
```
GreenDao数据库升级数据迁移

allprojects {
    repositories {
        google()
        jcenter()
        maven {url"http://jitpack.io"}
    }
}

//数据库升级数据迁移
implementation 'com.github.yuweiguocn:GreenDaoUpgradeHelper:v2.0.1'
```

创建实体类，生成dao文件
```
@Entity
public class dayStep {
    @Id
    private long id;
    private String date;
    private int step;
    private Long sportId;
    @ToOne(joinProperty = " sportId")
    private SportInfo sportInfo;//关系表
}

```
1.@Entity 用于标识这是一个需要GreenDao帮我们生成代码的bean</br>
2.@Id 标明主键，主键Long型，可以通过@id(autoincrement = true)设置自增长，括号里可以指定是否自增</br>
3.@Property 设置一个非默认关系映射所对应的列名，默认是使用字段名，例如：@Property(nameInDb = "name")</br>
4.@NotNull 非空</br>
5.@Transient 标识这个字段是自定义的不会创建到数据表里</br>

关系注解
---

@ToOne 是将自己的一个属性与另一个表建立关联</br>
@ToMany 定义与多个实体对象的关系（的属性referencedJoinProperty，类似于外键约束）</br>
@JoinProperty 对于更复杂的关系，可以使用这个注解标明属性的源属性

索引注解
---

@Index: 使用@Index作为一个属性来创建一个索引，通过name设置索引别名，也可以通过unique给索引添加约束</Br>
@Unique: 向数据库添加一个唯一的约束
