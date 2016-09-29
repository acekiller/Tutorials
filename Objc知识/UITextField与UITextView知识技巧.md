#TextField与UITextView知识技巧

UITextField与UITextView是我们做iOS开发中常用的两个输入空间，或者说是目前iOS中唯一已有的两个文本输入框空间。对于常规的使用还是很简单的。不过，当我们要对这两个控件的展示样式和输入内容做一定处理的时候，就感觉坑太多了。

这篇文章，就是针对笔者自己在这上面遇到的坑整理成文章的。下面就先介绍一下这篇文章涉及到的点吧:

1. 文字长度限制的问题;
2. 右对齐输入空格不显示的问题;
3. 自定义键盘切换的问题;
4. UITextField明文与密文的切换显示问题;
5. UITextView设置边距的问题

首先我们要讨论的是关于UITextField与UITextView的输入长度限制的问题。还记得我们常常采用的处理方式么怎样的吧。我们只需要分别对UItextField的代理协议
－ (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string和UITextView的代理协议- (BOOL)textView:(UITextView *)textView shouldChangeTextInRange:(NSRange)range replacementText:(NSString *)text实现并判断文字长度就好了。好吧，似乎一切很OK。特别是禁用了词汇联想功能的情况下，似乎丝毫不会有问题。

## 4 UITextField明文与密文的切换显示问题
当调用对UITextField在明文和密文之间切换是，又于文字长短的不一致，或导致光标和文字间存在空白等问题。产生这种问题在于界面未重绘。这是一个很好的原因解释，事实也应该如此。这样的话，似乎我们可以通过调用- (void)setNeedsLayout来解决，然而并没有效果。好吧仔细分析一下，其实这个不执行也是有可能的，因为我们没修改过界面的任何内容，无法触发contentSize从新计算，也许是苹果出于处理优化吧，对切换之后进行类容显示也没有，触发从新计算contentSize。既然这样，我们可以猜测内容contentSize的修改可能性(根据经验判断来推测吧，对于一些不确定的可以通过修改设置来观察界面变化做出推测判断)：

1. 文字发生变化；
2. 显示的字体变化；

<pre>
示例1
<code>
UITextField *textField;
 
....

NSString *text = self.securityField.text;
static BOOL isSecurity = NO;
BOOL isSecurity = !isSecurity;
[textField setSecureTextEntry: isSecurity];
textField.text = @"";
textField.text = text;
</code>
</pre>

    
<pre>
示例2
<code>
UITextField *textField;

...

static BOOL isSecurity = NO;
BOOL isSecurity = !isSecurity;
[self.securityField setSecureTextEntry: isSecurity];
self.securityField.font = [UIFont systemFontOfSize: 12.f];
self.securityField.font = [UIFont systemFontOfSize: 17.f];
</code>
</pre>
对