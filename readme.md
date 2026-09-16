<br>
<p align="center">
  <img src="./.github/banner.svg" height="150px" alt="Design Patterns for Humans banner" />
</p>

---

<p align="center">
🎉 把设计模式讲到最简单！ 🎉
</p>
<p align="center">
这个话题很容易让人头晕。在这里，我尽量用 <i>最简单</i> 的方式讲解它们，让它们留在你的<br>脑子里（顺便也留在我脑子里）。
</p>

---

<sub>欢迎看看我的[另一个项目](http://roadmap.sh)，也欢迎来 [Twitter](https://twitter.com/kamrify) 打个招呼。</sub>

<br>

## 目录

- [目录](#目录)
- [简介](#简介)
  - [注意事项](#注意事项)
  - [设计模式的类型](#设计模式的类型)
- [创建型设计模式 (Creational Design Patterns)](#创建型设计模式-creational-design-patterns)
  - [🏠 简单工厂 (Simple Factory)](#-简单工厂-simple-factory)
  - [🏭 工厂方法 (Factory Method)](#-工厂方法-factory-method)
  - [🔨 抽象工厂 (Abstract Factory)](#-抽象工厂-abstract-factory)
  - [👷 建造者 (Builder)](#-建造者-builder)
  - [🐑 原型 (Prototype)](#-原型-prototype)
  - [💍 单例 (Singleton)](#-单例-singleton)
- [结构型设计模式 (Structural Design Patterns)](#结构型设计模式-structural-design-patterns)
  - [🔌 适配器 (Adapter)](#-适配器-adapter)
  - [🚡 桥接 (Bridge)](#-桥接-bridge)
  - [🌿 组合 (Composite)](#-组合-composite)
  - [☕ 装饰器 (Decorator)](#-装饰器-decorator)
  - [📦 外观 (Facade)](#-外观-facade)
  - [🍃 享元 (Flyweight)](#-享元-flyweight)
  - [🎱 代理 (Proxy)](#-代理-proxy)
- [行为型设计模式 (Behavioral Design Patterns)](#行为型设计模式-behavioral-design-patterns)
  - [🔗 责任链 (Chain of Responsibility)](#-责任链-chain-of-responsibility)
  - [👮 命令 (Command)](#-命令-command)
  - [➿ 迭代器 (Iterator)](#-迭代器-iterator)
  - [👽 中介者 (Mediator)](#-中介者-mediator)
  - [💾 备忘录 (Memento)](#-备忘录-memento)
  - [😎 观察者 (Observer)](#-观察者-observer)
  - [🏃 访问者 (Visitor)](#-访问者-visitor)
  - [💡 策略 (Strategy)](#-策略-strategy)
  - [💢 状态 (State)](#-状态-state)
  - [📒 模板方法 (Template Method)](#-模板方法-template-method)
- [🚦 总结](#-总结)
- [👬 参与贡献](#-参与贡献)
- [许可证](#许可证)

<br>

## 简介

设计模式是对反复出现的问题的解法，是**关于如何应对特定问题的指导方针**。它们不是类、软件包或库，不是那种插进应用就能坐等奇迹发生的东西；而是在特定情境下应对特定问题的一组指导方针。

> 设计模式是对反复出现的问题的解法，是关于如何应对特定问题的指导方针

维基百科是这样定义的：

> 在软件工程中，软件设计模式是特定情境下针对常见问题的通用、可复用的解法。它不是能直接变换成源代码或机器码的成品设计，而是对如何解决某类问题的描述或模板，可以在许多不同情境中使用。

### 注意事项

- 设计模式不是解决你所有问题的银弹。
- 不要生搬硬套；强行套用，准没好事。
- 记住：设计模式是「针对问题」的解法，不是「替你找问题」的工具，所以别想太多。
- 用在对的地方、用对方法，它们能救你于水火；用错了地方，代码就可能变成一团乱麻。

> 另外请注意，下文的示例代码用的是 PHP 7，不过这不该成为障碍，概念本身是相通的。

### 设计模式的类型

- [创建型](#创建型设计模式-creational-design-patterns)
- [结构型](#结构型设计模式-structural-design-patterns)
- [行为型](#行为型设计模式-behavioral-design-patterns)

## 创建型设计模式 (Creational Design Patterns)

**通俗解释**

> 创建型模式关注的是如何实例化一个对象，或者一组相关的对象。

**维基百科说**

> 在软件工程中，创建型设计模式处理对象的创建机制，试图以适合当前情境的方式创建对象。最基本的对象创建方式可能带来设计问题，或者给设计增加复杂度；创建型模式通过某种方式控制对象的创建来解决这个问题。

### 🏠 简单工厂 (Simple Factory)

**现实世界例子**

> 假设你在盖房子，需要门。你可以换上木匠服，搬来木头、胶水、钉子和全套工具，在自己家里动手做门；也可以直接打电话给工厂，让做好的门送上门——你既不用学做门的手艺，也不用收拾做门的一地狼藉。

**通俗解释**

> 简单工厂为客户端生成一个实例，但不向客户端暴露任何实例化逻辑。

**维基百科说**

> 在面向对象编程（OOP）中，工厂是用于创建其他对象的对象。正式地说，工厂是一个函数或方法，从某次方法调用中返回不同原型或类的对象，而这些对象通常被认为是用 `new` 创建出来的。

**示例代码**

首先是一个门的接口和它的实现

```php
interface Door
{
    public function getWidth(): float;
    public function getHeight(): float;
}

class WoodenDoor implements Door
{
    protected $width;
    protected $height;

    public function __construct(float $width, float $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getWidth(): float
    {
        return $this->width;
    }

    public function getHeight(): float
    {
        return $this->height;
    }
}
```

然后是门的工厂，负责制作并返回门

```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new WoodenDoor($width, $height);
    }
}
```

用起来是这样

```php
// Make me a door of 100x200
$door = DoorFactory::makeDoor(100, 200);

echo 'Width: ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();

// Make me a door of 50x100
$door2 = DoorFactory::makeDoor(50, 100);
```

**何时使用？**

当创建一个对象不只是几次赋值、还涉及一些逻辑时，把它放进专门的工厂里更合理，而不是把同样的代码到处复制。

### 🏭 工厂方法 (Factory Method)

**现实世界例子**

> 想想招聘经理的情况。一个人不可能把所有岗位的面试都面完，她得根据职位的不同，把面试环节分派给不同的人。

**通俗解释**

> 它提供了一种把实例化逻辑交给子类的办法。

**维基百科说**

> 在基于类的编程中，工厂方法模式是一种创建型模式，它借助工厂方法来解决「创建对象时无须指定对象具体类」的问题。做法是：不直接调用构造函数，而是调用工厂方法来创建对象——工厂方法或者在接口中声明、由子类实现，或者在基类中实现、由派生类按需覆盖。

**示例代码**

接着用上面招聘经理的例子。先是一个面试官接口，以及它的几个实现

```php
interface Interviewer
{
    public function askQuestions();
}

class Developer implements Interviewer
{
    public function askQuestions()
    {
        echo 'Asking about design patterns!';
    }
}

class CommunityExecutive implements Interviewer
{
    public function askQuestions()
    {
        echo 'Asking about community building';
    }
}
```

然后创建 `HiringManager`

```php
abstract class HiringManager
{

    // Factory method
    abstract protected function makeInterviewer(): Interviewer;

    public function takeInterview()
    {
        $interviewer = $this->makeInterviewer();
        $interviewer->askQuestions();
    }
}

```

任何子类都可以继承它，并提供自己需要的面试官

```php
class DevelopmentManager extends HiringManager
{
    protected function makeInterviewer(): Interviewer
    {
        return new Developer();
    }
}

class MarketingManager extends HiringManager
{
    protected function makeInterviewer(): Interviewer
    {
        return new CommunityExecutive();
    }
}
```

用起来是这样

```php
$devManager = new DevelopmentManager();
$devManager->takeInterview(); // Output: Asking about design patterns

$marketingManager = new MarketingManager();
$marketingManager->takeInterview(); // Output: Asking about community building.
```

**何时使用？**

当一个类里有通用的处理流程，但具体需要哪个子类要到运行时才能确定时，工厂方法就派上用场。换句话说：客户端不知道自己需要的具体子类是什么时，用它。

### 🔨 抽象工厂 (Abstract Factory)

**现实世界例子**

> 接着简单工厂里门的例子往下说。根据需要，你可能从木门店买木门，从铁艺店买铁门，从相应的店买 PVC 门。此外，装不同材质的门还需要不同专长的师傅：木门找木匠，铁门找焊工，等等。可以看到，门和安装师傅之间产生了依赖：木门配木匠，铁门配焊工。

**通俗解释**

> 工厂的工厂；把一组各自独立但相互关联/依赖的工厂组合在一起，却不指明它们的具体类。

**维基百科说**

> 抽象工厂模式提供了一种方式，把一组有共同主题的独立工厂封装起来，而无须指明它们的具体类。

**示例代码**

把上面门的例子写成代码。先是 `Door` 接口和它的两个实现

```php
interface Door
{
    public function getDescription();
}

class WoodenDoor implements Door
{
    public function getDescription()
    {
        echo 'I am a wooden door';
    }
}

class IronDoor implements Door
{
    public function getDescription()
    {
        echo 'I am an iron door';
    }
}
```

然后是每种门对应的安装师傅

```php
interface DoorFittingExpert
{
    public function getDescription();
}

class Welder implements DoorFittingExpert
{
    public function getDescription()
    {
        echo 'I can only fit iron doors';
    }
}

class Carpenter implements DoorFittingExpert
{
    public function getDescription()
    {
        echo 'I can only fit wooden doors';
    }
}
```

现在有了抽象工厂，它让我们能制造一族相关的对象：木门工厂生产木门和木门安装师傅，铁门工厂生产铁门和铁门安装师傅

```php
interface DoorFactory
{
    public function makeDoor(): Door;
    public function makeFittingExpert(): DoorFittingExpert;
}

// Wooden factory to return carpenter and wooden door
class WoodenDoorFactory implements DoorFactory
{
    public function makeDoor(): Door
    {
        return new WoodenDoor();
    }

    public function makeFittingExpert(): DoorFittingExpert
    {
        return new Carpenter();
    }
}

// Iron door factory to get iron door and the relevant fitting expert
class IronDoorFactory implements DoorFactory
{
    public function makeDoor(): Door
    {
        return new IronDoor();
    }

    public function makeFittingExpert(): DoorFittingExpert
    {
        return new Welder();
    }
}
```

用起来是这样

```php
$woodenFactory = new WoodenDoorFactory();

$door = $woodenFactory->makeDoor();
$expert = $woodenFactory->makeFittingExpert();

$door->getDescription();  // Output: I am a wooden door
$expert->getDescription(); // Output: I can only fit wooden doors

// Same for Iron Factory
$ironFactory = new IronDoorFactory();

$door = $ironFactory->makeDoor();
$expert = $ironFactory->makeFittingExpert();

$door->getDescription();  // Output: I am an iron door
$expert->getDescription(); // Output: I can only fit iron doors
```

可以看到，木门工厂把 `carpenter` 和 `wooden door` 封装在了一起，铁门工厂把 `iron door` 和 `welder` 封装在了一起。这就保证了每扇门配到的安装师傅都不会错。

**何时使用？**

当存在相互关联的依赖，并且创建逻辑不那么简单时。

### 👷 建造者 (Builder)

**现实世界例子**

> 想象你在 Hardee's 点了一份套餐，比如「Big Hardee」，店员二话不说直接递给你——这就是简单工厂。但有些情况，创建逻辑包含更多步骤。比如你想在 Subway 定制一份套餐，汉堡怎么做有很多选项：要什么面包？加哪些酱？要什么奶酪？……这时就该建造者模式出场了。

**通俗解释**

> 让你创建一个对象的各种不同「口味」，同时避免构造函数膨胀。适用于一个对象可能有多种形态，或者创建过程包含很多步骤的场景。

**维基百科说**

> 建造者模式是一种对象创建软件设计模式，目的是解决 telescoping constructor（层层叠加的构造函数）反模式。

说到这里，补充一下什么是 telescoping constructor 反模式。我们都见过下面这样的构造函数：

```php
public function __construct($size, $cheese = true, $pepperoni = true, $tomato = false, $lettuce = true)
{
}
```

可以看到，构造函数参数的个数很容易失控，参数的排列也变得难以理解。而且将来想加更多选项时，这个参数列表还会继续膨胀。这就叫 telescoping constructor 反模式。

**示例代码**

正经的替代方案是建造者模式。首先是我们想要制作的汉堡

```php
class Burger
{
    protected $size;

    protected $cheese = false;
    protected $pepperoni = false;
    protected $lettuce = false;
    protected $tomato = false;

    public function __construct(BurgerBuilder $builder)
    {
        $this->size = $builder->size;
        $this->cheese = $builder->cheese;
        $this->pepperoni = $builder->pepperoni;
        $this->lettuce = $builder->lettuce;
        $this->tomato = $builder->tomato;
    }
}
```

然后是建造者

```php
class BurgerBuilder
{
    public $size;

    public $cheese = false;
    public $pepperoni = false;
    public $lettuce = false;
    public $tomato = false;

    public function __construct(int $size)
    {
        $this->size = $size;
    }

    public function addPepperoni()
    {
        $this->pepperoni = true;
        return $this;
    }

    public function addLettuce()
    {
        $this->lettuce = true;
        return $this;
    }

    public function addCheese()
    {
        $this->cheese = true;
        return $this;
    }

    public function addTomato()
    {
        $this->tomato = true;
        return $this;
    }

    public function build(): Burger
    {
        return new Burger($this);
    }
}
```

用起来是这样：

```php
$burger = (new BurgerBuilder(14))
                    ->addPepperoni()
                    ->addLettuce()
                    ->addTomato()
                    ->build();
```

**何时使用？**

当一个对象可能有多种形态、又想避免构造函数层层叠加时使用。它与工厂模式的关键区别在于：创建过程一步到位的，用工厂模式；创建过程分多步的，用建造者模式。

### 🐑 原型 (Prototype)

**现实世界例子**

> 还记得多利吗？那只被克隆出来的羊！细节就不展开了，关键点在于：这一切的核心是克隆。

**通俗解释**

> 基于已有对象，通过克隆来创建新对象。

**维基百科说**

> 原型模式是软件开发中的一种创建型设计模式。当要创建的对象类型由一个原型实例决定时，就使用该模式：克隆这个原型来产生新对象。

简而言之，它让你复制一个现有对象，再按需修改，省去从零创建并配置一个对象的麻烦。

**示例代码**

在 PHP 里，用 `clone` 就能轻松做到

```php
class Sheep
{
    protected $name;
    protected $category;

    public function __construct(string $name, string $category = 'Mountain Sheep')
    {
        $this->name = $name;
        $this->category = $category;
    }

    public function setName(string $name)
    {
        $this->name = $name;
    }

    public function getName()
    {
        return $this->name;
    }

    public function setCategory(string $category)
    {
        $this->category = $category;
    }

    public function getCategory()
    {
        return $this->category;
    }
}
```

然后就可以像下面这样克隆

```php
$original = new Sheep('Jolly');
echo $original->getName(); // Jolly
echo $original->getCategory(); // Mountain Sheep

// Clone and modify what is required
$cloned = clone $original;
$cloned->setName('Dolly');
echo $cloned->getName(); // Dolly
echo $cloned->getCategory(); // Mountain sheep
```

另外，还可以用魔术方法 `__clone` 来定制克隆行为。

**何时使用？**

当需要一个与现有对象相似的对象，或者从头创建的开销比克隆大时。

### 💍 单例 (Singleton)

**现实世界例子**

> 一个国家同一时间只能有一位总统。无论何时需要，都得是同一位总统出面。这里的总统就是单例。

**通俗解释**

> 确保某个类只创建一个对象。

**维基百科说**

> 在软件工程中，单例模式是一种把类的实例化限制在单个对象上的软件设计模式。当整个系统恰好只需要一个对象来协调各项动作时，它就派上用场。

单例模式实际上已被视为一种反模式，应当避免过度使用。它不一定是坏东西，也有一些合理用例，但使用时要小心：它会往应用里引入全局状态，在一处的改动可能影响到其他地方，调试起来会相当费劲。另一个坏处是它让代码紧耦合，而且 mock 一个单例可能很困难。

**示例代码**

创建单例的做法是：把构造函数设为私有，禁止克隆，禁止继承，再用一个静态变量存放实例

```php
final class President
{
    private static $instance;

    private function __construct()
    {
        // Hide the constructor
    }

    public static function getInstance(): President
    {
        if (!self::$instance) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    private function __clone()
    {
        // Disable cloning
    }

    private function __wakeup()
    {
        // Disable unserialize
    }
}
```

使用时

```php
$president1 = President::getInstance();
$president2 = President::getInstance();

var_dump($president1 === $president2); // true
```

## 结构型设计模式 (Structural Design Patterns)

**通俗解释**

> 结构型模式主要关注对象的组合，换句话说，各个实体之间如何相互使用。换一种说法：它们帮助回答「如何搭建一个软件组件？」

**维基百科说**

> 在软件工程中，结构型设计模式通过找出实体之间建立关系的简单办法来简化设计。

### 🔌 适配器 (Adapter)

**现实世界例子**

> 假设你的存储卡里有一些照片，要传到电脑上。传照片需要某种与电脑端口兼容的适配器，才能把存储卡接到电脑上——这里读卡器就是适配器。
> 另一个例子是有名的电源适配器：三脚插头插不进两孔插座，得用一个电源适配器让它兼容两孔插座。
> 还有一个例子：把一个人的话翻译给另一个人听的翻译。

**通俗解释**

> 适配器模式让你把一个本来不兼容的对象包进适配器，使它与另一个类兼容。

**维基百科说**

> 在软件工程中，适配器模式让现有类的接口可以被当作另一个接口来用。它常用于让现有类与其他类协作，而不修改其源代码。

**示例代码**

设想一个游戏，里面有一位猎狮子的猎人。

先是一个 `Lion` 接口，所有种类的狮子都要实现它

```php
interface Lion
{
    public function roar();
}

class AfricanLion implements Lion
{
    public function roar()
    {
    }
}

class AsianLion implements Lion
{
    public function roar()
    {
    }
}
```

猎人打猎时，接受任何 `Lion` 接口的实现。

```php
class Hunter
{
    public function hunt(Lion $lion)
    {
        $lion->roar();
    }
}
```

现在假设游戏要加入一只 `WildDog`，让猎人也能猎它。但不能直接加，因为狗的接口不同。为了让猎人能用它，得造一个兼容的适配器

```php
// This needs to be added to the game
class WildDog
{
    public function bark()
    {
    }
}

// Adapter around wild dog to make it compatible with our game
class WildDogAdapter implements Lion
{
    protected $dog;

    public function __construct(WildDog $dog)
    {
        $this->dog = $dog;
    }

    public function roar()
    {
        $this->dog->bark();
    }
}
```

现在，`WildDog` 可以借助 `WildDogAdapter` 出现在游戏里了。

```php
$wildDog = new WildDog();
$wildDogAdapter = new WildDogAdapter($wildDog);

$hunter = new Hunter();
$hunter->hunt($wildDogAdapter);
```

### 🚡 桥接 (Bridge)

**现实世界例子**

> 假设你有一个多页面的网站，要允许用户切换主题。你会怎么做？为每个主题把每个页面都复制出一份，还是把主题独立出来、按用户偏好加载？桥接模式让你做到后者，也就是：

![使用与不使用桥接模式的对比](https://cloud.githubusercontent.com/assets/11269635/23065293/33b7aea0-f515-11e6-983f-98823c9845ee.png)

**通俗解释**

> 桥接模式讲究的是优先使用组合而不是继承。把实现细节从一层继承体系中抽出来，推进另一个拥有独立继承体系的对象里。

**维基百科说**

> 桥接模式是软件工程中的一种设计模式，意在「把抽象与实现解耦，使二者可以独立变化」。

**示例代码**

把上面的网页例子写成代码。这里是 `WebPage` 这一层

```php
interface WebPage
{
    public function __construct(Theme $theme);
    public function getContent();
}

class About implements WebPage
{
    protected $theme;

    public function __construct(Theme $theme)
    {
        $this->theme = $theme;
    }

    public function getContent()
    {
        return "About page in " . $this->theme->getColor();
    }
}

class Careers implements WebPage
{
    protected $theme;

    public function __construct(Theme $theme)
    {
        $this->theme = $theme;
    }

    public function getContent()
    {
        return "Careers page in " . $this->theme->getColor();
    }
}
```

另一边是独立的主题体系

```php

interface Theme
{
    public function getColor();
}

class DarkTheme implements Theme
{
    public function getColor()
    {
        return 'Dark Black';
    }
}
class LightTheme implements Theme
{
    public function getColor()
    {
        return 'Off white';
    }
}
class AquaTheme implements Theme
{
    public function getColor()
    {
        return 'Light blue';
    }
}
```

两边合起来用

```php
$darkTheme = new DarkTheme();

$about = new About($darkTheme);
$careers = new Careers($darkTheme);

echo $about->getContent(); // "About page in Dark Black";
echo $careers->getContent(); // "Careers page in Dark Black";
```

### 🌿 组合 (Composite)

**现实世界例子**

> 每个组织都由员工组成。员工们有着共同的特征：有工资，有职责，可能向某人汇报，也可能有下属，等等。

**通俗解释**

> 组合模式让客户端以统一的方式对待单个对象。

**维基百科说**

> 在软件工程中，组合模式是一种分区设计模式。它描述的是：一组对象应当与单个对象实例以同样的方式对待。组合的意图是把对象「组合」成树形结构，以表示部分—整体的层级关系。实现组合模式能让客户端统一地对待单个对象和对象组合。

**示例代码**

用上面的员工例子。这里有几种员工类型

```php
interface Employee
{
    public function __construct(string $name, float $salary);
    public function getName(): string;
    public function setSalary(float $salary);
    public function getSalary(): float;
    public function getRoles(): array;
}

class Developer implements Employee
{
    protected $salary;
    protected $name;
    protected $roles;

    public function __construct(string $name, float $salary)
    {
        $this->name = $name;
        $this->salary = $salary;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function setSalary(float $salary)
    {
        $this->salary = $salary;
    }

    public function getSalary(): float
    {
        return $this->salary;
    }

    public function getRoles(): array
    {
        return $this->roles;
    }
}

class Designer implements Employee
{
    protected $salary;
    protected $name;
    protected $roles;

    public function __construct(string $name, float $salary)
    {
        $this->name = $name;
        $this->salary = $salary;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function setSalary(float $salary)
    {
        $this->salary = $salary;
    }

    public function getSalary(): float
    {
        return $this->salary;
    }

    public function getRoles(): array
    {
        return $this->roles;
    }
}
```

然后是一个由多种员工组成的组织

```php
class Organization
{
    protected $employees;

    public function addEmployee(Employee $employee)
    {
        $this->employees[] = $employee;
    }

    public function getNetSalaries(): float
    {
        $netSalary = 0;

        foreach ($this->employees as $employee) {
            $netSalary += $employee->getSalary();
        }

        return $netSalary;
    }
}
```

用起来是这样

```php
// Prepare the employees
$john = new Developer('John Doe', 12000);
$jane = new Designer('Jane Doe', 15000);

// Add them to organization
$organization = new Organization();
$organization->addEmployee($john);
$organization->addEmployee($jane);

echo "Net salaries: " . $organization->getNetSalaries(); // Net Salaries: 27000
```

### ☕ 装饰器 (Decorator)

**现实世界例子**

> 想象你开一家汽车服务店，提供多种服务。账单怎么算？先选一项服务，然后动态地把各项服务的价格累加上去，直到得出最终费用。这里每种服务都是一个装饰器。

**通俗解释**

> 装饰器模式让你在运行时把对象包进装饰器类的对象，从而动态改变它的行为。

**维基百科说**

> 在面向对象编程中，装饰器模式允许向单个对象静态或动态地添加行为，且不影响同类的其他对象。装饰器模式也常有助于遵守单一职责原则，因为它让功能分散到各司其职的类中。

**示例代码**

拿咖啡举例。先是一个实现咖啡接口的简单咖啡

```php
interface Coffee
{
    public function getCost();
    public function getDescription();
}

class SimpleCoffee implements Coffee
{
    public function getCost()
    {
        return 10;
    }

    public function getDescription()
    {
        return 'Simple coffee';
    }
}
```

我们希望代码可扩展，能在需要时加选项。来做几个加料（装饰器）

```php
class MilkCoffee implements Coffee
{
    protected $coffee;

    public function __construct(Coffee $coffee)
    {
        $this->coffee = $coffee;
    }

    public function getCost()
    {
        return $this->coffee->getCost() + 2;
    }

    public function getDescription()
    {
        return $this->coffee->getDescription() . ', milk';
    }
}

class WhipCoffee implements Coffee
{
    protected $coffee;

    public function __construct(Coffee $coffee)
    {
        $this->coffee = $coffee;
    }

    public function getCost()
    {
        return $this->coffee->getCost() + 5;
    }

    public function getDescription()
    {
        return $this->coffee->getDescription() . ', whip';
    }
}

class VanillaCoffee implements Coffee
{
    protected $coffee;

    public function __construct(Coffee $coffee)
    {
        $this->coffee = $coffee;
    }

    public function getCost()
    {
        return $this->coffee->getCost() + 3;
    }

    public function getDescription()
    {
        return $this->coffee->getDescription() . ', vanilla';
    }
}
```

现在来点一杯咖啡

```php
$someCoffee = new SimpleCoffee();
echo $someCoffee->getCost(); // 10
echo $someCoffee->getDescription(); // Simple Coffee

$someCoffee = new MilkCoffee($someCoffee);
echo $someCoffee->getCost(); // 12
echo $someCoffee->getDescription(); // Simple Coffee, milk

$someCoffee = new WhipCoffee($someCoffee);
echo $someCoffee->getCost(); // 17
echo $someCoffee->getDescription(); // Simple Coffee, milk, whip

$someCoffee = new VanillaCoffee($someCoffee);
echo $someCoffee->getCost(); // 20
echo $someCoffee->getDescription(); // Simple Coffee, milk, whip, vanilla
```

### 📦 外观 (Facade)

**现实世界例子**

> 你怎么打开电脑？「按电源键」！你敢这么肯定，是因为你用的是电脑对外提供的简单接口；内部为了完成这件事，其实要做一大堆工作。这种包住复杂子系统的简单接口，就是外观。

**通俗解释**

> 外观模式为复杂子系统提供一个简化接口。

**维基百科说**

> 外观是为庞大的代码体（比如类库）提供简化接口的对象。

**示例代码**

用上面的电脑例子。这里是 Computer 类

```php
class Computer
{
    public function getElectricShock()
    {
        echo "Ouch!";
    }

    public function makeSound()
    {
        echo "Beep beep!";
    }

    public function showLoadingScreen()
    {
        echo "Loading..";
    }

    public function bam()
    {
        echo "Ready to be used!";
    }

    public function closeEverything()
    {
        echo "Bup bup bup buzzzz!";
    }

    public function sooth()
    {
        echo "Zzzzz";
    }

    public function pullCurrent()
    {
        echo "Haaah!";
    }
}
```

这是外观

```php
class ComputerFacade
{
    protected $computer;

    public function __construct(Computer $computer)
    {
        $this->computer = $computer;
    }

    public function turnOn()
    {
        $this->computer->getElectricShock();
        $this->computer->makeSound();
        $this->computer->showLoadingScreen();
        $this->computer->bam();
    }

    public function turnOff()
    {
        $this->computer->closeEverything();
        $this->computer->pullCurrent();
        $this->computer->sooth();
    }
}
```

使用外观

```php
$computer = new ComputerFacade(new Computer());
$computer->turnOn(); // Ouch! Beep beep! Loading.. Ready to be used!
$computer->turnOff(); // Bup bup buzzz! Haah! Zzzzz
```

### 🍃 享元 (Flyweight)

**现实世界例子**

> 你在茶摊买过现沏的茶吗？摊主常常一次沏好不止你要的那一杯，剩下的留给下一位顾客，为的是省资源，比如煤气。享元模式讲的就是这件事：共享。

**通俗解释**

> 通过与相似对象尽可能多地共享，来降低内存占用或计算开销。

**维基百科说**

> 在计算机编程中，享元是一种软件设计模式。享元对象通过与其他相似对象尽可能共享数据来减少内存使用；当简单重复的对象表示会占用不可接受的内存量时，可以用这种方式来大量使用对象。

**示例代码**

把上面买茶的例子写成代码。先是茶叶种类和沏茶器

```php
// Anything that will be cached is flyweight.
// Types of tea here will be flyweights.
class KarakTea
{
}

// Acts as a factory and saves the tea
class TeaMaker
{
    protected $availableTea = [];

    public function make($preference)
    {
        if (empty($this->availableTea[$preference])) {
            $this->availableTea[$preference] = new KarakTea();
        }

        return $this->availableTea[$preference];
    }
}
```

然后是接单上茶的 `TeaShop`

```php
class TeaShop
{
    protected $orders;
    protected $teaMaker;

    public function __construct(TeaMaker $teaMaker)
    {
        $this->teaMaker = $teaMaker;
    }

    public function takeOrder(string $teaType, int $table)
    {
        $this->orders[$table] = $this->teaMaker->make($teaType);
    }

    public function serve()
    {
        foreach ($this->orders as $table => $tea) {
            echo "Serving tea to table# " . $table;
        }
    }
}
```

用起来像下面这样

```php
$teaMaker = new TeaMaker();
$shop = new TeaShop($teaMaker);

$shop->takeOrder('less sugar', 1);
$shop->takeOrder('more milk', 2);
$shop->takeOrder('without sugar', 5);

$shop->serve();
// Serving tea to table# 1
// Serving tea to table# 2
// Serving tea to table# 5
```

### 🎱 代理 (Proxy)

**现实世界例子**

> 你刷过门禁卡吗？开门的方式不止一种：可以刷卡，也可以按一个绕过安保的按钮。门的主要功能就是开，但在它之上加了一层代理，用来附加一些功能。用下面的代码例子能说得更清楚。

**通俗解释**

> 使用代理模式，一个类代表另一个类的功能。

**维基百科说**

> 代理在最一般的形式下，是充当某种东西的接口的类。代理是包装或代理对象，客户端调用它来访问幕后真正的服务对象。代理可以只是简单转发，也可以提供额外逻辑：比如对真实对象的操作很耗资源时加缓存，或在调用真实对象前检查前置条件。

**示例代码**

用上面的安保门例子。先是门接口和一种门的实现

```php
interface Door
{
    public function open();
    public function close();
}

class LabDoor implements Door
{
    public function open()
    {
        echo "Opening lab door";
    }

    public function close()
    {
        echo "Closing the lab door";
    }
}
```

然后是给任意门加上安保的代理

```php
class SecuredDoor implements Door
{
    protected $door;

    public function __construct(Door $door)
    {
        $this->door = $door;
    }

    public function open($password)
    {
        if ($this->authenticate($password)) {
            $this->door->open();
        } else {
            echo "Big no! It ain't possible.";
        }
    }

    public function authenticate($password)
    {
        return $password === '$ecr@t';
    }

    public function close()
    {
        $this->door->close();
    }
}
```

用法如下

```php
$door = new SecuredDoor(new LabDoor());
$door->open('invalid'); // Big no! It ain't possible.

$door->open('$ecr@t'); // Opening lab door
$door->close(); // Closing lab door
```

另一个例子是某种数据映射器的实现。比如我最近用这个模式给 MongoDB 写了一个 ODM（对象数据映射器）：借助魔术方法 `__call()`，在 mongo 类外面套了一层代理。所有方法调用都被转发给原始的 mongo 类，取回的结果原样返回；但调用 `find` 或 `findOne` 时，数据会被映射成目标类的对象，返回的是对象而不是 `Cursor`。

## 行为型设计模式 (Behavioral Design Patterns)

**通俗解释**

> 它关心对象之间职责的分配。它与结构型模式的区别在于：不只规定结构，还规定了对象之间消息传递/沟通的方式。换句话说，它们帮助回答「如何在软件组件中运行一个行为？」

**维基百科说**

> 在软件工程中，行为型设计模式找出对象之间常见的沟通模式并加以实现。这样做之后，这些模式提高了执行这种沟通的灵活性。

### 🔗 责任链 (Chain of Responsibility)

**现实世界例子**

> 比如你的账户里设置了三种支付方式（`A`、`B` 和 `C`），余额各不相同：`A` 有 100 美元，`B` 有 300 美元，`C` 有 1000 美元，支付优先级是 `A`、`B`、`C`。你要买 210 美元的东西。用责任链模式，先检查账户 `A` 能不能支付：能，就付款，链条到此为止；不能，请求就传给账户 `B` 检查余额，能就截断链条，不能就继续往后传，直到找到能处理请求的对象为止。这里的 `A`、`B`、`C` 就是链条上的环，整个机制就是责任链。

**通俗解释**

> 它帮你把对象连成一条链。请求从一端进入，逐个对象传递，直到找到能处理的那个。

**维基百科说**

> 在面向对象设计中，责任链模式由命令对象的来源和一系列处理对象组成。每个处理对象包含定义自己能处理哪些命令对象的逻辑，其余的命令传给链条上的下一个处理对象。

**示例代码**

把上面的账户例子写成代码。先是把账户串成链的基类，以及几种账户

```php
abstract class Account
{
    protected $successor;
    protected $balance;

    public function setNext(Account $account)
    {
        $this->successor = $account;
    }

    public function pay(float $amountToPay)
    {
        if ($this->canPay($amountToPay)) {
            echo sprintf('Paid %s using %s' . PHP_EOL, $amountToPay, get_called_class());
        } elseif ($this->successor) {
            echo sprintf('Cannot pay using %s. Proceeding ..' . PHP_EOL, get_called_class());
            $this->successor->pay($amountToPay);
        } else {
            throw new Exception('None of the accounts have enough balance');
        }
    }

    public function canPay($amount): bool
    {
        return $this->balance >= $amount;
    }
}

class Bank extends Account
{
    protected $balance;

    public function __construct(float $balance)
    {
        $this->balance = $balance;
    }
}

class Paypal extends Account
{
    protected $balance;

    public function __construct(float $balance)
    {
        $this->balance = $balance;
    }
}

class Bitcoin extends Account
{
    protected $balance;

    public function __construct(float $balance)
    {
        $this->balance = $balance;
    }
}
```

现在用上面定义的环节（Bank、Paypal、Bitcoin）准备这条链

```php
// Let's prepare a chain like below
//      $bank->$paypal->$bitcoin
//
// First priority bank
//      If bank can't pay then paypal
//      If paypal can't pay then bit coin

$bank = new Bank(100);          // Bank with balance 100
$paypal = new Paypal(200);      // Paypal with balance 200
$bitcoin = new Bitcoin(300);    // Bitcoin with balance 300

$bank->setNext($paypal);
$paypal->setNext($bitcoin);

// Let's try to pay using the first priority i.e. bank
$bank->pay(259);

// Output will be
// ==============
// Cannot pay using bank. Proceeding ..
// Cannot pay using paypal. Proceeding ..:
// Paid 259 using Bitcoin!
```

### 👮 命令 (Command)

**现实世界例子**

> 一个通用例子是你在餐厅点餐。你（`Client`）请服务员（`Invoker`）上菜（`Command`），服务员把请求转给厨师（`Receiver`），他知道做什么菜、怎么做。
> 另一个例子：你（`Client`）用遥控器（`Invoker`）打开（`Command`）电视（`Receiver`）。

**通俗解释**

> 它让你把动作封装进对象。这个模式的核心思想，是提供一种把客户端与接收者解耦的手段。

**维基百科说**

> 在面向对象编程中，命令模式是一种行为型设计模式：用一个对象来封装执行动作或触发事件所需的全部信息，以便日后执行。这些信息包括方法名、方法所属的对象，以及方法参数的值。

**示例代码**

先是接收者，它实现了所有可以执行的动作

```php
// Receiver
class Bulb
{
    public function turnOn()
    {
        echo "Bulb has been lit";
    }

    public function turnOff()
    {
        echo "Darkness!";
    }
}
```

然后是每个命令都要实现的接口，接着是一组命令

```php
interface Command
{
    public function execute();
    public function undo();
    public function redo();
}

// Command
class TurnOn implements Command
{
    protected $bulb;

    public function __construct(Bulb $bulb)
    {
        $this->bulb = $bulb;
    }

    public function execute()
    {
        $this->bulb->turnOn();
    }

    public function undo()
    {
        $this->bulb->turnOff();
    }

    public function redo()
    {
        $this->execute();
    }
}

class TurnOff implements Command
{
    protected $bulb;

    public function __construct(Bulb $bulb)
    {
        $this->bulb = $bulb;
    }

    public function execute()
    {
        $this->bulb->turnOff();
    }

    public function undo()
    {
        $this->bulb->turnOn();
    }

    public function redo()
    {
        $this->execute();
    }
}
```

然后是 `Invoker`，客户端通过它来提交命令

```php
// Invoker
class RemoteControl
{
    public function submit(Command $command)
    {
        $command->execute();
    }
}
```

最后看客户端里怎么用

```php
$bulb = new Bulb();

$turnOn = new TurnOn($bulb);
$turnOff = new TurnOff($bulb);

$remote = new RemoteControl();
$remote->submit($turnOn); // Bulb has been lit!
$remote->submit($turnOff); // Darkness!
```

命令模式还能用来实现基于事务的系统：执行每条命令的同时记录历史；如果最后一条命令执行成功，万事大吉；否则就回溯历史，对所有已执行的命令逐一执行 `undo`。

### ➿ 迭代器 (Iterator)

**现实世界例子**

> 一台老式收音机就是迭代器的好例子：用户从某个频道开始，用「下一个/上一个」按钮逐个切换频道。MP3 播放器或电视机也一样：按下下一个/上一个按钮，切换曲目或频道。换句话说，它们都提供了一个接口，用来遍历各自的频道、歌曲或电台。

**通俗解释**

> 它提供一种访问对象元素的办法，同时不暴露内部表示。

**维基百科说**

> 在面向对象编程中，迭代器模式用迭代器遍历容器并访问容器的元素。迭代器模式把算法与容器解耦；某些情况下，算法必然依赖容器，无法解耦。

**示例代码**

在 PHP 里，用 SPL（标准 PHP 库）实现起来相当容易。把上面的电台例子写成代码。先是 `RadioStation`

```php
class RadioStation
{
    protected $frequency;

    public function __construct(float $frequency)
    {
        $this->frequency = $frequency;
    }

    public function getFrequency(): float
    {
        return $this->frequency;
    }
}
```

然后是迭代器

```php
use Countable;
use Iterator;

class StationList implements Countable, Iterator
{
    /** @var RadioStation[] $stations */
    protected $stations = [];

    /** @var int $counter */
    protected $counter;

    public function addStation(RadioStation $station)
    {
        $this->stations[] = $station;
    }

    public function removeStation(RadioStation $toRemove)
    {
        $toRemoveFrequency = $toRemove->getFrequency();
        $this->stations = array_filter($this->stations, function (RadioStation $station) use ($toRemoveFrequency) {
            return $station->getFrequency() !== $toRemoveFrequency;
        });
    }

    public function count(): int
    {
        return count($this->stations);
    }

    public function current(): RadioStation
    {
        return $this->stations[$this->counter];
    }

    public function key()
    {
        return $this->counter;
    }

    public function next()
    {
        $this->counter++;
    }

    public function rewind()
    {
        $this->counter = 0;
    }

    public function valid(): bool
    {
        return isset($this->stations[$this->counter]);
    }
}
```

用起来是这样

```php
$stationList = new StationList();

$stationList->addStation(new RadioStation(89));
$stationList->addStation(new RadioStation(101));
$stationList->addStation(new RadioStation(102));
$stationList->addStation(new RadioStation(103.2));

foreach($stationList as $station) {
    echo $station->getFrequency() . PHP_EOL;
}

$stationList->removeStation(new RadioStation(89)); // Will remove station 89
```

### 👽 中介者 (Mediator)

**现实世界例子**

> 一个常见的例子：你用手机和某人通话时，运营商坐在你们中间，对话经由它传达，而不是直接送到对方。这里运营商就是中介者。

**通俗解释**

> 中介者模式引入一个第三方对象（称为中介者），来控制两个对象（称为同事）之间的交互。它有助于降低通信类之间的耦合，因为它们不再需要了解彼此的实现。

**维基百科说**

> 在软件工程中，中介者模式定义一个对象，封装一组对象如何交互。由于它能改变程序的运行行为，这个模式被归为行为型模式。

**示例代码**

下面是最简单的聊天室（中介者）例子，用户（同事）相互发消息。

先是中介者，也就是聊天室

```php
interface ChatRoomMediator
{
    public function showMessage(User $user, string $message);
}

// Mediator
class ChatRoom implements ChatRoomMediator
{
    public function showMessage(User $user, string $message)
    {
        $time = date('M d, y H:i');
        $sender = $user->getName();

        echo $time . '[' . $sender . ']:' . $message;
    }
}
```

然后是用户，也就是同事

```php
class User {
    protected $name;
    protected $chatMediator;

    public function __construct(string $name, ChatRoomMediator $chatMediator) {
        $this->name = $name;
        $this->chatMediator = $chatMediator;
    }

    public function getName() {
        return $this->name;
    }

    public function send($message) {
        $this->chatMediator->showMessage($this, $message);
    }
}
```

用法

```php
$mediator = new ChatRoom();

$john = new User('John Doe', $mediator);
$jane = new User('Jane Doe', $mediator);

$john->send('Hi there!');
$jane->send('Hey!');

// Output will be
// Feb 14, 10:58 [John]: Hi there!
// Feb 14, 10:58 [Jane]: Hey!
```

### 💾 备忘录 (Memento)

**现实世界例子**

> 以计算器（发起人）为例：每次完成计算后，上一次计算会存进内存（备忘录），之后你可以回到它，用某个按键（负责人）把它恢复。

**通俗解释**

> 备忘录模式捕捉并保存对象的当前状态，让日后可以顺利地恢复。

**维基百科说**

> 备忘录模式是一种软件设计模式，提供把对象恢复到先前状态的能力（通过回滚实现撤销）。

通常在你需要提供某种撤销功能时有用。

**示例代码**

以文本编辑器为例：它不时保存状态，你想恢复随时可以恢复。

先是能保存编辑器状态的备忘录对象

```php
class EditorMemento
{
    protected $content;

    public function __construct(string $content)
    {
        $this->content = $content;
    }

    public function getContent()
    {
        return $this->content;
    }
}
```

然后是编辑器，也就是使用备忘录对象的发起人

```php
class Editor
{
    protected $content = '';

    public function type(string $words)
    {
        $this->content = $this->content . ' ' . $words;
    }

    public function getContent()
    {
        return $this->content;
    }

    public function save()
    {
        return new EditorMemento($this->content);
    }

    public function restore(EditorMemento $memento)
    {
        $this->content = $memento->getContent();
    }
}
```

用起来是这样

```php
$editor = new Editor();

// Type some stuff
$editor->type('This is the first sentence.');
$editor->type('This is second.');

// Save the state to restore to : This is the first sentence. This is second.
$saved = $editor->save();

// Type some more
$editor->type('And this is third.');

// Output: Content before Saving
echo $editor->getContent(); // This is the first sentence. This is second. And this is third.

// Restoring to last saved state
$editor->restore($saved);

$editor->getContent(); // This is the first sentence. This is second.
```

### 😎 观察者 (Observer)

**现实世界例子**

> 一个好例子是求职者：订阅某个招聘网站，一有匹配的工作机会就收到通知。

**通俗解释**

> 在对象之间定义依赖：一旦某个对象状态变化，所有依赖它的对象都会收到通知。

**维基百科说**

> 观察者模式是一种软件设计模式：一个被称为主体（subject）的对象维护一份依赖它的对象列表（称为观察者），状态一有变化就自动通知它们，通常是调用它们的某个方法。

**示例代码**

把上面的例子写成代码。先是需要收到职位通知的求职者

```php
class JobPost
{
    protected $title;

    public function __construct(string $title)
    {
        $this->title = $title;
    }

    public function getTitle()
    {
        return $this->title;
    }
}

class JobSeeker implements Observer
{
    protected $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function onJobPosted(JobPost $job)
    {
        // Do something with the job posting
        echo 'Hi ' . $this->name . '! New job posted: '. $job->getTitle();
    }
}
```

然后是求职者会订阅的职位发布

```php
class EmploymentAgency implements Observable
{
    protected $observers = [];

    protected function notify(JobPost $jobPosting)
    {
        foreach ($this->observers as $observer) {
            $observer->onJobPosted($jobPosting);
        }
    }

    public function attach(Observer $observer)
    {
        $this->observers[] = $observer;
    }

    public function addJob(JobPost $jobPosting)
    {
        $this->notify($jobPosting);
    }
}
```

用起来是这样

```php
// Create subscribers
$johnDoe = new JobSeeker('John Doe');
$janeDoe = new JobSeeker('Jane Doe');

// Create publisher and attach subscribers
$jobPostings = new EmploymentAgency();
$jobPostings->attach($johnDoe);
$jobPostings->attach($janeDoe);

// Add a new job and see if subscribers get notified
$jobPostings->addJob(new JobPost('Software Engineer'));

// Output
// Hi John Doe! New job posted: Software Engineer
// Hi Jane Doe! New job posted: Software Engineer
```

### 🏃 访问者 (Visitor)

**现实世界例子**

> 想象某人去迪拜旅游。他只需要一种入境方式（签证），落地后想参观哪里就参观哪里，不必为去某处请求许可，也不必四处跑腿；只要告诉他有个地方，他就能去。访问者模式正是如此：帮你把「可去的地方」加进去，让他不用跑腿就能尽量多逛。

**通俗解释**

> 访问者模式让你不修改对象，就能给对象添加新的操作。

**维基百科说**

> 在面向对象编程和软件工程中，访问者模式把算法与其作用的对象结构分开。这种分离的实际效果，是能在不修改现有对象结构的前提下添加新操作。它是遵循开闭原则的一种方式。

**示例代码**

以动物园模拟为例：园里有各种动物，要让它们发声。用访问者模式来实现

```php
// Visitee
interface Animal
{
    public function accept(AnimalOperation $operation);
}

// Visitor
interface AnimalOperation
{
    public function visitMonkey(Monkey $monkey);
    public function visitLion(Lion $lion);
    public function visitDolphin(Dolphin $dolphin);
}
```

然后是各动物的实现

```php
class Monkey implements Animal
{
    public function shout()
    {
        echo 'Ooh oo aa aa!';
    }

    public function accept(AnimalOperation $operation)
    {
        $operation->visitMonkey($this);
    }
}

class Lion implements Animal
{
    public function roar()
    {
        echo 'Roaaar!';
    }

    public function accept(AnimalOperation $operation)
    {
        $operation->visitLion($this);
    }
}

class Dolphin implements Animal
{
    public function speak()
    {
        echo 'Tuut tuttu tuutt!';
    }

    public function accept(AnimalOperation $operation)
    {
        $operation->visitDolphin($this);
    }
}
```

实现访问者

```php
class Speak implements AnimalOperation
{
    public function visitMonkey(Monkey $monkey)
    {
        $monkey->shout();
    }

    public function visitLion(Lion $lion)
    {
        $lion->roar();
    }

    public function visitDolphin(Dolphin $dolphin)
    {
        $dolphin->speak();
    }
}
```

用起来是这样

```php
$monkey = new Monkey();
$lion = new Lion();
$dolphin = new Dolphin();

$speak = new Speak();

$monkey->accept($speak);    // Ooh oo aa aa!
$lion->accept($speak);      // Roaaar!
$dolphin->accept($speak);   // Tuut tutt tuutt!
```

这个需求本来也可以靠给动物建一套继承体系来解决，但那样的话，每次给动物加新动作都得改动动物类。而现在不用改它们了。比如要求给动物加上「跳」的行为，只需新建一个访问者：

```php
class Jump implements AnimalOperation
{
    public function visitMonkey(Monkey $monkey)
    {
        echo 'Jumped 20 feet high! on to the tree!';
    }

    public function visitLion(Lion $lion)
    {
        echo 'Jumped 7 feet! Back on the ground!';
    }

    public function visitDolphin(Dolphin $dolphin)
    {
        echo 'Walked on water a little and disappeared';
    }
}
```

用法如下

```php
$jump = new Jump();

$monkey->accept($speak);   // Ooh oo aa aa!
$monkey->accept($jump);    // Jumped 20 feet high! on to the tree!

$lion->accept($speak);     // Roaaar!
$lion->accept($jump);      // Jumped 7 feet! Back on the ground!

$dolphin->accept($speak);  // Tuut tutt tuutt!
$dolphin->accept($jump);   // Walked on water a little and disappeared
```

### 💡 策略 (Strategy)

**现实世界例子**

> 以排序为例：我们实现了冒泡排序，但数据量开始增长，冒泡排序变得非常慢。为了应对，我们换了快速排序。可快速排序虽然在大数据集上表现更好，小数据集上却很慢。于是我们定下一个策略：小数据集用冒泡排序，大数据集用快速排序。

**通俗解释**

> 策略模式让你根据情况切换算法或策略。

**维基百科说**

> 在计算机编程中，策略模式（也称 policy 模式）是一种行为型软件设计模式，能在运行时选择算法的行为。

**示例代码**

把上面的例子写成代码。先是策略接口和不同的策略实现

```php
interface SortStrategy
{
    public function sort(array $dataset): array;
}

class BubbleSortStrategy implements SortStrategy
{
    public function sort(array $dataset): array
    {
        echo "Sorting using bubble sort";

        // Do sorting
        return $dataset;
    }
}

class QuickSortStrategy implements SortStrategy
{
    public function sort(array $dataset): array
    {
        echo "Sorting using quick sort";

        // Do sorting
        return $dataset;
    }
}
```

然后是会使用任一策略的客户端

```php
class Sorter
{
    protected $sorterSmall;
    protected $sorterBig;

    public function __construct(SortStrategy $sorterSmall, SortStrategy $sorterBig)
    {
        $this->sorterSmall = $sorterSmall;
        $this->sorterBig = $sorterBig;
    }

    public function sort(array $dataset): array
    {
        if (count($dataset) > 5) {
            return $this->sorterBig->sort($dataset);
        } else {
            return $this->sorterSmall->sort($dataset);
        }
    }
}
```

用起来是这样

```php
$smalldataset = [1, 3, 4, 2];
$bigdataset = [1, 4, 3, 2, 8, 10, 5, 6, 9, 7];

$sorter = new Sorter(new BubbleSortStrategy(), new QuickSortStrategy());

$sorter->sort($dataset); // Output : Sorting using bubble sort

$sorter->sort($bigdataset); // Output : Sorting using quick sort
```

### 💢 状态 (State)

**现实世界例子**

> 想象你在用某个绘图应用，选了画笔开始画画。画笔的行为随所选颜色而变：选了红色就画红色，选了蓝色就画蓝色。

**通俗解释**

> 它让你在状态变化时改变类的行为。

**维基百科说**

> 状态模式是一种行为型软件设计模式，以面向对象的方式实现状态机。使用状态模式时，每个状态实现为状态接口的派生类，状态切换则通过调用模式父类定义的方法来完成。
> 状态模式也可以理解为一种策略模式，只是它能通过调用模式接口定义的方法来切换当前策略。

**示例代码**

以打电话为例。先是状态接口和几个状态实现

```php
interface PhoneState {
    public function pickUp(): PhoneState;
    public function hangUp(): PhoneState;
    public function dial(): PhoneState;
}

// states implementation
class PhoneStateIdle implements PhoneState {
    public function pickUp(): PhoneState {
        return new PhoneStatePickedUp();
    }
    public function hangUp(): PhoneState {
        throw new Exception("already idle");
    }
    public function dial(): PhoneState {
        throw new Exception("unable to dial in idle state");
    }
}

class PhoneStatePickedUp implements PhoneState {
    public function pickUp(): PhoneState {
        throw new Exception("already picked up");
    }
    public function hangUp(): PhoneState {
        return new PhoneStateIdle();
    }
    public function dial(): PhoneState {
        return new PhoneStateCalling();
    }
}

class PhoneStateCalling implements PhoneState {
    public function pickUp(): PhoneState {
        throw new Exception("already picked up");
    }
    public function hangUp(): PhoneState {
        return new PhoneStateIdle();
    }
    public function dial(): PhoneState {
        throw new Exception("already dialing");
    }
}
```

然后是 Phone 类，不同的行为调用会切换状态

```php
class Phone {
    private $state;

    public function __construct() {
        $this->state = new PhoneStateIdle();
    }
    public function pickUp() {
        $this->state = $this->state->pickUp();
    }
    public function hangUp() {
        $this->state = $this->state->hangUp();
    }
    public function dial() {
        $this->state = $this->state->dial();
    }
}
```

用起来像下面这样，相应的状态方法会被调用：

```php
$phone = new Phone();

$phone->pickUp();
$phone->dial();
```

### 📒 模板方法 (Template Method)

**现实世界例子**

> 假设我们要盖一栋房子。施工步骤大概是这样：
>
> - 打地基
> - 砌墙
> - 加屋顶
> - 再加楼层

> 这些步骤的顺序不能变——不砌墙就上屋顶是不可能的——但每一步本身可以调整，比如墙可以用木头、聚酯材料或石头来砌。

**通俗解释**

> 模板方法定义某个算法如何执行的整体骨架，把其中一些步骤的实现推迟到子类。

**维基百科说**

> 在软件工程中，模板方法模式是一种行为型设计模式：在一个操作中定义算法的程序骨架，把某些步骤推迟到子类实现。它让人可以在不改变算法结构的前提下，重新定义算法的某些步骤。

**示例代码**

想象我们有一个构建工具，帮我们测试、静态检查、构建、生成构建报告（代码覆盖率报告、lint 报告等），并把应用部署到测试服务器。

先是规定构建算法骨架的基类

```php
abstract class Builder
{

    // Template method
    final public function build()
    {
        $this->test();
        $this->lint();
        $this->assemble();
        $this->deploy();
    }

    abstract public function test();
    abstract public function lint();
    abstract public function assemble();
    abstract public function deploy();
}
```

然后是各平台的实现

```php
class AndroidBuilder extends Builder
{
    public function test()
    {
        echo 'Running android tests';
    }

    public function lint()
    {
        echo 'Linting the android code';
    }

    public function assemble()
    {
        echo 'Assembling the android build';
    }

    public function deploy()
    {
        echo 'Deploying android build to server';
    }
}

class IosBuilder extends Builder
{
    public function test()
    {
        echo 'Running ios tests';
    }

    public function lint()
    {
        echo 'Linting the ios code';
    }

    public function assemble()
    {
        echo 'Assembling the ios build';
    }

    public function deploy()
    {
        echo 'Deploying ios build to server';
    }
}
```

用起来是这样

```php
$androidBuilder = new AndroidBuilder();
$androidBuilder->build();

// Output:
// Running android tests
// Linting the android code
// Assembling the android build
// Deploying android build to server

$iosBuilder = new IosBuilder();
$iosBuilder->build();

// Output:
// Running ios tests
// Linting the ios code
// Assembling the ios build
// Deploying ios build to server
```

## 🚦 总结

内容就到这里。我会继续完善这个仓库，欢迎 watch/star 以便回访。另外，我计划用同样的方式写一写架构模式，敬请期待。

## 👬 参与贡献

- 报告问题
- 提交改进的 pull request
- 广而告之
- 有任何反馈请随时联系 [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/kamrify.svg?style=social&label=Follow%20%40kamrify)](https://twitter.com/kamrify)

## 许可证

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

---

> 本 README 为中文译本，原文出自 [kamranahmedse/design-patterns-for-humans](https://github.com/kamranahmedse/design-patterns-for-humans)，原文与译文均遵循 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可。
