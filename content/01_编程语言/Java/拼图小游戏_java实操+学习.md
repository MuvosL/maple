# 1 主界面分析

## 1.1 JFrame
J：Java
Frame：窗体/界面
我们所有要展示的文字以及图片都是在这个窗体上的
![[Pasted image 20251107202349.png]]
## 1.2 JMenuBar
菜单
最上层的菜单
![[Pasted image 20251107202432.png]]
![[Pasted image 20251107202628.png]]
## 1.3 JLabel
管理文字和图片的容器
相当于前端中的div
![[Pasted image 20251107202800.png]]

上面的这些东西都可以称为组件

# 2 创建主界面

到idea中创建一个宽603像素，高680像素的游戏主界面
到idea中创建一个宽488像素，高430像素的登录界面
到idea中创建一个宽488像素，高500像素的注册界面


**先创建一个测试类，看看效果**
```java
package com.moyeah.ui;  
  
import javax.swing.*;  //导包
  
public class Test {  
    public static void main(String[] args) {  
        //1.创建一个游戏的主界面  
        //JavaBean类描述
        JFrame gameframe=new JFrame();  //创建一个对象
        gameframe.setSize(603,680);  //调用方法设置窗口大小，单位为像素
        gameframe.setVisible(true);  //窗口默认事隐藏的，所以我们要对其设置一下
    }  
}

```
![[Pasted image 20251107204145.png]]

三个都创建好运行后是这样一个效果
```java
//1.创建一个游戏的主界面  
JFrame gameframe=new JFrame();  
gameframe.setSize(603,680);  
gameframe.setVisible(true);  
  
//2.创建一个登陆界面  
JFrame loginframe=new JFrame();  
loginframe.setSize(488,430);  
loginframe.setVisible(true);  
  
//3.创建一个注册界面  
JFrame registerframe=new JFrame();  
registerframe.setSize(488,500);  
registerframe.setVisible(true);
```

![[Pasted image 20251107204408.png]]

在idea中，选中类或方法，ctlr+B可向上跟进，一直找到它的爹
就拿那个展示的方法来说吧，它的祖宗是show方法，也就是说我们直接调用show方法，效果是一样的
```java
gameframe.show();
```
但这个方法是过时方法，可用，但不推荐


---
## 2.1 游戏主界面

**先以其中办一张图片为例，实现玩游戏的基本功能**

### 2.1.1 窗口初始化

```java
package com.moyeah.ui;  
  
import javax.swing.*;  
  
public class GameJFrame extends JFrame {  
  
  
    public GameJFrame() {  
        //设置界面的宽高  
        this.setSize(603,680);  
  
        //设置界面的标题  
        this.setTitle("拼图单机版 v1.0");  
  
        //设置界面置顶  
        this.setAlwaysOnTop(true);  
  
        //设置界面居中  
        this.setLocationRelativeTo(null);  
  
        //设置关闭模式  
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  
        
        //让窗口能显示出来  
        this.setVisible(true);  
    }  
}
```

```java
package com.moyeah.ui;  
  
import javax.swing.*;  
  
public class LoginJFrame extends JFrame {  
  
  
  
    public LoginJFrame() {  
        //宽,高  
        this.setSize(488,430);  
  
        //设置界面的标题  
        this.setTitle("拼图登录界面");  
  
        //设置界面置顶  
        this.setAlwaysOnTop(true);  
  
        //设置界面居中  
        this.setLocationRelativeTo(null);  
  
        //设置关闭模式  
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  
  
  
        //设置可见  
        this.setVisible(true);  
    }  
}
```

```java
package com.moyeah.ui;  
  
import javax.swing.*;  
  
public class RegisterJFrame extends JFrame {  
  
  
    public RegisterJFrame() {  
        //设置宽、高  
        this.setSize(488,500);  
  
        //设置界面的标题  
        this.setTitle("拼图注册界面");  
  
        //设置界面置顶  
        this.setAlwaysOnTop(true);  
  
        //设置界面居中  
        this.setLocationRelativeTo(null);  
  
        //设置关闭模式  
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  
  
        //设置可见  
        this.setVisible(true);  
    }  
}
```

### 2.1.2菜单制作

JMenuBar：整个菜单
JMenu：每个选项
JMenuItem：每个条目

这个很像前端的盒子
![[Pasted image 20251107214548.png]]

![[Pasted image 20251107214838.png]]

```java
//初始化菜单  
//创建整个的菜单对象  
JMenuBar jMenuBar = new JMenuBar();  
  
//创建菜单上的两个选项的对象（功能 关于我们）  
JMenu functionJMenu = new JMenu("功能");  
JMenu abdoutJMenu = new JMenu("关于我们");  
  
//创建选项下买你的条目对象  
JMenuItem replayItem = new JMenuItem("重新游戏");  
JMenuItem reLoginItem =  new JMenuItem("重新登录");  
JMenuItem closeItem = new JMenuItem("关闭游戏");  
  
JMenuItem accountItem = new JMenuItem("公众号");  
  
//将每一个选项下的条目添加到选项当中  
functionJMenu.add(replayItem);  
functionJMenu.add(reLoginItem);  
functionJMenu.add(closeItem);  
  
abdoutJMenu.add(accountItem);  
  
//将菜单里面的两个选项添加到菜单当中  
jMenuBar.add(functionJMenu);  
jMenuBar.add(abdoutJMenu);  
  
//给整个界面设置菜单  
this.setJMenuBar(jMenuBar);
```
![[Pasted image 20251108112112.png]]
![[Pasted image 20251108112124.png]]
构造方法中的东西太多了，所以我们选择将其分成初始化菜单部分和初始化界面部分，分别选中对应区块代码
`ctrl + alt +M` ，即可抽取方法
![[Pasted image 20251108112751.png]]

### 2.1.3 添加图片
图片对应的类是ImageIcon,但是其对象不能直接放到JFrame中，要为其添加JLabel管理区域中
JLable可以管理图片、文字，在管理图片的时候可以对图片的宽、高、位置、边框进行设置

![[Pasted image 20251108114015.png]]
最基本的添加图片添加
```java
//创建一个图片ImageIcon的对象  
ImageIcon icon = new ImageIcon("D:\\MINE\\projects\\java_projects\\puzzlegame\\puzzlegame\\image\\animal\\animal3\\3.jpg");  
  
//创建一个JLable对象，管理容器  
JLabel jLabel = new JLabel(icon);  
  
//把管理容器添加到界面中  
this.add(jLabel);
```
![[Pasted image 20251108115119.png]]

坐标
![[Pasted image 20251108115613.png]]
图片的位置即为图片左上角点的位置，每个小图片的宽高都为105像素

![[Pasted image 20251108120451.png]]
![[Pasted image 20251108120504.png]]
```java
private void initJFrame() {  
    ......
  
    //取消默认的居中位置，只有取消了才会按照XY轴的形式添加组件  
    this.setLayout(null);  
}
```
```java
private initImage(){
    ......
    //先获取到这个隐藏的容器，再进行添加
    this.getContentPane().add(jLabel1);
    
}
```
![[Pasted image 20251108121446.png]]
这个隐藏容器的对象在创建JFrame时是会自己创建的，我们在翻看其源码时就可以发现，所以我们直接通过get方法去获取即可
![[Pasted image 20251108121833.png]]

![[Pasted image 20251108121810.png]]

先做一个添加一个完整图片的示例，这里用到了循环
```java
private void initIamge() {  
    int number = 1;  
    for (int i = 0; i < 4; i++) {  
        for (int j = 0; j < 4; j++) {  
            //创建一个JLabel对象（管理容器）  
            JLabel jLabel = new JLabel(new ImageIcon("D:\\MINE\\projects\\java_projects\\puzzlegame\\puzzlegame\\image\\animal\\animal3\\" + number + ".jpg"));  
  
            //指定图片位置  
            jLabel.setBounds(105 * j, 105 * i,105,105 );  
  
            //把管理容器添加到界面中  
            this.getContentPane().add(jLabel);  
  
            //添加一次number自增  
            number++;  
        }  
    }  
}
```
![[Pasted image 20251108124741.png]]

### 2.1.4 打乱图片
我们可以给每个小图片一个对应标号，我们对标号进行打乱
标号我们采用二维数组
先来看看怎么对一个普通的二维数组进行打乱

```java
public static void main(String[] args) {  
    //需求：  
    //把一个一维数组中的数据：0~15 打乱顺序  
    //然后按照4个一组的方式添加到二维数组当中  
  
    //1.定义一个一一维数组  
    int[] tempArr = {0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15};  
    //2.打乱数组中数据的顺序  
    //遍历数组，得到每一个元素，拿着每一个元素跟随机索引上的数据进行交换  
    Random random = new Random();  
    for (int i = 0; i < tempArr.length; i++) {  
        //获取随即索引  
        int index = random.nextInt(tempArr.length);  
        //拿着遍历到的每一个数据，跟随机索引上的数据进行交换  
        int temp = tempArr[i];  
        tempArr[i] = tempArr[index];  
        tempArr[index] = temp;  
    }  
    //3.遍历数组  
    for (int i = 0; i < tempArr.length; i++) {  
        System.out.print(tempArr[i] + " ");  
    }  
    System.out.println();  
    //4.创建一个二维数组  
    int[][] data = new int[4][4];  
    //5.给二维数据添加数据  
    for (int i = 0; i <tempArr.length; i++) {  
        data[i / 4][i % 4] = tempArr[i];  
    }  
    for (int i = 0; i < data.length; i++) {  
        for (int j = 0; j < data[i].length; j++) {  
            System.out.print(data[i][j] + " ");  
        }  
        System.out.println();  
    }  
}
```

![[Pasted image 20251108130956.png]]
现在我们再来更新一下代码
```java
public class GameJFrame extends JFrame {  
  
    //创建一个二维数组  
    //目的：用来管理数据  
    //加载图片的时候，会根据二维数组中的数据进行加载  
    int[][] data = new int[4][4];  
  
    public GameJFrame() {...}
    
    ......
}
```

```java
//初始化图片  
private void initIamge() {  
  
    for (int i = 0; i < 4; i++) {  
        for (int j = 0; j < 4; j++) {  
            //获取当前要加载图片的序号  
            int num = data[i][j];  
            //创建一个JLabel对象（管理容器）  
            JLabel jLabel = new JLabel(new ImageIcon("D:\\MINE\\projects\\java_projects\\puzzlegame\\puzzlegame\\image\\animal\\animal3\\" + num + ".jpg"));  
  
            //指定图片位置  
            jLabel.setBounds(105 * j, 105 * i,105,105 );  
  
            //把管理容器添加到界面中  
            this.getContentPane().add(jLabel);  
  
        }  
    }  
}
```
![[Pasted image 20251108132512.png]]
![[Pasted image 20251108132527.png]]
可以看到我们每次打开的图片都被成功打乱了，且顺序都是不一样的

### 2.1.5 事件
事件是可被组件识别的操作
当你对组件干了某件事情之后，就会执行对应的代码

- 事件源：按钮 图片 窗体
- 事件：某些操作
    如：鼠标单击，鼠标划入...
- 绑定监听：当事件源上发生了某个事件，则执行某段代码
![[Pasted image 20251108133322.png]]
键盘监听:理解为绑定一个快捷键
鼠标键监听：例如单击，双击，右键之类的
动作监听：鼠标只有单击，键盘只有空格

**动作监听**

测试一下
```java
//创建一个按钮对象  
JButton jtb = new JButton("点我");  
//设置位置和宽高  
jtb.setBounds(0,0,100,50);  
//给按钮添加动作监听  
//jtb：组件对象，表示要给哪个组件添加事件  
//addActionListener：表示要给按钮添加哪个事件监听  
//参数：表示事件被触发后要执行的代码  
jtb.addActionListener(new MyActionListener());
```
查看一下源码，选中`addActionListener`
他是要传入这么一个类型的
![[Pasted image 20251108135003.png]]
接着选中`addActionListener`，继续查看
它是一个接口
![[Pasted image 20251108135110.png]]
所以我们要往addActionListener里面传入一个ActionListener接口的实现类
```java
public class MyActionListener implements ActionListener {  
  
    @Override  
    public void actionPerformed(ActionEvent e) {  
        System.out.println("被点击了");  
    }  
}
```
把按钮添加到界面中
```java
frame.getContentPane().add(jtb);
```
下面是一个效果图
我点击了六次按钮，它那串代码就执行了五次
![[Pasted image 20251108135856.png]]

**写法一**
这时候，当一个接口的实现类只被用到一次时候，我们就没有必要再去单独定义一个类了。此时我们就可以使用匿名内部类的形式简化代码
```java
jtb.addActionListener(new ActionListener(){  
    @Override  
    public void actionPerformed(ActionEvent e){  
        System.out.println("不要点我");  
    }  
});

```
匿名类是`ActionListener（）`后面那个大括号中的东西，后面的匿名类实现了`ActionListener`接口，前面的`new`，实例化了后面的匿名类。当前addActionListener的参数整体就是匿名内部类的对象

**写法二**
我们让当前这个界面类去实现监听接口
下面是示例代码


```java
public class MyJFrame extends JFrame implements ActionListener {  
  
    JButton jtb1 = new JButton("点我");  
    JButton jtb2 = new JButton("再点我");  
    public MyJFrame() {  
        ......
  
        jtb1.setBounds(0,0,100,50);  
        jtb1.addActionListener(this);  
        
  
        jtb2.setBounds(100,0,100,50);  
        jtb2.addActionListener(this);  
  
        this.getContentPane().add(jtb1);  
        this.getContentPane().add(jtb2);  
        
        ......
  
    }  
  
    @Override  
    public void actionPerformed(ActionEvent e) {  
        //对当前按钮进行判断  
  
        //获取当前被操作的那个按钮对象  
        Object source = e.getSource();  
        if (source == jtb1) {  
            jtb1.setSize(200,200);  
        }else if (source == jtb2) {  
            Random r = new Random();  
            jtb2.setLocation(r.nextInt(500),r.nextInt(500));  
        }  
  
    }  
}
```
拿`jtb1.addActionListener(this);`来说明一下

`this`是什么意思呢，指的是本类对象

你当前`MyFrame`这个类实现了`ActionListener`接口，并在下面重写了接口中的`actionPerformed`方法。我们`addActionListener`方法中本来传入的是接口的实现类的对象，它会去调用对象中的`actionPerformed`方法。现在你这个`MyFrame`就是那个接口的实现类，直接使用this在本类内，效果是和之前那种一样的
![[Pasted image 20251108145801.png]]
**其他事件的使用方式跟上面类似，如果不会用，ctrl+B查看源码，查看api帮助文档**

### 2.1.6 美化界面

对图片区域位置进行偏移
![[Pasted image 20251108152322.png]]
添加背景图片
```java
private void initIamge() {  
    ......
    //添加背景图片  
    JLabel background = new JLabel(new ImageIcon("D:\\MINE\\projects\\java_projects\\puzzlegame\\puzzlegame\\image\\background.png"));  
    background.setBounds(40, 40,508,560 );  
    //把背景图片添加到界面当中  
    this.getContentPane().add(background);  
}
```
先加载的图片在上方，后加载的图片在下方

为图片添加边框
```java
//指定图片位置  
jLabel.setBounds(105 * j + 83, 105 * i + 134,105,105 );  
  
//给图片添加边框  
//0:让图片凸出  
//1：让图片凹陷  
jLabel.setBorder(new BevelBorder(1));
```

优化路径
使用相对路径
```java
//添加背景图片  
JLabel background = new JLabel(new ImageIcon("..\\puzzlegame\\image\\background.png"));
```

### 2.1.7 业务逻辑实现
#### 移动实现
**添加键盘监听事件**
![[Pasted image 20251108155820.png]]![[Pasted image 20251108155831.png]]
记录空白图片的位置
```java
//记录空白图片的位置  
int x = 0;  
int y = 0;

......

for (int i = 0; i <tempArr.length; i++) {  
    if(tempArr[i]==0){  
        x = i / 4;  
        y = i % 4;  
    }else {  
        data[i / 4][i % 4] = tempArr[i];  
    }  
}
```
![[Pasted image 20251108160507.png]]

**向上移动举例**
```java
这个是在keyReleased()方法中
//向上移动  
//逻辑：将空白方块下方的数字往上移动  
//x,y 空白方块  
//x+1，y 空白下方方块  
data[x][y] = data[x+1][y];  
data[x+1][y] = 0;  
x++;  
  
//调用方法，重新加载图片  
initIamge();
```
这里要对initImage()方法进行修改一下
```java
private void initIamge() {  
    //清除已有图片  
    this.getContentPane().removeAll();  
    ......
    
    //刷新界面  
    this.getContentPane().repaint();  
}
```
完整移动代码,做了边界处理
```java
public void keyReleased(KeyEvent e) {  
    //对上下左右进行判断  
    //左：37 上：38 右：39 下：40  
   int code = e.getKeyCode();  
   if(code == 37){  
       //向左移动  
  
       //数组越界判断,即空白方块已到最右边  
       if(y == 3) {  
           return;  
       }  
  
       //逻辑：将空白方块右方的数字往上移动  
       //x,y 空白方块  
       //x，y+1 空白下方方块  
       data[x][y] = data[x][y + 1];  
       data[x][y + 1] = 0;  
       y++;  
  
       //调用方法，重新加载图片  
       initIamge();  
  
   }else if(code == 38){  
       //向上移动  
  
       //数组越界判断,即空白方块已到底部  
       if(x == 3) {  
           return;  
       }  
  
       //逻辑：将空白方块下方的数字往上移动  
       //x,y 空白方块  
       //x+1，y 空白下方方块  
       data[x][y] = data[x + 1][y];  
       data[x + 1][y] = 0;  
       x++;  
  
       //调用方法，重新加载图片  
       initIamge();  
  
   }else if(code == 39){  
       //数组越界判断,即空白方块已到最左边  
       if(y == 0) {  
           return;  
       }  
  
       //向右移动  
       data[x][y] = data[x][y - 1];  
       data[x][y - 1] = 0;  
       y--;  
  
       //调用方法，重新加载图片  
       initIamge();  
  
   }  
   else if(code == 40){  
       //数组越界判断,即空白方块已到顶部  
       if(x == 0) {  
           return;  
       }  
       //向下移动  
       data[x][y] = data[x - 1][y];  
       data[x - 1][y] = 0;  
       x--;  
  
       //调用方法，重新加载图片  
       initIamge();  
  
   }  
  
  
}
```

#### 查看完整图片
```java
//按下不松时会调用这个方法  
@Override  
public void keyPressed(KeyEvent e) {  
    int code = e.getKeyCode();  
    if (code == 65) {  
        //把界面中所有图片全部删除  
        this.getContentPane().removeAll();  
  
        //加载完整图片  
        JLabel all = new JLabel(new ImageIcon("..\\puzzlegame\\image\\animal\\animal3\\all.jpg"));  
        all.setBounds(83,134,420,420);  
        this.getContentPane().add(all);  
  
        //添加背景图片  
        JLabel background = new JLabel(new ImageIcon("..\\puzzlegame\\image\\background.png"));  
        background.setBounds(40, 40,508,560 );  
        //把背景图片添加到界面当中  
        this.getContentPane().add(background);  
  
        //刷新界面  
        this.getContentPane().repaint();  
    }  
  
}
```
再去松开时的方法中多加一个判断
```java
else if(code == 65) {  
    initIamge();  
}
```
这样就能完成，按住时，展现完整图片，送开时回到游戏
#### 作弊码
直接，在松开事件中
![[Pasted image 20251108171853.png]]
#### 判断胜利
- 先定义一个正确的二维数组win
- 加载图片前，判断二维数组和win是否相同
- 如果相同，展示胜利，否则，不展示
只展示方法
```java
public boolean victory() {  
    for (int i = 0; i < data.length; i++) {  
        for (int j = 0; j < data[i].length; j++) {  
            if(data[i][j] != win[i][j]) {  
                return false;  
            }  
        }  
    }  
    return true;  
}
```
还需要再按键的那几个方法中加上判断
```java
//判断游戏是否胜利，如果胜利，此方法需要直接结束，不能再执行下面的移动代码了  
if(victory()){  
    return;  
}
```
#### 计步
![[Pasted image 20251108173137.png]]

然后再每个负责移动的代码块中添加`step++`
#### 重新开始
- 给重新游戏绑定点击事件
- 重新打乱二维数组中的数字
- 加载图片
- 计步器清零

给条目绑定事件
![[Pasted image 20251108174002.png]]



#### 结束游戏

将初始化数据的代码进行更改
![[Pasted image 20251108175401.png]]
![[Pasted image 20251108175430.png]]


#### 关于我们

将JLabel放到JDialog中
```java
//创建一个弹框对象  
JDialog jDialog = new JDialog();  
//创建一个管理图片的容器对象  
JLabel jLabel = new JLabel(new ImageIcon("..\\puzzlegame\\image\\about.png"));  
//设置位置和宽高  
jLabel.setBounds(0,0,614,590);  
//把图片添加到弹框中  
jDialog.getContentPane().add(jLabel);  
//给弹框设置大小  
jDialog.setSize(614,590);  
//让弹框置顶  
jDialog.setAlwaysOnTop(true);  
//让弹框居中  
jDialog.setLocationRelativeTo(null);  
//弹框不关闭则无法操作下面的界面  
jDialog.setModal(true);  
//让弹框显示  
jDialog.setVisible(true);
```

### 2.1.8 功能完善
可以看到我们目前的游戏只有这么一张图片，而且文件夹中的那么多种类的图片都没有用到，接下来我们来完成这些功能

学到的是JMenuBar下面JMenu，JMenu下面放JMenuItem，那么现在选择图片已经是JMenuItem，我还想在选择图片下面放动物、女孩、运动，该怎么办呢，这里我查到的是
JMenu可以往JMenu里放
所以我选择将选择图片由原来的JMenuItem改为JMenu，将选择图片添加到功能这个JMenu中

```java
JMenu selectionJMenu = new JMenu("图片选择");  
    //图片选择下面的几种选项  
    JMenuItem animalItem = new JMenuItem("动物");  
    JMenuItem girlItem = new JMenuItem("女孩");  
    JMenuItem sportItem = new JMenuItem("运动");
```

```java
//将每一个选项下的条目添加到选项当中  
functionJMenu.add(selectionJMenu);  
    selectionJMenu.add(animalItem);  
    selectionJMenu.add(girlItem);  
    selectionJMenu.add(sportItem);
```

接下来就是关于图片怎么更换了
我写了一个接口，负责图片路径这块，我统一采用的相对路径
```java
ackage com.moyeah.dao;  
  
public interface ImageAboutPath {  
    void setImageNo(int imageNo);  
    void setPath(String Path);  
    int getImageNo();  
    String getPath();  
}
```
为什么我用了个接口呢，这里就体现了多态
我还写了三个接口的实现类，分别负责Animal、Gir、Sport类图片的路径
这里拿Animal来举例
下面是这个实现类的代码
```java
package com.moyeah.dao;  
import java.util.*;  
  
public class Animal implements ImageAboutPath {  
    Random rand = new Random();  
  
    final private int imageNumber = 8;  
    private int imageNo;  
    private String Path;  
  
    public Animal() {  
        setImageNo(rand.nextInt(imageNumber) + 1);  
        setPath("..\\puzzlegame\\image\\animal\\animal" + getImageNo() + "\\");  
    }  
  
  
    public void setImageNo(int imageNo) {  
        this.imageNo = imageNo;  
    }  
    public void setPath(String allPath) {  
        this.Path = allPath;  
    }  
    public int getImageNo() {  
        return imageNo;  
    }  
    public String getPath() {  
        return Path;  
    }  
  
}
```

我在GameFrame中的图片资源定义是这样写的
```java
//定义初始图片资源  
ImageAboutPath gameImage = new Animal();

......
//加载图片部分是这样写的
//创建一个JLabel对象（管理容器）  
JLabel jLabel = new JLabel(new ImageIcon(gameImage.getPath() + num + ".jpg"));

//还有下面的作弊器
JLabel all = new JLabel(new ImageIcon(gameImage.getPath() + "all.jpg"));

//在给那三个子条目绑定鼠标监听事件后
else if(obj == animalItem){  
  
    //更改图片类型  
    gameImage = new Animal();  
  
    //计步器清零  
    step = 0;  
  
    //再次打乱二维数组中的数据  
    initData();  
  
    //重新加载图片  
    initIamge();  
  
}else if(obj == girlItem){  
    gameImage = new Girl();  
    step = 0;  
    initData();  
    initIamge();  
}else if(obj == sportItem){  
    gameImage = new Sport();  
    step = 0;  
    initData();  
    initIamge();  
}
```
这样写的话，我游戏主界面中只管使用的是图片的信息，而不用管具体是哪个，具体是哪个由后面的对象决定
我还在重新游戏中添加了个小判断，如果胜利的话重新游戏就要更换图片但不更换图片类型
```java
//如果当前关卡已经胜利，重新游戏即更换当前图片，但不更换大类  
if(victory()){  
    if(gameImage instanceof Animal){  
        gameImage = new Animal();  
    }  
    if(gameImage instanceof Girl){  
        gameImage = new Girl();  
    }  
    if(gameImage instanceof Sport){  
        gameImage = new Sport();  
    }  
}
```

## 2.2 注册界面
我直接摆代码了
我这儿还弄了个User类，里面放着用户的信息和添加用户到users.txt文件的功能和检验用户是否已存在还有验证用户是否登录的功能，这个验证用户登录会在LoginJFrame中有用到

![[Pasted image 20251110211628.png]]

```java
package com.moyeah.user;  
  
import java.io.*;  
import java.nio.file.Files;  
import java.nio.file.Paths;  
import java.nio.file.StandardOpenOption;  
  
public class User {  
    private String username;  
    private String password;  
  
    public User(String username, String password) {  
        this.username = username;  
        this.password = password;  
    }  
  
    public String getUsername() {  
        return username;  
    }  
  
    public void setUsername(String username) {  
        this.username = username;  
    }  
  
    public String getPassword() {  
        return password;  
    }  
  
    public void setPassword(String password) {  
        this.password = password;  
    }  
  
    public boolean addUser() {  
        String userInformation = this.username + "," + this.password + "\n";  
  
        try {  
            // 确保目录存在  
            File file = new File("..\\puzzlegame\\user\\users.txt");  
            File parentDir = file.getParentFile();  
            if (parentDir != null && !parentDir.exists()) {  
                parentDir.mkdirs();  
            }  
  
            Files.write(Paths.get("..\\puzzlegame\\user\\users.txt"), userInformation.getBytes(),  
                    StandardOpenOption.CREATE, StandardOpenOption.APPEND);  
            return true;  
  
        } catch (IOException e) {  
            System.err.println("写入用户文件失败: " + e.getMessage());  
            return false;  
        }  
    }  
  
    /**  
     * 检查用户名是否已存在  
     */  
    public static boolean isUsernameExists(String username) {  
        File file = new File("..\\puzzlegame\\user\\users.txt");  
  
        if (!file.exists()) {  
            return false;  
        }  
  
        try (BufferedReader reader = new BufferedReader(new FileReader(file))) {  
            String line;  
            while ((line = reader.readLine()) != null) {  
                String[] parts = line.split(",", 2);  
                if (parts.length > 0 && parts[0].equals(username.trim())) {  
                    return true;  
                }  
            }  
        } catch (IOException e) {  
            System.err.println("读取用户文件失败: " + e.getMessage());  
        }  
  
        return false;  
    }  
  
    /**  
     * 验证用户登录  
     */  
    public static boolean validateUser(String username, String password) {  
        File file = new File("..\\puzzlegame\\user\\users.txt");  
  
        if (!file.exists()) {  
            return false;  
        }  
  
        try (BufferedReader reader = new BufferedReader(new FileReader(file))) {  
            String line;  
            while ((line = reader.readLine()) != null) {  
                String[] parts = line.split(",", 2);  
                if (parts.length == 2 && parts[0].equals(username)) {  
                    return parts[1].equals(password);  
                }  
            }  
        } catch (IOException e) {  
            System.err.println("读取用户文件失败: " + e.getMessage());  
        }  
  
        return false;  
    }  
}
```

```java
package com.moyeah.ui;  
  
import com.moyeah.user.User;  
  
import javax.swing.*;  
import java.awt.event.MouseEvent;  
import java.awt.event.MouseListener;  
import java.util.Arrays;  
  
public class RegisterJFrame extends JFrame implements MouseListener {  
  
    private JTextField usernameField;  
    private JPasswordField passwordField;  
    private JPasswordField confirmPasswordField; // 添加确认密码字段  
  
    private JLabel registerButton = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\注册按钮.png"));  
  
    public RegisterJFrame() {  
        //初始化界面  
        initJFrame();  
        //初始化图片  
        initImage();  
        //设置可见  
        this.setVisible(true);  
    }  
  
    //初始化界面展示内容  
    private void initImage() {  
        //账号和密码  
        JLabel usernameImage = new JLabel(new ImageIcon("..\\puzzlegame\\image\\register\\注册用户名.png"));  
        JLabel passwordImage = new JLabel(new ImageIcon("..\\puzzlegame\\image\\register\\注册密码.png"));  
        JLabel confirmPasswordImage = new JLabel(new ImageIcon("..\\puzzlegame\\image\\register\\确认密码.png")); // 添加确认密码标签  
  
        usernameImage.setBounds(130, 130, 47, 17);  
        passwordImage.setBounds(130, 180, 36, 16);  
        confirmPasswordImage.setBounds(130, 230, 60, 16); // 确认密码标签位置  
  
        this.getContentPane().add(usernameImage);  
        this.getContentPane().add(passwordImage);  
        this.getContentPane().add(confirmPasswordImage);  
  
        usernameField = new JTextField(20);  
        passwordField = new JPasswordField(20);  
        confirmPasswordField = new JPasswordField(20); // 初始化确认密码字段  
  
        usernameField.setBounds(190, 130, 200, 30);  
        passwordField.setBounds(190, 180, 200, 30);  
        confirmPasswordField.setBounds(190, 230, 200, 30); // 确认密码输入框位置  
  
        this.getContentPane().add(usernameField);  
        this.getContentPane().add(passwordField);  
        this.getContentPane().add(confirmPasswordField);  
  
        //注册按钮  
        registerButton.setBounds(220, 280, 128, 47); // 调整按钮位置  
  
        this.getContentPane().add(registerButton);  
  
        //为注册添加监听事件  
        registerButton.addMouseListener(this);  
        // 设置鼠标手型光标，提示用户可点击  
        registerButton.setCursor(new java.awt.Cursor(java.awt.Cursor.HAND_CURSOR));  
  
        //创建一个JLabel对象,为登录背景图  
        JLabel background = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\background.png"));  
        background.setBounds(0, 0, 470, 390);  
        this.getContentPane().add(background);  
    }  
  
    //初始化界面  
    private void initJFrame() {  
        //设置宽,高  
        this.setSize(488,430);  
  
        //设置界面的标题  
        this.setTitle("拼图注册界面"); // 修改标题  
  
        //设置界面置顶  
        this.setAlwaysOnTop(true);  
  
        //设置界面居中  
        this.setLocationRelativeTo(null);  
  
        //设置关闭模式  
        this.setDefaultCloseOperation(WindowConstants.DISPOSE_ON_CLOSE); // 修改关闭模式  
  
        //取消默认的居中位置，只有取消了才会按照XY轴的形式添加组件  
        this.setLayout(null);  
    }  
  
    @Override  
    public void mouseClicked(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == registerButton) {  
            handleRegister(); // 在点击事件中处理注册  
        }  
    }  
  
    @Override  
    public void mousePressed(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == registerButton) {  
            // 按钮按下效果  
            registerButton.setLocation(registerButton.getX() + 1, registerButton.getY() + 1);  
        }  
    }  
  
    @Override  
    public void mouseReleased(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == registerButton) {  
            // 按钮释放效果  
            registerButton.setLocation(registerButton.getX() - 1, registerButton.getY() - 1);  
        }  
    }  
  
    @Override  
    public void mouseEntered(MouseEvent e) {  
        //鼠标悬停时切换图片  
        Object source = e.getSource();  
        if (source == registerButton) {  
            registerButton.setIcon(new ImageIcon("..\\puzzlegame\\image\\login\\注册按下.png"));  
        }  
    }  
  
    @Override  
    public void mouseExited(MouseEvent e) {  
        //鼠标离开时恢复图片  
        Object source = e.getSource();  
        if (source == registerButton) {  
            registerButton.setIcon(new ImageIcon("..\\puzzlegame\\image\\login\\注册按钮.png"));  
        }  
    }  
  
    //注册验证  
    private void handleRegister() {  
        // 获取输入值  
        String username = usernameField.getText().trim();  
        char[] passwordChars = passwordField.getPassword();  
        char[] confirmPasswordChars = confirmPasswordField.getPassword();  
  
        String password = new String(passwordChars);  
        String confirmPassword = new String(confirmPasswordChars);  
  
        // 输入验证  
        if (username.isEmpty()) {  
            JOptionPane.showMessageDialog(this, "用户名不能为空!", "错误", JOptionPane.ERROR_MESSAGE);  
            // 安全清理密码  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
            return;  
        }  
  
        if (password.isEmpty()) {  
            JOptionPane.showMessageDialog(this, "密码不能为空!", "错误", JOptionPane.ERROR_MESSAGE);  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
            return;  
        }  
  
        if (!password.equals(confirmPassword)) {  
            JOptionPane.showMessageDialog(this, "两次输入的密码不一致!", "错误", JOptionPane.ERROR_MESSAGE);  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
            return;  
        }  
  
        if (password.length() < 6) {  
            JOptionPane.showMessageDialog(this, "密码长度不能少于6位!", "错误", JOptionPane.ERROR_MESSAGE);  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
            return;  
        }  
  
        // 检查用户名是否已存在  
        if (User.isUsernameExists(username)) {  
            JOptionPane.showMessageDialog(this, "用户名已存在，请选择其他用户名!", "错误", JOptionPane.ERROR_MESSAGE);  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
            return;  
        }  
  
        // 创建用户对象并保存  
        User newUser = new User(username, password);  
        if (newUser.addUser()) {  
            JOptionPane.showMessageDialog(this,  
                    "注册成功!\n用户名: " + username + "\n请返回登录界面登录。",  
                    "注册成功", JOptionPane.INFORMATION_MESSAGE);  
  
            // 安全清理密码  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
  
            // 清空输入框  
            usernameField.setText("");  
            passwordField.setText("");  
            confirmPasswordField.setText("");  
  
            // 询问是否返回登录界面  
            int option = JOptionPane.showConfirmDialog(this,  
                    "是否立即返回登录界面?", "返回登录",  
                    JOptionPane.YES_NO_OPTION);  
  
            if (option == JOptionPane.YES_OPTION) {  
                new LoginJFrame().setVisible(true);  
                this.dispose(); // 关闭注册界面  
            }  
        } else {  
            JOptionPane.showMessageDialog(this,  
                    "注册失败，请检查文件权限或重试!", "错误", JOptionPane.ERROR_MESSAGE);  
            clearPasswordArrays(passwordChars, confirmPasswordChars);  
        }  
    }  
  
    // 安全清理密码数组  
    private void clearPasswordArrays(char[]... arrays) {  
        for (char[] array : arrays) {  
            if (array != null) {  
                Arrays.fill(array, '0');  
            }  
        }  
    }  
}
```

## 2.3 登录界面
```java
package com.moyeah.ui;  
  
import com.moyeah.user.User;  
  
import javax.swing.*;  
import java.awt.event.MouseEvent;  
import java.awt.event.MouseListener;  
import java.util.Arrays;  
  
public class LoginJFrame extends JFrame implements MouseListener {  
  
    private JTextField usernameField;  
    private JPasswordField passwordField;  
    private String username;  
    private String password;  
  
    private JLabel loginButton = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\登录按钮.png"));  
    private JLabel registerButton = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\注册按钮.png"));  
  
    public LoginJFrame() {  
        //初始化界面  
        initJFrame();  
        //初始化图片  
        initImage();  
        //设置可见  
        this.setVisible(true);  
    }  
  
    //初始化界面展示内容  
    private void initImage() {  
        //账号和密码  
        JLabel usernameImage = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\用户名.png"));  
        JLabel passwordImage = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\密码.png"));  
  
        usernameImage.setBounds(130, 130, 47, 17);  
        passwordImage.setBounds(130, 180,36, 16);  
  
        this.getContentPane().add(usernameImage);  
        this.getContentPane().add(passwordImage);  
  
        usernameField = new JTextField(20);  
        passwordField = new JPasswordField(20);  
  
        usernameField.setBounds(190, 130, 200, 30);  
        passwordField.setBounds(190, 180, 200, 30);  
  
        this.getContentPane().add(usernameField);  
        this.getContentPane().add(passwordField);  
  
        //注册和登录按钮  
        loginButton.setBounds(110, 230, 128, 47);  
        registerButton.setBounds(269, 230, 128, 47);  
  
        this.getContentPane().add(loginButton);  
        this.getContentPane().add(registerButton);  
  
        //为注册登录添加监听事件  
        loginButton.addMouseListener(this);  
        registerButton.addMouseListener(this);  
        // 设置鼠标手型光标，提示用户可点击  
        loginButton.setCursor(new java.awt.Cursor(java.awt.Cursor.HAND_CURSOR));  
        registerButton.setCursor(new java.awt.Cursor(java.awt.Cursor.HAND_CURSOR));  
  
        //创建一个JLabel对象,为登录背景图  
        JLabel background = new JLabel(new ImageIcon("..\\puzzlegame\\image\\login\\background.png"));  
        background.setBounds(0, 0, 470, 390);  
        this.getContentPane().add(background);  
    }  
  
    //初始化界面  
    private void initJFrame() {  
        //设置宽,高  
        this.setSize(488,430);  
  
        //设置界面的标题  
        this.setTitle("拼图登录界面");  
  
        //设置界面置顶  
        this.setAlwaysOnTop(true);  
  
        //设置界面居中  
        this.setLocationRelativeTo(null);  
  
        //设置关闭模式  
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  
  
        //取消默认的居中位置，只有取消了才会按照XY轴的形式添加组件  
        this.setLayout(null);  
    }  
  
    @Override  
    public void mouseClicked(MouseEvent e) {  
        // 可以在这里处理点击事件，或者保持在mouseReleased中  
    }  
  
    @Override  
    public void mousePressed(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == loginButton) {  
            // 按钮按下效果  
            loginButton.setLocation(loginButton.getX() + 1, loginButton.getY() + 1);  
        } else if (source == registerButton) {  
            registerButton.setLocation(registerButton.getX() + 1, registerButton.getY() + 1);  
        }  
    }  
  
    @Override  
    public void mouseReleased(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == loginButton) {  
            // 按钮释放效果  
            loginButton.setLocation(loginButton.getX() - 1, loginButton.getY() - 1);  
            handleLogin();  
        } else if (source == registerButton) {  
            registerButton.setLocation(registerButton.getX() - 1, registerButton.getY() - 1);  
            handleRegister();  
        }  
    }  
  
    @Override  
    public void mouseEntered(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == loginButton) {  
            loginButton.setIcon(new ImageIcon("..\\puzzlegame\\image\\login\\登录按下.png"));  
        } else if (source == registerButton) {  
            registerButton.setIcon(new ImageIcon("..\\puzzlegame\\image\\login\\注册按下.png"));  
        }  
    }  
  
    @Override  
    public void mouseExited(MouseEvent e) {  
        Object source = e.getSource();  
        if (source == loginButton) {  
            loginButton.setIcon(new ImageIcon("..\\puzzlegame\\image\\login\\登录按钮.png"));  
        } else if (source == registerButton) {  
            registerButton.setIcon(new ImageIcon("..\\puzzlegame\\image\\login\\注册按钮.png"));  
        }  
    }  
  
    //登录验证  
    private void handleLogin() {  
        // 获取输入的用户名和密码  
        String username = usernameField.getText().trim();  
        char[] passwordChars = passwordField.getPassword();  
        String password = new String(passwordChars);  
  
        // 输入验证  
        if (username.isEmpty()) {  
            showErrorMessage("用户名不能为空!");  
            clearPasswordArray(passwordChars);  
            return;  
        }  
  
        if (password.isEmpty()) {  
            showErrorMessage("密码不能为空!");  
            clearPasswordArray(passwordChars);  
            return;  
        }  
  
        // 使用User类验证登录  
        if (User.validateUser(username, password)) {  
            // 登录成功  
            JOptionPane.showMessageDialog(this,  
                    "登录成功!\n欢迎回来，" + username + "!",  
                    "登录成功", JOptionPane.INFORMATION_MESSAGE);  
  
            // 安全清理密码  
            clearPasswordArray(passwordChars);  
  
            // 打开游戏界面  
            new GameJFrame().setVisible(true);  
            this.dispose(); 
        } else {  
            // 登录失败  
            showErrorMessage("用户名或密码错误!");  
            clearPasswordArray(passwordChars);  
        }  
    }  
  
    // 处理注册按钮点击  
    private void handleRegister() {  
        // 打开注册界面  
        new RegisterJFrame().setVisible(true);  
        this.dispose();  
    }  
  
    // 显示错误消息 
    private void showErrorMessage(String message) {  
        JOptionPane.showMessageDialog(this, message, "错误", JOptionPane.ERROR_MESSAGE);  
    }  
  
    // 安全清理密码数组  
    private void clearPasswordArray(char[] passwordArray) {  
        if (passwordArray != null) {  
            Arrays.fill(passwordArray, '0');  
        }  
    }  
}
```


# 3 感受
在写这个项目的过程中，我更加感受到什么叫面向对象，尤其是在添加JFrame还有各种各样管理图片还有文字，以及对各种组件进行管理的过程中。对接口的实现以及方法调用的一些理解更加深刻。还有对一些业务逻辑的基本理解，可能没啥理解。整体项目有从子龙哥那里做参考，但可能我的技术不到家，这个结构啊编码等不太规范还，也算是一个java学习过程中的小里程碑

前两天有人问我sql注入，我去看了看java里的预防sql注入。
这里了解到一个知识点就是，它java里面预置sql语句，有用`$`接收参数的，还有`#`的
我去查文章的时候说是
`$`比较危险，而#比较安全
为什么呢，我之前寒假的时候搭建那个人博客项目（php+mysql），看ai给我写的（那个只是了解了一下一个网站的前后端交互，所以没自己写），扫了一眼它说预置sql语句可以预防sql注入，我以为只要预置了就可以预防了，其实这里理解浅显了

`$`那个，它的内部逻辑是字符串拼接，既然字符串拼接了，那我就可以使用一些闭合符号去构造`payload`了
而`#`呢，它的内部逻辑是值的传递，也就是说那些拼接符号还有注释符它会被当作值，就不会对原来的语句造成改变

这是我的项目文件结构
![[Pasted image 20251118141310.png]]
至于它为什么是这么个结构我其实还没有去细了解，有些地方目前也只是跟上去做了一遍，游戏界面是跟着教程来的，登录和注册则是自己敲的，当然也有一些新的东西，有查资料这里改怎么写，看源码、api帮助文档啥的，碰到什么不会学什么

# 4 下面是一个安全问题

## 核心问题：字符串的不可变性

### 1. 字符串的特殊存储方式

在Java中，字符串是**不可变对象**。这意味着：

- 一旦创建，内容就不能被修改
    
- 任何"修改"操作都会创建新的字符串对象
    
- 旧的字符串对象会继续存在于内存中，直到被垃圾回收
    

```
String password = "myPassword123";
password = "newPassword"; // 实际上创建了新对象，旧对象还在内存中
```

### 2. 垃圾回收的不确定性

Java的垃圾回收机制是**非确定性的**：

- 你无法控制何时进行垃圾回收
    
- 无法保证字符串对象会立即被清除
    
- 密码字符串可能在内存中停留几分钟、几小时，甚至程序运行期间一直存在
    

## 具体的安全风险

### 风险1：内存转储攻击

攻击者可以通过以下方式获取内存内容：

- **系统崩溃时的核心转储文件**
    
- **调试工具直接读取进程内存**
    
- **虚拟机的快照功能**
    
- **恶意软件扫描内存**
    

如果密码以字符串形式存在，攻击者很容易在内存中找到它。

### 风险2：字符串池的持久化

字符串字面量会进入字符串常量池，这可能使密码长期存在：

```
// 不安全的做法 - 可能进入字符串池
String password = "hardcodedPassword";

// 相对好一些，但仍有风险
String password = new String(passwordField.getPassword());
```

### 风险3：日志记录和调试信息

字符串更容易意外泄露：

```
// 可能无意中将密码记录到日志
logger.debug("用户密码: " + password); // ❌ 危险！
System.out.println(password); // ❌ 极其危险！
```

## 为什么字符数组更安全？

### 优势1：可以主动清除

```
char[] passwordChars = passwordField.getPassword();

// 使用密码进行验证...
userService.login(username, passwordChars);

// 使用后立即清除
Arrays.fill(passwordChars, '\0'); // 用空字符覆盖
```

### 优势2：不会进入字符串池

字符数组是普通对象，不会被特殊缓存。

### 优势3：减少意外泄露

- 不容易被意外记录到日志
    
- 调试信息通常不会显示数组内容
    
- 需要显式操作才能转换为字符串
    

## 实际代码对比

### ❌ 不安全的字符串方式

```
public class LoginService {
    private String currentPassword; // 危险：密码长期存在
    
    public boolean login(String username, String password) {
        this.currentPassword = password; // 危险：保留了引用
        // 验证逻辑...
        return isValid;
    }
    
    // 即使设置为null，也不能保证立即从内存清除
    public void logout() {
        this.currentPassword = null;
    }
}
```

### ✅ 安全的字符数组方式

```
public class SecureLoginService {
    private char[] currentPassword; // 相对安全
    
    public boolean login(String username, char[] password) {
        // 立即使用，不长期保存引用
        boolean isValid = validateCredentials(username, password);
        
        // 使用后立即清除
        Arrays.fill(password, '\0');
        return isValid;
    }
    
    public void clearPassword() {
        if (currentPassword != null) {
            Arrays.fill(currentPassword, '\0');
            currentPassword = null;
        }
    }
}
```

## 现实世界中的攻击案例

1. **Heartbleed漏洞**：攻击者可以读取服务器内存中的敏感信息
    
2. **内存分析工具**：取证工具可以分析崩溃转储文件
    
3. **虚拟化环境**：云服务中其他虚拟机可能通过侧信道攻击读取内存
    

## 最佳实践总结

1. **优先使用char[]**处理密码
    
2. **尽快清除**：使用后立即用`Arrays.fill()`覆盖
    
3. **避免缓存**：不要长期保存密码引用
    
4. **小心转换**：尽量避免将char[]转换为String
    
5. **使用安全API**：如Java的`Console.readPassword()`
    

```
// 安全的使用模式
char[] password = passwordField.getPassword();
try {
    // 进行身份验证
    authenticate(username, password);
} finally {
    // 确保无论如何都会清除
    Arrays.fill(password, '\0');
}
```

这就是为什么专业的密码处理都推荐使用字符数组的原因。虽然不能100%防止所有攻击，但大大降低了密码在内存中泄露的风险。

# 5 改进
# 5.1 登录注册机制改进
将原本的用户名登录和注册改为账号id，用户可更改昵称
id为唯一值，将其改为数据库存储