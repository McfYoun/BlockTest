# BlockTest
描述自己对block的理解，理解有误的地方欢迎大神指出

#import "ViewController.h"

@implementation ViewController
{
//block 作为全局变量
int (^block0)(int);
}

//类型重定义block
typedef int (^blocka)(int);

- (void)viewDidLoad {
[super viewDidLoad];
//初始化全局变量block0
block0 = ^(int a){
NSLog(@"全局变量block0的参数为:%d",a);
return a;
};
block0(1);
blocka block01 = ^(int b){
NSLog(@"类型重定义block,参数为：%d",b);
return 1;
};
block01(2);

//函数内的block
[self blockTest1];

[self para1:2 blockPara:^(int a) {
if (a == 10) {
NSLog(@"callback调用此block时传进来的参数：%d",a);
}else{
NSLog(@"callback调用此block时传进来的参数：%d",a);
}
}];
//block作为返回值
int (^blockBack)(int) = [self blockBack];
blockBack(100);
}

- (void)blockTest1
{
//函数内block

//1.无参数无返回值block
void (^block1)(void) = ^{
NSLog(@"1.无参数无返回值的block");
};
block1();

//2.有参数无返回值block
void (^block2)(int) = ^(int a){
NSLog(@"有参数无返回值block，参数为：%d",a);
};
block2(2);

//3.有参数有返回值的block
int (^block3)(int) = ^(int para3){
NSLog(@"1.有参数有返回值的block,参数为：%d",para3);
return para3 + 1;
};
int back3 = block3(1);
NSLog(@"返回值为：%d",back3);
}

//block 作为函数参数
- (void)para1:(int)p1 blockPara:(void (^)(int a))callback
{
if (p1 == 1) {
callback(10);
}else{
callback(20);
}
}

//block作为返回值
- (int (^)(int back))blockBack
{
int (^blockback)(int) = ^(int a){
NSLog(@"所返回block的参数为：%d",a);
return a;
};
return blockback;
}


- (void)setRepresentedObject:(id)representedObject {
[super setRepresentedObject:representedObject];

// Update the view, if already loaded.
}
