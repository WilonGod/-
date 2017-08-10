# -
const 修饰符的意义：
const是C/C++中的一个关键字(修饰符), const一般用来定义一个常量, 既然叫做常量, 即以后再也不能修改其值。
int  const  *p   //  *p只读 ;p变量
int  * const  p  // *p变量 ; p只读
const  int   * const p //p和*p都只读
int  const  * const  p   //p和*p都只读
//注释
1、const int *a
这里const 修饰的是int，而int定义的是一个整值
因此*a 所指向的对象 值 不能通过 *a 来修改，但是 可以重新给 a 来赋值，使其指向不同的对象
eg:
  const int *a = 0;
  const int b = 1;
  int c = 1;
  a = &b //ok！ 额外：注意不能通过a 来修改 b值
  a = &c //ok！ 额外：虽然c本身不是一个常量
  *a = 2 //erro！ 为题就在这里，不能修改通过 *a 所指向的对象值，最后赋值得对象是c，因此不能通过*a 来修改c值。
2、int *const a  
这里const修饰的是 a ，a代表的是一个指针地址
因此不能赋给a其他的地址值，但可以修改a指向的值
这有点和cont int *a相反的意味，例子就不说了
3、至于int const *a 和 const int *a 的意义是相同的 他们两个的作用等价
补充：
4、const int * const a 
这个代表a所指向的对象的值以及它的地址本身都不能被改变
int const * const a;表示a是一个指针常量，初始化的时候必须固定指向一个int常量或者int变量，之后就不能再指向别的地方了，它总是把它所指向的目标当作一个int常量。也可以写成const int* const a;含义相同。  
5. 对于const int *a和int *const a，可以理解为：const int *a中const修饰*a，但是a可变，只要a指向的目标是const类型就可以；而int *const a中const修饰a，一旦指向则不能改写，但是可以修改*a的值

Static关键字的意义：
1.当一个进程的全局变量被声明为static之后，它的中文名叫静态全局变量。静态全局变量和其他的全局变量的存储地点并没有区别，都是在.data段（已初始化）或者.bss段（未初始化）内，但是它只在定义它的源文件内有效，其他源文件无法访问它
2.普通的局部变量在栈空间上分配，这个局部变量所在的函数被多次调用时，每次调用这个局部变量在栈上的位置都不一定相同。局部变量也可以在堆上动态分配，但是记得使用完这个堆空间后要释放之。
  static局部变量中文名叫静态局部变量。它与普通的局部变量比起来有如下几个区别：
  1）位置：静态局部变量被编译器放在全局存储区.data（注意：不在.bss段内，原因见3）），所以它虽然是局部的，但是在程序的整个生命周期中存在。
  2）访问权限：静态局部变量只能被其作用域内的变量或函数访问。也就是说虽然它会在程序的整个生命周期中存在，由于它是static的，它不能被其他的函数和源文件访问。
  3）值：静态局部变量如果没有被用户初始化，则会被编译器自动赋值为0，以后每次调用静态局部变量的时候都用上次调用后的值。这个比较好理解，每次函数调用静态局部变量的时候都修改它然后离开，下次读的时候从全局存储区读出的静态局部变量就是上次修改后的值。
  3.声明函数
    相信大家还记得C++面向对象编程中的private函数，私有函数只有该类的成员变量或成员函数可以访问。在C语言中，也有“private函数”，它就是接下来要说的static函数，完成面向对象编程中private函数的功能。
    当你的程序中有很多个源文件的时候，你肯定会让某个源文件只提供一些外界需要的接口，其他的函数可能是为了实现这些接口而编写，这些其他的函数你可能并不希望被外界（非本源文件）所看到，这时候就可以用static修饰这些“其他的函数”。
    所以static函数的作用域是本源文件，把它想象为面向对象中的private函数就可以了。
    extern，表示该函数是外部函数，可供其他文件调用。另外在要引用别的文件中定义的外部函数的文件中，使用extern声明要用的外部函数即可。
    
设计模式是什么？ 你知道哪些设计模式，并简要叙述？
设计模式是一种编码经验，就是用比较成熟的逻辑去处理某一种类型的事情。
1). MVC模式：Model View Control，把模型 视图 控制器 层进行解耦合编写。
2). MVVM模式：Model View ViewModel 把模型 视图 业务逻辑 层进行解耦和编写。
3). 单例模式：通过static关键词，声明全局变量。在整个进程运行期间只会被赋值一次。
4). 观察者模式：KVO是典型的通知模式，观察某个属性的状态，状态发生变化时通知观察者。
5). 委托模式：代理+协议的组合。实现1对1的反向传值操作。
6). 工厂模式：通过一个类方法，批量的根据已有模板生产对象。
#import跟 #include 有什么区别，@class呢，#import<> 跟 #import””有什么区别？
1). #import是Objective-C导入头文件的关键字，#include是C/C++导入头文件的关键字，使用#import头文件会自动只导入一次，不会重复导入。
2). @class告诉编译器某个类的声明，当执行时，才去查看类的实现文件，可以解决头文件的相互包含。
3). #import<>用来包含系统的头文件，#import””用来包含用户头文件。
frame 和 bounds 有什么不同？
frame指的是：该view在父view坐标系统中的位置和大小。(参照点是父view的坐标系统)
bounds指的是：该view在本身坐标系统中的位置和大小。(参照点是本身坐标系统)

CALayer与UIView的联系及区别：



每个 UIView 内部都有一个 CALayer 在背后提供内容的绘制和显示，并且 UIView 的尺寸样式都由内部的 Layer 所提供。两者都有树状层级结构，layer 内部有 SubLayers，View 内部有 SubViews.但是 Layer 比 View 多了个AnchorPoint
在 View显示的时候，UIView 做为 Layer 的 CALayerDelegate,View 的显示内容由内部的 CALayer 的 display
CALayer 是默认修改属性支持隐式动画的，在给 UIView 的 Layer 做动画的时候，View 作为 Layer 的代理，Layer 通过 actionForLayer:forKey:向 View请求相应的 action(动画行为)
layer 内部维护着三分 layer tree,分别是 presentLayer Tree(动画树),modeLayer Tree(模型树), Render Tree (渲染树),在做 iOS动画的时候，我们修改动画的属性，在动画的其实是 Layer 的 presentLayer的属性值,而最终展示在界面上的其实是提供 View的modelLayer
两者最明显的区别是 View可以接受并处理事件，而 Layer 不可以

//**
1.首先UIView可以响应事件，Layer不可以.
UIKit使用UIResponder作为响应对象，来响应系统传递过来的事件并进行处理。UIApplication、UIViewController、UIView、和所有从UIView派生出来的UIKit类（包括UIWindow）都直接或间接地继承自UIResponder类。
在 UIResponder中定义了处理各种事件和事件传递的接口, 而 CALayer直接继承 NSObject，并没有相应的处理事件的接口。
2.View和CALayer的Frame映射及View如何创建CALayer.
一个 Layer 的 frame 是由它的 anchorPoint,position,bounds,和 transform 共同决定的，而一个 View 的 frame 只是简单的返回 Layer的 frame，同样 View 的 center和 bounds 也是返回 Layer 的一些属性。［UIView _createLayerWithFrame］
步骤：
[UIView _createLayerWithFrame]
[Layer setBounds:bounds]
[UIView setFrame：Frame]
[Layer setFrame:frame]
[Layer setPosition:position]
[Layer setBounds:bounds]
UIView并没有做什么工作；它只是简单的各自调用它底层的CALayer的frame，bounds和position方法。
3.UIView主要是对显示内容的管理而 CALayer 主要侧重显示内容的绘制。
[UIView(CALayerDelegate) drawLayer:inContext]调用 UIView 的 DrawRect方法，从而绘制出了 UIView 的内容.
4.在做 iOS 动画的时候，修改非 RootLayer的属性（譬如位置、背景色等）会默认产生隐式动画，而修改UIView则不会
对于每一个 UIView 都有一个 layer,把这个 layer 且称作RootLayer,而不是 View 的根 Layer的叫做 非 RootLayer。我们对UIView的属性修改时时不会产生默认动画，而对单独 layer属性直接修改会，这个默认动画的时间缺省值是0.25s
UIView 默认情况下禁止了 layer 动画，但是在 animation block 中又重新启用了它们
是因为任何可动画的 layer 属性改变时，layer 都会寻找并运行合适的 'action' 来实行这个改变。在 Core Animation 的专业术语中就把这样的动画统称为动作 (action，或者 CAAction)。
layer 通过向它的 delegate 发送 actionForLayer:forKey: 消息来询问提供一个对应属性变化的 action。delegate 可以通过返回以下三者之一来进行响应：
它可以返回一个动作对象，这种情况下 layer 将使用这个动作。
它可以返回一个 nil， 这样 layer 就会到其他地方继续寻找。
它可以返回一个 NSNull 对象，告诉 layer 这里不需要执行一个动作，搜索也会就此停止。
当 layer 在背后支持一个 view 的时候，view 就是它的 delegate；
**//

@property 的本质是什么？ivar、getter、setter 是如何生成并添加到这个类中的

@property 的本质是什么？
	@property = ivar + getter + setter;
“属性” (property)有两大概念：ivar（实例变量）、getter+setter（存取方法）

@property中有哪些属性关键字？/ @property 后面可以有哪些修饰符？

属性可以拥有的特质分为四类:
1.原子性--- nonatomic 特质
2.读/写权限---readwrite(读写)、readonly (只读)
3.内存管理语义---assign、strong、 weak、unsafe_unretained、copy
4.方法名---getter=<name> 、setter=<name>
5.不常用的：nonnull,null_resettable,nullable


@property中有哪些属性关键字？/ @property 后面可以有哪些修饰符？

属性可以拥有的特质分为四类:
1.原子性--- nonatomic 特质
2.读/写权限---readwrite(读写)、readonly (只读)
3.内存管理语义---assign、strong、 weak、unsafe_unretained、copy
4.方法名---getter=<name> 、setter=<name>
5.不常用的：nonnull,null_resettable,nullable

什么情况使用 weak 关键字，相比 assign 有什么不同？

1.在 ARC 中,在有可能出现循环引用的时候,往往要通过让其中一端使用 weak 来解决,比如: delegate 代理属性。
2.自身已经对它进行一次强引用,没有必要再强引用一次,此时也会使用 weak,自定义 IBOutlet 控件属性一般也使用 weak；当然，也可以使用strong。

IBOutlet连出来的视图属性为什么可以被设置成weak?
	因为父控件的subViews数组已经对它有一个强引用。

不同点：
assign 可以用非 OC 对象，而 weak 必须用于 OC 对象。

怎么用 copy 关键字？

 用途：
 1. NSString、NSArray、NSDictionary 等等经常使用copy关键字，是因为他们有对应的可变类型：NSMutableString、NSMutableArray、NSMutableDictionary；
 2. block 也经常使用 copy 关键字。

 说明：
 block 使用 copy 是从 MRC 遗留下来的“传统”,在 MRC 中,方法内部的 block 是在栈区的,使用 copy 可以把它放到堆区.在 ARC 中写不写都行：对于 block 使用 copy 还是 strong 效果是一样的，但写上 copy 也无伤大雅，还能时刻提醒我们：编译器自动对 block 进行了 copy 操作。如果不写 copy ，该类的调用者有可能会忘记或者根本不知道“编译器会自动对 block 进行了 copy 操作”，他们有可能会在调用之前自行拷贝属性值。这种操作多余而低效。
 
 
 用@property声明的 NSString / NSArray / NSDictionary 经常使用 copy 关键字，为什么？如果改用strong关键字，可能造成什么问题？

答：用 @property 声明 NSString、NSArray、NSDictionary 经常使用 copy 关键字，是因为他们有对应的可变类型：NSMutableString、NSMutableArray、NSMutableDictionary，他们之间可能进行赋值操作（就是把可变的赋值给不可变的），为确保对象中的字符串值不会无意间变动，应该在设置新属性值时拷贝一份。

1. 因为父类指针可以指向子类对象,使用 copy 的目的是为了让本对象的属性不受外界影响,使用 copy 无论给我传入是一个可变对象还是不可对象,我本身持有的就是一个不可变的副本。
2. 如果我们使用是 strong ,那么这个属性就有可能指向一个可变对象,如果这个可变对象在外部被修改了,那么会影响该属性。

//总结：使用copy的目的是，防止把可变类型的对象赋值给不可变类型的对象时，可变类型对象的值发送变化会无意间篡改不可变类型对象原来的值。

浅拷贝和深拷贝的区别？

答：
浅拷贝：只复制指向对象的指针，而不复制引用对象本身。
深拷贝：复制引用对象本身。内存中存在了两份独立对象本身，当修改A时，A_copy不变。

系统对象的 copy 与 mutableCopy 方法

不管是集合类对象（NSArray、NSDictionary、NSSet ... 之类的对象），还是非集合类对象（NSString, NSNumber ... 之类的对象），接收到copy和mutableCopy消息时，都遵循以下准则：
1. copy 返回的是不可变对象（immutableObject）；如果用copy返回值调用mutable对象的方法就会crash。
2. mutableCopy 返回的是可变对象（mutableObject）。

这个写法会出什么问题：@property (nonatomic, copy) NSMutableArray *arr;

问题：添加,删除,修改数组内的元素的时候,程序会因为找不到对应的方法而崩溃。
//如：-[__NSArrayI removeObjectAtIndex:]: unrecognized selector sent to instance 0x7fcd1bc30460
// copy后返回的是不可变对象（即 arr 是 NSArray 类型，NSArray 类型对象不能调用 NSMutableArray 类型对象的方法）
原因：是因为 copy 就是复制一个不可变 NSArray 的对象，不能对 NSArray 对象进行添加/修改。

如何让自己的类用 copy 修饰符？如何重写带 copy 关键字的 setter？

若想令自己所写的对象具有拷贝功能，则需实现 NSCopying 协议。如果自定义的对象分为可变版本与不可变版本，那么就要同时实现 NSCopying 与 NSMutableCopying 协议。
具体步骤：
	1. 需声明该类遵从 NSCopying 协议
	2. 实现 NSCopying 协议的方法。
		// 该协议只有一个方法: 
		- (id)copyWithZone:(NSZone *)zone;
		// 注意：使用 copy 修饰符，调用的是copy方法，其实真正需要实现的是 “copyWithZone” 方法。
    
Objective-C的类可以多重继承么？可以实现多个接口么？Category是什么？重写一个类的方式用继承好还是分类好？为什么？
Objective-C的类不可以多重继承；可以实现多个接口（协议）；Category是类别；一般情况用分类好，用Category去重写类的方法，仅对本Category有效，不会影响到其他类与原有类的关系。

Category（类别）、 Extension（扩展）和继承的区别
1. 分类有名字，类扩展没有分类名字，是一种特殊的分类。
2. 分类只能扩展方法（属性仅仅是声明，并没真正实现），类扩展可以扩展属性、成员变量和方法。
3. 继承可以增加，修改或者删除方法，并且可以增加属性。

分类Caterygory的实现原理
虽然分类可以声明属性，但是编译时，系统并没有生成分类属性的 get／set 方法，所以，这就是为什么分类要利用
runtime 动态添加属性
把category的实例方法、协议以及属性添加到类上
把category的类方法和协议添加到类的metaclass上
那么分类中得方法会覆盖原来那一份实现代码 
category 主要作用给已经存在的类添加方法
为现有的类添加私有变量以帮助实现细节；
为现有的类添加公有属性；
为 KVO 创建一个关联的观察者。

delegate  notification  kvo kvc  block 分别是什么 什么场景使用
委托代理，面向过程，
因为是外部引用不受控制，不知何时释放，所以weak
Delegate(委托模式)：1对1的反向消息通知功能。
Notification(通知模式)：只想要把消息发送出去，告知某些状态的变化。但是并不关心谁想要知道这个。



kvo: KVO就是观察者模式。

kvc就是键值编码（key－value），说白了就是通过指定的key获得想要的值value。而不是通过调用Setter、Getter方法访问。*
. setValue:forKey的搜索方式：

当一个对象调用setValue方法时，方法内部会做以下操作：
1). 检查是否存在相应的key的set方法，如果存在，就调用set方法。
2). 如果set方法不存在，就会查找与key相同名称并且带下划线的成员变量，如果有，则直接给成员变量属性赋值。
3). 如果没有找到_key，就会查找相同名称的属性key，如果有就直接赋值。
4). 如果还没有找到，则调用valueForUndefinedKey:和setValue:forUndefinedKey:方法。
这些方法的默认实现都是抛出异常，我们可以根据需要重写它们。


1. 首先搜索set<Key>:方法

如果成员用@property，@synthsize处理，因为@synthsize告诉编译器自动生成set<Key>:格式的setter方法，所以这种情况下会直接搜索到。

注意：这里的<Key>是指成员名，而且首字母大写。下同。

2. 上面的setter方法没有找到，如果类方法accessInstanceVariablesDirectly返回YES(注：这是NSKeyValueCodingCatogery中实现的类方法，默认实现为返回YES)。

那么按_<key>，_is<Key>，<key>，is<key>的顺序搜索成员名。

3. 如果找到设置成员的值，如果没有调用setValue:forUndefinedKey:。

1 .访问私有变量
2. 使用KVC直接访问 NSArray 或者 NSSet 的属性值
3. 使用KVC将字典（json）转化成模型

block 类似指针函数，代码块，带有局部变量的匿名函数更面向结果，无状态，返回值适合


block属性

这里还有一点关于block类型的ARC属性。上文也说明了，ARC会自动帮strong类型且捕获外部变量的block进行copy，所以在定义block类型的属性时也可以使用strong，不一定使用copy。也就是以下代码：
一个Block被复制到堆上时，与之相关的__block变量也会被复制到堆上，此时堆上的Block持有相应堆上的__block变量。当堆上的__block变量没有持有者时，它才会被废弃


/** 假如有栈block赋给以下两个属性 **/

// 这里因为ARC，当栈block中会捕获外部变量时，这个block会被copy进堆中
// 如果没有捕获外部变量，这个block会变为全局类型
// 不管怎么样，它都脱离了栈生命周期的约束




我们说的OC是动态运行时语言是什么意思？
主要是将数据类型的确定由编译时，推迟到了运行时。简单来说, 运行时机制使我们直到运行时才去决定一个对象的类别,以及调用该类别对象指定方法。
KVO的实现及步骤：
重写setter方法：
1.注册需要观察的对象的属性addObserver:forKeyPath:options:context:
2.实现observeValueForKeyPath:ofObject:change:context:方法，这个方法当观察的属性变化时会自动调用
3.取消注册观察removeObserver:forKeyPath:context:

如何访问并修改一个类的私有属性？

1). 一种是通过KVC获取。
2). 通过runtime访问并修改私有属性。

isa指针问题

isa：是一个Class 类型的指针. 每个实例对象有个isa的指针,他指向对象的类,而Class里也有个isa的指针, 指向meteClass(元类)。元类保存了类方法的列表。当类方法被调 用时,先会从本身查找类方法的实现,如果没有,元类会向他父类查找该方法。同时注意的是:元类(meteClass)也是类,它也是对象。元类也有isa指针,它的isa指针最终指向的是一个根元类(root meteClass)。根元类的isa指针指向本身,这样形成了一个封闭的内循环。

一个objc对象的isa的指针指向什么？有什么作用？

答：指向他的类对象,从而可以找到对象上的方法。

下面的代码输出什么？

@implementation Son : Father
- (id)init {
   if (self = [super init]) {
       NSLog(@"%@", NSStringFromClass([self class])); // Son
       NSLog(@"%@", NSStringFromClass([super class])); // Son
   }
   return self;
}
@end


lldb（gdb）常用的控制台调试命令？

1). p 输出基本类型。是打印命令，需要指定类型。是print的简写
	p (int)[[[self view] subviews] count]
2). po 打印对象，会调用对象description方法。是print-object的简写
	po [self view]
3). expr 可以在调试时动态执行指定表达式，并将结果打印出来。常用于在调试过程中修改变量的值。
4). bt：打印调用堆栈，是thread backtrace的简写，加all可打印所有thread的堆栈
5). br l：是breakpoint list的简写

lldb（gdb）常用的控制台调试命令？

1). p 输出基本类型。是打印命令，需要指定类型。是print的简写
	p (int)[[[self view] subviews] count]
2). po 打印对象，会调用对象description方法。是print-object的简写
	po [self view]
3). expr 可以在调试时动态执行指定表达式，并将结果打印出来。常用于在调试过程中修改变量的值。
4). bt：打印调用堆栈，是thread backtrace的简写，加all可打印所有thread的堆栈
5). br l：是breakpoint list的简写



static id _instance;
+ (id)allocWithZone:(struct _NSZone *)zone {
   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
       _instance = [super allocWithZone:zone];
   });
   return _instance;
}

+ (instancetype)sharedData {
   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
       _instance = [[self alloc] init];
   });
   return _instance;
}

- (id)copyWithZone:(NSZone *)zone {
   return _instance;
}


写一个完整的代理，包括声明、实现

// 创建
@protocol MyDelagate
@required
-(void)eat:(NSString *)foodName; 
@optional
-(void)run;
@end

//  声明 .h
@interface person: NSObject<MyDelagate>

@end

//  实现 .m
@implementation person
- (void)eat:(NSString *)foodName { 
   NSLog(@"吃:%@!", foodName);
} 
- (void)run {
   NSLog(@"run!");
}

@end



如何访问并修改一个类的私有属性？

1). 一种是通过KVC获取。
2). 通过runtime访问并修改私有属性。


什么是 RunLoop

从字面上讲就是运行循环，它内部就是do-while循环，在这个循环内部不断地处理各种任务。
一个线程对应一个RunLoop，基本作用就是保持程序的持续运行，处理app中的各种事件。通过runloop，有事运行，没事就休息，可以节省cpu资源，提高程序性能。

主线程的run loop默认是启动的。iOS的应用程序里面，程序启动后会有一个如下的main()函数
int main(int argc, char * argv[]) {
	@autoreleasepool {
    	return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
	}
}

什么是 Runtime

Runtime又叫运行时，是一套底层的C语言API，其为iOS内部的核心之一，我们平时编写的OC代码，底层都是基于它来实现的。

Runtime实现的机制是什么，怎么用，一般用于干嘛？

1). 使用时需要导入的头文件 <objc/message.h> <objc/runtime.h>
2). Runtime 运行时机制，它是一套C语言库。
3). 实际上我们编写的所有OC代码，最终都是转成了runtime库的东西。
	比如：
		类转成了 Runtime 库里面的结构体等数据类型，
		方法转成了 Runtime 库里面的C语言函数，
		平时调方法都是转成了 objc_msgSend 函数（所以说OC有个消息发送机制）
	// OC是动态语言，每个方法在运行时会被动态转为消息发送，即：objc_msgSend(receiver, selector)。
	// [stu show];  在objc动态编译时，会被转意为：objc_msgSend(stu, @selector(show));	
4). 因此，可以说 Runtime 是OC的底层实现，是OC的幕后执行者。

有了Runtime库，能做什么事情呢？
 Runtime库里面包含了跟类、成员变量、方法相关的API。
 比如：
    （1）获取类里面的所有成员变量。
    （2）为类动态添加成员变量。
    （3）动态改变类的方法实现。
    （4）为类动态添加新的方法等。
 因此，有了Runtime，想怎么改就怎么改。

什么是 Method Swizzle（黑魔法），什么情况下会使用？

1). 在没有一个类的实现源码的情况下，想改变其中一个方法的实现，除了继承它重写、和借助类别重名方法暴力抢先之外，还有更加灵活的方法 Method Swizzle。
2). Method Swizzle 指的是改变一个已存在的选择器对应的实现的过程。OC中方法的调用能够在运行时通过改变，通过改变类的调度表中选择器到最终函数间的映射关系。
3). 在OC中调用一个方法，其实是向一个对象发送消息，查找消息的唯一依据是selector的名字。利用OC的动态特性，可以实现在运行时偷换selector对应的方法实现。
4). 每个类都有一个方法列表，存放着selector的名字和方法实现的映射关系。IMP有点类似函数指针，指向具体的方法实现。
5). 我们可以利用 method_exchangeImplementations 来交换2个方法中的IMP。
6). 我们可以利用 class_replaceMethod 来修改类。
7). 我们可以利用 method_setImplementation 来直接设置某个方法的IMP。
8). 归根结底，都是偷换了selector的IMP。

_objc_msgForward 函数是做什么的，直接调用它将会发生什么？

答：_objc_msgForward是 IMP 类型，用于消息转发的：当向一个对象发送一条消息，但它并没有实现的时候，_objc_msgForward会尝试做消息转发。


GCD 与 NSOperation 的区别：

GCD 和 NSOperation 都是用于实现多线程：
	GCD 基于C语言的底层API，GCD主要与block结合使用，代码简洁高效。
	NSOperation 属于Objective-C类，是基于GCD更高一层的封装。复杂任务一般用NSOperation实现。

写出使用GCD方式从子线程回到主线程的方法代码

答：dispatch_sync(dispatch_get_main_queue(), ^{ });

如何用GCD同步若干个异步调用？（如根据若干个url异步加载多张图片，然后在都下载完成后合成一张整图）

// 使用Dispatch Group追加block到Global Group Queue,这些block如果全部执行完毕，就会执行Main Dispatch Queue中的结束处理的block。
// 创建队列组
dispatch_group_t group = dispatch_group_create();
// 获取全局并发队列
dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
dispatch_group_async(group, queue, ^{ /*加载图片1 */ });
dispatch_group_async(group, queue, ^{ /*加载图片2 */ });
dispatch_group_async(group, queue, ^{ /*加载图片3 */ }); 
// 当并发队列组中的任务执行完毕后才会执行这里的代码
dispatch_group_notify(group, dispatch_get_main_queue(), ^{
        // 合并图片
});

dispatch_barrier_async（栅栏函数）的作用是什么？

函数定义：dispatch_barrier_async(dispatch_queue_t queue, dispatch_block_t block);
作用：
	1.在它前面的任务执行结束后它才执行，它后面的任务要等它执行完成后才会开始执行。
	2.避免数据竞争

// 1.创建并发队列
dispatch_queue_t queue = dispatch_queue_create("myQueue", DISPATCH_QUEUE_CONCURRENT);
// 2.向队列中添加任务
dispatch_async(queue, ^{  // 1.2是并行的
    NSLog(@"任务1, %@",[NSThread currentThread]);
});
dispatch_async(queue, ^{
    NSLog(@"任务2, %@",[NSThread currentThread]);
});

dispatch_barrier_async(queue, ^{
    NSLog(@"任务 barrier, %@", [NSThread currentThread]);
});

dispatch_async(queue, ^{   // 这两个是同时执行的
    NSLog(@"任务3, %@",[NSThread currentThread]);
});
dispatch_async(queue, ^{
    NSLog(@"任务4, %@",[NSThread currentThread]);
});

// 输出结果: 任务1 任务2 ——》 任务 barrier ——》任务3 任务4 
// 其中的任务1与任务2，任务3与任务4 由于是并行处理先后顺序不定。


你一般是怎么用Instruments的？

Instruments里面工具很多，常用：
1). Time Profiler: 性能分析
2). Zombies：检查是否访问了僵尸对象，但是这个工具只能从上往下检查，不智能。
3). Allocations：用来检查内存，写算法的那批人也用这个来检查。
4). Leaks：检查内存，看是否有内存泄露。

iOS中常用的数据存储方式有哪些？

数据存储有四种方案：NSUserDefault、KeyChain、file、DB。
	其中File有三种方式：plist、Archive（归档）
	DB包括：SQLite、FMDB、CoreData

block的注意点

1). 在block内部使用外部指针且会造成循环引用情况下，需要用__week修饰外部指针：
	__weak typeof(self) weakSelf = self; 
2). 在block内部如果调用了延时函数还使用弱指针会取不到该指针，因为已经被销毁了，需要在block内部再将弱指针重新强引用一下。
	__strong typeof(self) strongSelf = weakSelf;
3). 如果需要在block内部改变外部栈区变量的话，需要在用__block修饰外部变量。

BAD_ACCESS在什么情况下出现？

答：这种问题在开发时经常遇到。原因是访问了野指针，比如访问已经释放对象的成员变量或者发消息、死循环等。

描述下GCD死锁现象。

响应者链：
指的是有响应和处理事件能力的对象。响应者链就是由一系列的响应者对象构成的一个层次结构。
UIApplication、 UIViewController、UIWindow和所有继承自UIView的UIKit类都直接或间接的继承自UIResponder，所以它们的实例都是可以构成响应者链的响应者对象。

1、响应者链通常是由视图（UIView）构成的；

2、一个视图的下一个响应者是它视图控制器（UIViewController）（如果有的话），然后再转给它的父视图（Super View）；

3、视图控制器（如果有的话）的下一个响应者为其管理的视图的父视图；

4、单例的窗口（UIWindow）的内容视图将指向窗口本身作为它的下一个响应者

5、单例的应用（UIApplication）是一个响应者链的终点，它的下一个响应者指向nil，以结束整个循环。
第一响应者（First responder）指的是当前接受触摸的响应者对象（通常是一个UIView对象），即表示当前该对象正在与用户交互，它是响应者链的开端。整个响应者链和事件分发的使命都是找出第一响应者。

UIWindow对象以消息的形式将事件发送给第一响应者，使其有机会首先处理事件。如果第一响应者没有进行处理，系统就将事件（通过消息）传递给响应者链中的下一个响应者，看看它是否可以进行处理。
iOS系统检测到手指触摸(Touch)操作时会将其打包成一个UIEvent对象，并放入当前活动Application的事件队列，单例的UIApplication会从事件队列中取出触摸事件并传递给单例的UIWindow来处理，UIWindow对象首先会使用hitTest:withEvent:方法寻找此次Touch操作初始点所在的视图(View)，即需要将触摸事件传递给其处理的视图，这个过程称之为hit-test view。

UIWindow实例对象会首先在它的内容视图上调用hitTest:withEvent:，此方法会在其视图层级结构中的每个视图上调用pointInside:withEvent:（该方法用来判断点击事件发生的位置是否处于当前视图范围内，以确定用户是不是点击了当前视图），如果pointInside:withEvent:返回YES，则继续逐级调用，直到找到touch操作发生的位置，这个视图也就是要找的hit-test view。

hitTest:withEvent:方法的处理流程如下

1.首先调用当前视图的pointInside:withEvent:方法判断触摸点是否在当前视图内；

若返回NO,则hitTest:withEvent:返回nil;

若返回YES,则向当前视图的所有子视图(subviews)发送hitTest:withEvent:消息，所有子视图的遍历顺序是从最顶层视图一直到到最底层视图，即从subviews数组的末尾向前遍历，直到有子视图返回非空对象或者全部子视图遍历完毕；

若第一次有子视图返回非空对象，则hitTest:withEvent:方法返回此对象，处理结束；

如所有子视图都返回非，则hitTest:withEvent:方法返回自身(self)。





