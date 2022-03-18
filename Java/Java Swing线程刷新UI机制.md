# Java Swing线程刷新UI机制

## 1. java中进度条不能更新问题的研究

> 感谢大佬：https://blog.csdn.net/smartcat86/article/details/2226681

为什么进度条在事件处理过程中不更新，而是在完成后，从0%调到100%？
分两种情况：
1）在AWT事件线程中执行的操作
当 应用程序在事件线程中执行长时间的操作时，会阻塞正常的AWT事件处理，因此阻止了重绘操作的发生。这同常会在下列情况下发生：应用程序响应一个来自用户 界面的请求时，在连接到一个按钮或其他GUI组件的事件处理程序中执行任务，任务的内容可能会需要较长时间，使事件线程挂起，直至远程系统发出答复为止。 当应用程序调用JProgressBar的setValue方法时，进度条可能更新期内部状态并调用repaint，这样做会把一个事件放置到AWT事件 队列中。不幸的是，直至应用程序的事件处理程序完成其处理并把控制权返回到线程的事件处理循环，才能处理该事件。
可以通过调用JComponent的paintImmediately方法来这样做，该方法有两种形式：
public void paintImmediately(int x, int y, int width, int height);
public void paintImmediately(Rectangel rect);
例如：
Dimension d = bar.getSize();
Rectangel rect = new Rectangle(0,0, d.width, d.height);
…
bar.setValue(progressValue);
bar.paintImmediately(rect);
…
2）在另一个线程中执行的操作
如 果在一个单独的线程中执行该操作，当调用进度条的setValue方法，它的更新不会出现任何问题，问题在于，后台线程必须调用JProgressBar 的setValue。而Swing组件只有在事件线程中才能安全的访问。因此，从执行实际工作的线程调用setValue方法是不安全的！解决的方法是使 用SwingUtilites的invokeLater方法，让AWT事件线程稍后进行setValue调用。
例如：
…
SwingUtilities.invokeLater(new Runnable() {
public void run() {
bar.setValue(value);
}
});
…
还有一种可能，不能再线程中改变swing组件，例如，不能从线程调用label.setText，但是可以使用EventQueue类的invokeLater和invokeAndWait方法，以便在事件调度线程中执行该调用程序。（From Core Java）

## 2. Swing 刷新组件java swing中两大原则: 1. 不要阻塞UI线程 2. 不要在UI线程外的线程去操作UI控件

> 感谢大佬：https://blog.csdn.net/u010536134/article/details/51434568

***Swing中事件处理和绘画代码都在一个单独的线程中执行，这个线程就叫做事件分发线程。***

java swing中两大原则:

**1. 不要阻塞UI线程
\2. 不要在UI线程外的线程去操作UI控件**



```
package com.test.loader;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
 
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.SwingUtilities;
 
public class LabelDemo extends JPanel implements ActionListener{
    private static final long serialVersionUID = 1L;
    private JLabel label2;
 
    public LabelDemo() {
        super(new GridLayout(2,1));
        JButton b1 = new JButton("click me");
        b1.addActionListener(this);
        label2 = new JLabel("Label");
        add(label2);
        add(b1);
    }
 
    private static void createAndShowGUI() {
        JFrame frame = new JFrame("LabelDemo");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.add(new LabelDemo());
        frame.pack();
        frame.setVisible(true);
    }
 
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                createAndShowGUI();
            }
        });
    }
 
    @Override
    public void actionPerformed(ActionEvent e) {
        new Thread(new Runnable(){
            @Override
            public void run() {
                for(int i = 0 ; i < 10 ; i ++){
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e1) {}
                    final int x =i;
                    SwingUtilities.invokeLater(new Runnable(){
                        @Override
                        public void run() {
                            label2.setText(x + "");
                        }
                    });
                }
            }
        }).start();
    }
}
```

## 3.Java Swing GUI多线程之SwingUtilities.invokeLater和invokeAndWait

> 感谢大佬：https://blog.csdn.net/guo583/article/details/84124985

在Java中Swing是线程不安全的，是单线程的设计，这样的造成结果就是：只能从事件派发线程访问将要在屏幕上绘制的Swing组件。事件派发线程是 调用paint和update等回调方法的线程，它还是事件监听器接口中定义的事件处理方法，例如，ActionListener中的 actionPerformed方法在事件派发线程中调用。

Swing是事件驱动的，所以在回调函数中更新可见的GUI是很自然的事情，比如，有一个按钮被按下，项目列表需要更新时，则通常在与该按钮相关联的事件 监听器的actionPerformed方法中来实现该列表的更新，从事件派发线程以外的线程中更新Swing组件是不正常的。

有时需要从事件派发线程以外的线程中更新Swing组件，例如，在actionPerformed中有很费时的操作，需要很长时间才能返回，按钮激活后需 要很长时间才能看到更新的列表，按钮会长时间保持按下的状态只到actionPerformed返回，一般说来耗时的操作不应该在事件处理方法中执行，因 为事件处理返回之前，其他事件是不能触发的，界面类似于卡住的状况，所以在独立的线程上执行比较耗时的操作可能更好，这会立即更新用户界面和释放事件派发 线程去派发其他的事件。

SwingUtilities类提供了两个方法：invokeLate和invoteAndWait，它们都使事件派发线程上的可运行对象排队。当可运行 对象排在事件派发队列的队首时，就调用其run方法。其效果是允许事件派发线程调用另一个线程中的任意一个代码块。

只有从事件派发线程才能更新组件。

程序示例：更新组件的错误方法
startButton.addActionListener(new ActionListener())
{
public void actionPerformed(ActionEvent e)
{
GetInfoThread t = new GetInfoThread(Test.this);
t.start();
startButton.setEnabled(false);
}
}

class GetInfoThread extends Thread
{
Test applet;
public GetInfoThread(Test applet)
{
this.applet = applet;
}

public void run()
{
while (true)
{
try
{
Thread.sleep(500);
applet.getProgressBar().setValue(Math.random() * 100);
}
catch (InterruptedException e)
{
e.printStackTrace();
}
}
}
}

错误分析：在actionPerformed中，监听器把按钮的允许状态设置为false，由于是在事件派发线程上调用 actionPerformed，所以setEnabled是一个有效的操作，但是在GetInfoThread中设置进度条是一个危险的做法，因为事件 派发线程以外的线程更新了进度条，所以运行是不正常的。

1、invokeLater使用
class GetInfoThread extends Thread
{
Test applet;

Runnable runx;

int value;

public GetInfoThread(final Test applet)
{
this.applet = applet;
runx = new Runnable()
{
public void run()
{
JProgressBar jpb = applet.getProgressBar();
jpb.setValue(value);
}
}
}

public void run()
{
while (true)
{
try
{
Thread.sleep(500);
value = (int) (Math.random() * 100);
System.out.println(value);
SwingUtilities.invokeLater(runx);
}
catch (InterruptedException e)
{
e.printStackTrace();
}
}
}
}

2、invokeAndWait
与invoikeLater一样，invokeAndWait也把可运行对象排入事件派发线程的队列中，invokeLater在把可运行的对象放入队列 后就返回，而invokeAndWait一直等待知道已启动了可运行的run方法才返回。如果一个操作在另外一个操作执行之前必须从一个组件获得信息，则 invokeAndWait方法是很有用的。

class GetInfoThread extends Thread
{
Runnable getValue,setValue;
int value,currentValue;
public GetInfoThread(final Test applet)
{
getValue=new Runnable()
{
public void run()
{
JProgressBar pb=applet.getProgressBar();
currentValue=pb.getValue();
}
};
setValue=new Runnable()
{
public void run()
{
JProgressBar pb=applet.getProgressBar();
pb.setValue(value);
}
}
}

public void run()
{
while(true)
{
try
{
Thread.currentThead().sleep(500);
value=(int)(Math.random()*100);
try
{
SwingUtilities.invokeAndWait(getValue);//直到getValue可运行的run方法返回后才返回
}
catch(Exception ex)
{

}
if(currentValue!=value)
{
SwingUtilities.invokeLater(setValue);
}
}
catch(Exception ex)
{
}
}
}
invokeLater和invoikeAndWait的一个重要区别：可以从事件派发线程中调用invokeLater，却不能从事件派发线程中调用 invokeAndWait，从事件派发线程调用invokeAndWait的问题是：invokeAndWait锁定调用它的线程，直到可运行对象从事 件派发线程中派发出去并且该可运行的对象的run方法激活，如果从事件派发线程调用invoikeAndWait，则会发生死锁的状况，因为 invokeAndWait正在等待事件派发，但是，由于是从事件派发线程中调用invokeAndWait，所以直到invokeAndWait返回后 事件才能派发。

actionPerformed();返回的时候事件派发线程才能派发线程，而在actionPerformed中使用invokeAndWait则会导致actionPerformed不能返回。所以也就无法派发invokeAndWait中的线程。

由于Swing是线程不安全的，所以，从事件派发线程之外的线程访问Swing组件是不安全的，SwingUtilities类提供这两种方法用于执行事件派发线程中的代码

总结: GUI中多线调用方法应该使用:SwingUtilities.invokeLater和invokeAndWait 而不是普通情况下那样应用.

看到很多地方讲述Swing中的并发和多线程问题，感觉讲的都不如Sun的教程，这里复述一下关键。Swing之所以和多线程紧密联系在一 起是因为图形界面编程中如果只采取顺序编程（也就是你的代码或任务依次执行），会出现很大的问题，比如你要编写一个FTP客户端，你不能让文件下载的时 候，用户界面死在那里，你既不能取消任务也不能和界面交互吧。所以有必要将耗时的任务，比如文件下载放到一个独立的线程中处理，而让用户同时能够干其他事 情。简单来说，Swing中有三种线程：

启动线程或者初始线程： 这个线程负责调用main方法，很多顺序编程一开始就用的是这种线程。在Swing中启动线程负责很少的事务，主要干两件事情，第一件就是创建一个可运行 的对象(Runnable Object),这个可运行对象的任务比较重要，它负责初始化图形界面，第二件就是将这个可运行对象安排到另外一个非常重要的线程，事件分派线程中执行。 第二件事情是通过SwingUtilies的invokeLater和invokeAndWait方法来实现的。几乎所有的创建Swing组件和与 Swing组件交互的代码都要在事件分派线程中执行。
事件分派线程：在Swing中负责事件处理的代码需要在一个特定的线程中运行，这个线程就 是事件分派线程。大部分调用Swing方法的代码也在这个线程中运行。原因是大部分Swing对象中的方法并不是线程安全的，所以需要这个特定的事件分派 线程来保证线程安全。当然也有部分swing对象中的方法指明是线程安全的，这些方法可以在任何线程中调用。你可以将事件分派线程中运行的代码想象成一系 列短小的任务，大部分任务都是调用事件处理方法，例如ActionListener.actionPerformed()方法，其他任务可被程序代码通过 SwingUtilities的invokeLater/invokeAndWait方法来安排。需要注意的是，在事件分派线程中的任务必须短小精悍，这 意味着这些任务能够很快执行完毕，如果你发现有一个耗时的任务，那么你肯定出错了，你会发现你的图形界面经常被卡住，或者死掉了。对于耗时任务你需要另外 一个线程，例如工作线程(Worker Thread)来处理。判断你的代码时候运行在事件分派线程上的方法很简单，使用 javax.swing.SwingUtilities.isEventDispatchThread()方法即可。
工作线程(Worker Thread)或者后台线程(Background Thread)：你可以在这个线程中处理耗时任务。

如何使用线程
　　Java平台从开始就被设计成为多线程环境。在你的主程序执行的时候，其它作业如碎片收集和事件处理则是在后台进行的。本 质上，你可以认为这些作业是线程。它们正好是系统管理线程，但是无论如何，它们是线程。线程使你能够定义相互独立的作业，彼此之间互不干扰。系统将交换这 些作业进或出CPU，这样（从外部看来）它们好象是同时运行的。
　　
　　在你需要在你的程序中处理多个作业时，你也可以使用多个进程。这些进程可以是你自己创建的，你也可以操纵系统线程。
　　
　　你进行这些多作业处理，要使用几个不同的类或接口：
　　
　　java.util.Timer类
　　javax.swing.Timer类
　　Thread类
　　Runnable接口
　　对于简单的作业，通常需要重复的，你可以使用java.util.Timer类告诉它“每半秒钟做一次”。注意：大多数系统例程是使用毫秒的。半秒钟是500毫秒。
　　
　　你希望Timer实现的任务是在java.util.TimerTask实例中定义的，其中运行的方法包含要执行的任务。这些在Hi类中进行了演示，其中字符串“Hi”重复地被显示在屏幕上，直到你按Enter键。
import java.util.*;

public class Hi {
public static void main(String args[]) throws java.io.IOException {
TimerTask task = new TimerTask() {
public void run() {
System.out.println(“Hi”);
}
};
Timer timer = new Timer();
timer.schedule(task, 0, 500);
System.out.println(“Press ENTER to stop”);
System.in.read(new byte[10]);
timer.cancel();
}
}

Java Runtime Environment工作的方式是只要有一个线程在运行，程序就不退出。这样，当取消被调用，没有其它线程在运行了，则程序退出。有一些系统线程在运 行，如碎片收集程序。这些系统线程也被称为后台线程。后台线程的存在不影响运行环境被关闭，只有非后台线程保证运行环境不被关闭。
　　
　 　Javax.swing.Timer类与java.util.timer类的工作方式相似，但是有一些差别需要注意。第一，运行的作业被 ActionListener接口的实现来定义。第二，作业的执行是在事件处理线程内部进行的，而不象java.util.Timer类是在它的外部。这 是很重要的，因为它关系到Swing组件集是如何设计的。
　　
　　如果你不熟悉Swing，它是一组可以被Java程序使用的图形组件。 Swing被设计程被称为单线程的。这意味着对Swing类内部内容的访问必须在单个线程中完成。这个特定的线程是事件处理线程。这样，例如你想改变 Label组件的文字，你不能仅仅调用Jlabel的setText方法。相反，你必须确认setText调用发生在事件处理线程中，而这正是 javax.swing.Time类派的上用场的地方。
　　
　　为了说明这第二种情况，下面的程序显示一个增加的计数器的值。美半秒钟计数器的数值增加，并且新的数值被显示。
　　
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Count {
public static void main(String args[]) {
JFrame frame = new JFrame();
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
Container contentPane = frame.getContentPane();
final JLabel label = new JLabel("", JLabel.CENTER);
label.setFont(new Font(“Serif”, Font.PLAIN, 36));
contentPane.add(label, BorderLayout.CENTER);
ActionListener listener = new ActionListener() {
int count = 0;

public void actionPerformed(ActionEvent e) {
count++;
label.setText(Integer.toString(count));
}
};
Timer timer = new Timer(500, listener);
timer.start();
frame.setSize(300, 100);
frame.show();
}
}
　　
　　上述程序的结果是：
　　[[The No.1 Picture.]]
　　万 一你要做的不是一个简单的重复作业，java.lang.Thread类就派上了用场。它允许你自己控制基本功能。通过创建Thread的一个子类，你可 以使你的系统脱离，并进行一个长时间运行的作业，如从网络上读取一个文件，而不阻碍你的其它程序的运行。这种长时间运行的作业将在run方法中定义。
　　
　　第二种方式是创建Thread类的子类并在子类中实现run方法，或在实现runnable的类中实现run方法，并将这个实现传递给Thread的构造函数。
　　
　　你可能会问有什么区别。Java编程语言仅支持单一继承。如果你设计的调用是除了Thread以外的其它类，你可以是你的类实现Runnable，而它可以是你的作业被执行。否则，你定义Thread的子类来运行你的Run方法，在处理过程中不再添加其它操作。
　　
　 　对于创建Thread子类的第三种情况，下面的程序生成了一个新的线程来计算一个特定URL的字符数，这个URL是通过命令行传递进来的。在这进行过程 之中，实现Runnable的第四种情况被演示，打印出重复的消息。注意在实现Runnable的这后一种情况下，你必须提供重复消息的代码。你必须同时 sleep，以分配时间并完成操作。在两种情况下，与使用Timer相比较。这段程序的最后一部分包含有你从命令行读取命令以触发程序结束。注意在系统读 取URL并打印消息的同时，你总可以按Enter键结束程序。

import java.io.*;
import java.net.*;

public class Both {
public static void main(String args[]) {
final String urlString = args[0];
final String message = args[1];
Thread thread1 = new Thread() {
public void run() {
try {
URL url = new URL(urlString);
URLConnection connection = url.openConnection();
InputStreamReader isr = new InputStreamReader(connection
.getInputStream());
BufferedReader reader = new BufferedReader(isr);
int count = 0;
while (reader.read() != -1) {
count++;
}
System.out.println("Size is : " + count);
reader.close();
} catch (MalformedURLException e) {
System.err.println("Bad URL: " + urlString);
} catch (IOException e) {
System.err.println(“I/O Problems”);
}
}
};
thread1.start();
Runnable runnable = new Runnable() {
public void run() {
while (true) {
System.out.println(message);
try {
Thread.sleep(500);
} catch (InterruptedException e) {
}
}
}
};
Thread thread2 = new Thread(runnable);
thread2.start();
try {
System.out.println(“Press ENTER to stop”);
System.in.read(new byte[10]);
} catch (IOException e) {
System.out.println(“I/O problems”);
}
System.exit(0);
}
}
　　因为有多种方式来处理线程，你选用哪种技术取决于你和你面临的条件。要成为一个有效的Java编程人员，尽管你通常不必学习Java编程语言的所有内容和核心库，但是线程是一个例外。你越早了解线程如何工作和如何使用线程，你将越早了解Java程序如何工作和交互

## 4. Swing理解Swing中的事件与线程

> 感谢大佬：http://www.360doc.com/content/16/1017/23/31775152_599223057.shtml
> talk is cheap ， show me the code.

Swing中的事件事件驱动
所有的GUI程序都是事件驱动的。Swing当然也是。

GUI程序不同于Command Line程序，一个很大的区别是程序执行的驱动条件：命令行程序是接受用户输入的文本参数，对命令解析，然后通过类似switch的选择来执行不同的功能模块。而GUI程 序就不一样了。GUI程序由界面元素组成，如Button，CheckBox，TextArea，等等。用户操作不同的组件，就会引发不同的事件，然后， 程序编写时注册到UI组件上的事件处理程序得到调用，以此来和用户交互。
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191129163313114.png)](https://img-blog.csdnimg.cn/20191129163313114.png)
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191129163315529.png)](https://img-blog.csdnimg.cn/20191129163315529.png)
事件Event
事件有点类似于异常：事件是事件类的对象，它携带了事件相关的信息，异常是异常类的对象，他携带了异常信息。无论是异常，还是事件

发生时，我们的程序都要事先写好相应的代码应对并处理。只不过，对于程序员来说，事件是正派的，而异常则是反派，谁也不希望自己的程序出现异常。

java中，所有的事件类都是EventObject类的子类，所有的事件都有一个成员字段：source用来保存事件源，即引发事件的对象。

public class EventObject implements java.io.Serializable { private static final long serialVersionUID = 5516075349620653480L; /* source保存 引发事件的对象的引用*/ protected transient Object source; public EventObject(Object source) { if (source == null) throw new IllegalArgumentException(‘null source’); this.source = source; } public Object getSource { return source; }
public String toString { return getClass.getName + ‘[source=’ + source + ‘]’; } }
Swing的事件机制由AWT提供，下面是Swing中常用的高级事件 ActionEvnet类的部分代码。还有其他事件。

public class ActionEvent extends AWTEvent
{ public ActionEvent(Object source, int id, String command, long when, int modifiers) { super(source, id); this.actionCommand = command; this.when = when; this.modifiers = modifiers; }
//… }
事件源EventSource
异常，有引发异常的原因，事件，也有引发事件的对象，这就是事件源。谁引发了事件，谁就是事件源。

比如，Button被点击时引发事件，Button就是事件源，JFrame 状态变化时，JFrame也是事件源。Swing中所有的组件，都有感知自己被操作的能力。

Swing中，事件源一般是一些用户组件，他们能感知用户的操作，并引发相应的事件，最后通知对自己注册的监听器。

事件源都会提供事件的注册接口，所有对某个组件的某个事件感兴趣的其他代码，都可以提前注册到这个组件上，事件发生时，此组件就会调用相应的注册的

事件处理程序。

下面是JButton的父类 AbstractButton的一个方法。

protected void fireActionPerformed(ActionEvent event) { // Guaranteed to return a non-null array Object listeners = listenerList.getListenerList; ActionEvent e = null; // Process the listeners last to first, notifying // those that are interested in this event for (int i = listeners.length-2; i>=0; i-=2) { if (listeners[i]==ActionListener.class) { // Lazily create the event: if (e == null) { String actionCommand = event.getActionCommand; if(actionCommand == null) { actionCommand = getActionCommand; }
e

= new ActionEvent(AbstractButton.this, ActionEvent.ACTION_PERFORMED, actionCommand, event.getWhen, event.getModifiers); } ((ActionListener)listeners[i+1

]).actionPerformed(e);

} } }
监听者Listener
监听者（有的也叫侦听器）：实现了某个监听接口的类对象。某个类实现了一个监听器接口，它就是一个监听者。

当事件发生时，并不是事件源处理事件，而是注册在事件源的上的监听器去处理。事件源只是通知监听器，通知实质是调用所有监听器对象按接口约定实现的的接口方法。

我们知道，对象实现了某个接口，就代表这个对象能做什么。同理，一个对象想成为监听器，它就必须实现相应的监听器接口，表明他有处理某个事件的能力。

监听器实现了监听接口，就必然要实现接口中定义的方法，用来应对事件。

所有的监听器接口都必须扩展自EventListener,它是一个空接口。一个事件往往对应一个监听者接口。

JComponnet类是所有Swing组件的父类。JComponnet 类中有一个 EventListenerList成员，它是一个表，用来存储所有注册的监听者。那也就是说，所有的Swing组件内部都包含一个存储监听者的列表，这也是为什么能向Swing组件中注册监听器的本质。

public abstract class JComponent extends Container implements Serializable,TransferHandler.HasGetTransferHandler
{ /** A list of event listeners for this component. */ protected EventListenerList listenerList = new EventListenerList; //… }
/**
EventListenerList类 这是一个用于保存监听器的一个表类型。这个表可以存储任何类型的EventListener，因为内部是用的一个Object数组存储的。 */ public class EventListenerList implements Serializable { protected transient Object listenerList = NULL_ARRAY; //获取所有监听者的数组 public Object getListenerList { return listenerList; }
/** * 返回监听者的数量*/ public int getListenerCount { return listenerList.length/2; } /** 向监听者列表中添加 “一对” 新的监听者。其实是添加一个监听者， 只不过对于一个监听者需要保存2项：监听者的类 t，和监听者本身 l */ public synchronized void add(Class t, T l) { if (l==null) {return;} if (!t.isInstance(l)) { throw new IllegalArgumentException(‘Listener ’ + l +’ is not of type ’ + t); } if (listenerList == NULL_ARRAY) { //如果是第一次添加监听者，则 new 一个Object 数组。 listenerList = new Object { t, l }; } else { int i = listenerList.length; Object tmp = new Object[i+2]; System.arraycopy(listenerList, 0, tmp, 0, i); tmp[i] = t; tmp[i+1] = l; listenerList = tmp; } } }
这个时候你再回去看事件源分块中的那段代码，是不是思路清晰许多了呢？

所以，事件源通知监听者，实质是遍历内部的监听者表，将自己作为EventSorece，构造一个事件对象，并调用所有监听者的事件处理程序时，将构造的事件对象传递过去。

如果你还是有点迷糊，下面通过一例子说明下。

下面是一个简单的Swing程序。

监听者：ButtonClickListener 类对象，它实现了监听器接口。一般我们会使用匿名内部类完成监听者的实例化，这里写出成员内部类是为了更清晰。当使用addActionListener方法注册后，ButtonClickListener对象就被存储在Button对象内部的一个EventListenerList列表中了。

事件 ：点击Button时生成。

事件源：被点击的Button对象。

import java.awt.Dimension;import java.awt.event.ActionEvent;import java.awt.event.ActionListener;import javax.swing.JButton;import javax.swing.JFrame;import javax.swing.JLabel;import javax.swing.JPanel;import javax.swing.SwingUtilities;public class SwingDrive { public static void main(String[] args) { SwingUtilities.invokeLater(new Runnable { @Override public void run { JFrame frame = new TestFrame(‘测试’); frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); frame.setVisible(true); } }); }}class TestFrame extends JFrame{ private static final int FRAME_WIDTH = 530; private static final int FRAME_HEIGHT = 360; /****\**\*\*\*\*\*\*\*View\*\*\*\*\*\*\*\*\**********/ private JPanel mainPanel = null; private JButton msgButton = null; private JLabel msgLabel = null; public TestFrame(String title) { super(title); initUI; } private void initUI { //内容面板 mainPanel = new JPanel; mainPanel.setPreferredSize(new Dimension(FRAME_WIDTH,FRAME_HEIGHT)); this.setContentPane(mainPanel); //按钮 msgButton = new JButton(‘我是按钮’); //监听者表示对按钮的点击事件感兴趣，于是注册到按钮上。 msgButton.addActionListener(new ButtonClickListener); //msg显示文本 msgLabel = new JLabel; //将组建添加到窗体的内容面板中 this.add(msgButton); this.add(msgLabel); this.pack; } /*监听者，实现了监听接口*/ private class ButtonClickListener implements ActionListener { @Override public void actionPerformed(ActionEvent e) { msgLabel.setText(‘你点击了按钮’); } }}
还有一点疑问
who invoke the fireActionPerformed(ActionEvent event) method？

谁调用了JButton的fireActionPerformed方法呢？

如果你能想到这个问题，说明你已经开始深入了。这是Swing本身的机制，确切说是AWT提供的机制。一个Swing程序中会有一个toolkit线程不断运行着，它监视用户对组件的操作，当组件被点击，获取焦点，被最大化，状态改变等，都会被toolkit线程发现，并将fireXXX发送带EDT中执行，fireXXX的执行，又会导致所有监听器的执行。

先不急，这涉及到Swing线程的知识，请往下看。

Swing中的线程
1、主线程，main方法，程序执行的入口。任何程序都必须有的。

2、初始化线程。创建和初始化图形界面。

3、tookit线程：负责捕捉系统事件，如鼠标，键盘等。负责感知组件的操作，并将事件发通知EDT。

4、EDT线程：处理Swing中的各种事件。UI绘制，UI的修改操作,UI的绘制渲染.，监听者的事件处理函数，等。所有的UI操作都必须在EDT线程中执行，不允许在其他线程中。

5、N个后台工作线程：处理耗时任务，如网络资源下载，可能阻塞的IO操作。

初始化线程

public static void main(String [] args){ SwingUtilities.invokeLater(new Runnable{ public void run { //初始化线程逻辑代码在这里执行 } }); }
Swing多线程的执行
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191221001010680.gif)](https://img-blog.csdnimg.cn/20191221001010680.gif)
图画完后，我才发现图画的有一问题：其中EDT线程和toolkit线程是循环线程，并没有确切的执行终点，也就是不知道这2个线程什么时候执行任务到100%。只要Swing程序没有结束，他们就一直工作，因为用户可能在任何时候执行UI操作。

后台工作线程当执行完任务后就结束了。

一、不要在EDT线程中执行耗时的任务。

一旦EDT线程被阻塞，UI组件就不能及时渲染，更新，使得整个程序失去对用户的响应。用户体验十分糟糕。

Swing本身是设计为单线程操作的,并非线程安全的.这就意味着:所有的UI操作都会必须在EDT线程中进行。内置的组件都是遵守这个约定的，比如一个JButton被按下时，它需要显示为按下的状态，那么，这个渲染为按下的状态，就会以事件的形式发布到EDT线程中去执行。同样，按钮弹起时，需要渲染为普通状态，也会引发事件，并在EDT中处理。

不要让EDT干 ‘体力活’。很明显，Swing中组件UI的更新，都会形成事件置于事件队列，并等待EDT派发，也就是UI更新依赖EDT线程完成。如果你的事件处理程序太耗时了，那么，UI就很久得不到及时更新，造成界面假死现象。

下面这个程序中，用户点击下载按钮后，真个界面都失去了响应，按钮久久不能弹起，窗口也失去了响应，体验很糟糕。
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20191129163404619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY3MDgwMg==,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/20191129163404619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY3MDgwMg==,size_16,color_FFFFFF,t_70)
class BadFrame extends JFrame { public BadFrame { super; initUI; } private JButton downloadButton ; private JPanel mainPane ; private void initUI { mainPane = new JPanel; mainPane.setPreferredSize(new Dimension(430,250)); this.setContentPane(mainPane); downloadButton = new JButton(‘下载’); this.getContentPane.add(downloadButton); downloadButton.addActionListener(new ActionListener { @Override public void actionPerformed(ActionEvent e) { downloadMovie; } }); this.pack; } //模拟下载任务 private void downloadMovie { try { Thread.sleep(5000); } catch (InterruptedException e) { // TODO Auto-generated catch block e.printStackTrace; } }}
二、不要在非EDT线程中访问UI，操作UI组件。

Swing组件都不是线程安全的，只有把他们的操作限制在一个线程中，才能保证所有的UI的操作都符合预期。这个线程就是EDT线程。那么，怎样将UI操作发送到EDT中执行呢？

通过以下之一。

1 SwingUtilities.invokeLater(new Runnable {2 3 @Override4 public void run {5 6 7 }8 });
9
1 SwingUtilities.invokeAndWait(new Runnable {2 3 @Override4 public void run {5 // TODO Auto-generated method stub6 7 }8 });
9
他们有什么区别？

SwingUtilities.invokeLater调用后立即返回。然后执行第9行后的代码。其他线程和 invokeLater中的参数线程异步执行。互不阻塞。

SwingUtilities.invokeAndWait调用后，必须等到 线程对象 run方法在EDT中执行完了，才返回，然后继续执行第9行后的代码。

下面是一个简单的例子：用户输入2个整数 start ，end，程序计算从start 累加到end 的结果。我依然使用了线程睡眠来模拟耗时任务。因为如果我使用更加贴近现实的例子的话，又会引出更多的知识点。

虽然简单，但说明了如何让Swing更好的工作。

import java.awt.Dimension;import java.awt.GridLayout;import java.awt.event.ActionEvent;import java.awt.event.ActionListener;import javax.swing.JButton;import javax.swing.JFrame;import javax.swing.JLabel;import javax.swing.JOptionPane;import javax.swing.JPanel;import javax.swing.JTextField;import javax.swing.SwingUtilities;public class Demo { public static void main(String[] args) { SwingUtilities.invokeLater(new Runnable { @Override public void run { MFrame frame = new MFrame; frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); frame.setVisible(true); } }); }}class MFrame extends JFrame{ public MFrame { initUI; onButtonClick; } /***\**\*\*\*\*\*\*\*\*\*\*Model\*\*\*\*\*\*\*\*\*\**\**/ private int start = 0; private int end = 0; private int result = 0; /\**\*\*\*\*\*\*\*\*\*\*View\*\*\*\*\*\*\*\*\*\**\****/ private JButton calcButton = null; private JTextField startField = null; private JTextField endField = null; private JTextField resultField = null; private JPanel mainpane = null; private void initUI { calcButton =new JButton(‘计算’); startField = new JTextField; startField.setColumns(5); endField = new JTextField; endField.setColumns(5); resultField = new JTextField; resultField.setColumns(5); resultField.setEditable(false); mainpane = new JPanel(new GridLayout(1, 4,5,0)); mainpane.setPreferredSize(new Dimension(300,50)); mainpane.add(startField); mainpane.add(endField); mainpane.add(resultField); mainpane.add(calcButton); this.setContentPane(mainpane); this.setLocationRelativeTo(null); this.pack; } //为button注册监听者 private void onButtonClick { calcButton.addActionListener(new ActionListener { @Override public void actionPerformed(ActionEvent event) { Thread calcThread = new Thread(new Runnable { @Override public void run { try{ start = Integer.parseInt(startField.getText); end = Integer.parseInt(endField.getText); for (int i = start; i <=end; i++)="" {="" result="" +=“i;” 假设计算过程十分耗时，就像挖矿一样。="" thread.sleep(500);="" }="" 耗时任务完成后了，通过swingutilities.invokelater将设置任务到ui的事件发送到edt线程中。="" swingutilities.invokelater(new="" runnable="" {="" @override="" public="" void="" run="" {="" resultfield.settext(result+’’);="" }="" });="" }="" catch(numberformatexception="" e)="" {="" joptionpane.showmessagedialog(mframe.this,="" ‘请输入一个合法的整数’,="" ‘错误’,="" joptionpane.error_message);="" }="" catch="" (interruptedexception="" e)="" {="" system.out.println(‘计算时错误’);="" }="" }="" });="" wrok="" thread="" new="" end="" calcthread.start;="" 启用任务线程="" }="" });="">更优雅的解决办法：SwingWorker线程类
当Swing程序复杂后，自定义线程会让代码越来越庞大，不好理解。于是jdk1.6中引入了SwingWorker线程类，简化了程序员的工作。今天就写到这里，我会在以后的文章中介绍。😃

------

> 案例参考：
> https://blog.csdn.net/hza419763578/article/details/80690689
> https://blog.csdn.net/paullinjie/article/details/51728930

> 补充：http://www.360doc.com/content/19/1212/21/67887324_879362148.shtml



__EOF__

![img](https://pic.cnblogs.com/avatar/1681943/20200401090321.png)

**本文作者**：**[TF-STUDY NOTES](https://www.cnblogs.com/tfxz/p/12621590.html)**
**本文链接**：https://www.cnblogs.com/tfxz/p/12621590.html
**关于博主**：评论和私信会在第一时间回复。或者[直接私信](https://msg.cnblogs.com/msg/send/tfxz)我。
**版权声明**：本博客所有文章除特别声明外，均采用 [BY-NC-SA](https://creativecommons.org/licenses/by-nc-nd/4.0/) 许可协议。转载请注明出处！
**声援博主**：如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。您的鼓励是博主的最大动力！

个人学习笔记！仅以学习为目的，感谢各位前辈！

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/1681943/20200401090321.png)](https://home.cnblogs.com/u/tfxz/)

[超级小白龙](https://home.cnblogs.com/u/tfxz/)
[关注 - 9](https://home.cnblogs.com/u/tfxz/followees/)
[粉丝 - 86](https://home.cnblogs.com/u/tfxz/followers/)

[+加关注](javascript:void(0);)

1

0

[« ](https://www.cnblogs.com/tfxz/p/12621592.html)上一篇： [Java socket中关闭IO流后，发生什么事？（以关闭输出流为例）](https://www.cnblogs.com/tfxz/p/12621592.html)
[» ](https://www.cnblogs.com/tfxz/p/12621589.html)下一篇： [在TCP文件传输中如何判断java流的末尾](https://www.cnblogs.com/tfxz/p/12621589.html)

posted @ 2019-11-29 16:36 [超级小白龙](https://www.cnblogs.com/tfxz/) 阅读(1199) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=12621590) [收藏](javascript:void(0)) [举报](javascript:void(0))





[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/tfxz/p/12621590.html#)[返回顶部](https://www.cnblogs.com/tfxz/p/12621590.html#top)

登录后才能查看或发表评论，立即 [登录](javascript:void(0);) 或者 [逛逛](https://www.cnblogs.com/) 博客园首页

[【推荐】百度智能云 2022 开年见礼，开发者上云优惠专场在等你](https://cloud.baidu.com/campaign/2022developer/index.html?track=a3bf76b1cfd5f7267f7e29bd69523019a0fc7b905e4d4cf9#cloud)

**编辑推荐：**
· [2021 .NET Conf China 主题分享之-轻松玩转.NET大规模版本升级](https://www.cnblogs.com/tianqing/p/15938703.html)
· [理解 OAuth2.0 协议和授权机制](https://www.cnblogs.com/CKExp/p/15938916.html)
· [Asp.net core IdentityServer4 与传统基于角色的权限系统的集成](https://www.cnblogs.com/xiaxiaolu/p/15929063.html)
· [记一次 .NET 某供应链WEB网站 CPU 爆高事故分析](https://www.cnblogs.com/huangxincheng/p/15928029.html)
· [从 Mongo 到 ClickHouse 我到底经历了什么？](https://www.cnblogs.com/1wen/p/15921343.html)

**最新新闻**：
· [特斯拉开始在加拿大推出全自动驾驶 FSD Beta 测试版](https://news.cnblogs.com/n/714648/)
· [华为应用市场全球月活跃用户达5.8亿 未来5年到10年聚焦全场景智慧生态](https://news.cnblogs.com/n/714647/)
· [苹果第八大股东表态：将投票反对苹果管理层薪酬计划](https://news.cnblogs.com/n/714646/)
· [累计46万公里 9年前的特斯拉Model S还能跑多远？](https://news.cnblogs.com/n/714645/)
· [苹果可折叠iPad/MacBook二合一曝光：20英寸触摸屏](https://news.cnblogs.com/n/714644/)
» [更多新闻...](https://news.cnblogs.com/)

MENU