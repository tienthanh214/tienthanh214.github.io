---
title: "Note: OOP Design Pattern"
excerpt: "23 design pattern - GoF note"
show_date: true
last_modified_at: 2022-03-02T08:53:04-04:00
tags:
  - java
  - OOP
categories:
  - Design pattern
toc: true
---

# Implementation
Github: [https://github.com/tienthanh214/design-patterns](https://github.com/tienthanh214/design-patterns)

# Lộ trình tôi học

- [ ] Các quan hệ (is-a, has-a, composition, ....)
- [ ] Sơ đồ UML 
- [ ] Code (Java)


# Tài liệu

## Sách
- [ ] Design Patterns: Elements of Reusable Object-Oriented Software
- [ ] Head First Design Patterns
- [ ] Design Patterns For Dummies
- [ ] Pattern Hatching: Design Patterns Applied.
- [ ] Refactoring to Patterns.
- [ ] Patterns of Enterprise Application Architecture.

## Website
- https://sourcemaking.com/design_patterns
- https://refactoring.guru/design-patterns

  UML
- https://viblo.asia/p/bieu-do-lop-uml-Az45bDaVZxY
- https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/


# Vài thuật ngữ

- white-box: visibility, with inheritance the internals of parent classes are often visible to subclasses
- black-box: no internal details of objects are visible


# Nguyên lý

1. **Program to an interface, not an implementation**
    
    Program to a supertype. 
    Sử dụng abstract class thay vì concrete class.

    Dùng interface, sẽ không cần biết cụ thể object được implement bởi class nào, chỉ cần biết interface của nó có thể thực hiện được yêu cầu mong đợi. 

2. **Favor object composition over class inheritance**

    Composition (quan hệ has-a) ưu tiên hơn Inheritance (quan hệ is-a).

    Quan hệ kế thừa là cho phép subclass thừa kế cứng nhắc tất cả các fields và methods từ superclass. Như vậy khi có nhiều subclass muốn thay đổi cài đặt để giải quyết một vấn đề mới nào đó thay vì dùng cài đặt sẵn có ở superclass thì phải override tất . 

    Inheritance không thể thay đổi implementations từ superclass trong run-time, vì inheritance được định nghĩa ở compile-time.

    "Inheritance breaks encapsulation", kế thừa protected hay public, subclass sẽ có toàn bộ thông tin từ superclass.

    Thay vì inheritance để phải override methods cho nhiều subclass, thì tạo object composition, khi đó object này có thể thay đổi tùy ý trong run-time chỉ cần truyền dữ liệu *(object cùng type)* vào hàm làm thay đổi object composition đó.

3. **Encapsulating the concept that varies**

    Xác định những phần thường xuyên thay đổi và đóng gói nó, tách nó khỏi phần ít thay đổi. Như vậy sẽ dễ hơn trong việc cập nhật các thành phần thường xuyên thay đổi đó mà không ảnh hưởng đến phần còn lại.

# Unified Modeling Language - UML
## Class Notation

1. Class
    - public: +
    - private: -
    - protected: #
    - method_name(param) : return type

2. Interface
    - Tên class là chữ nghiêng 
    - Ký hiệu như một hình tròn
    
## Relationships

1. Inheritance (Generalization)
    
    Nét liền, mũi tên tam giác trắng thể hiện quan hệ kế thừa
  
    Subclass -ᐅ Superclass 

    Quan hệ: **is-a**

2. Association

    Nét liền, không có mũi tên thể hiện hai class có quan hệ với nhau nhưng không cái nào sở hữu cái nào. Là tổng quát của aggregation.

    Màn hình và bàn phím không sở hữu lẫn nhau nhưng cả hai có quan hệ kết hợp với nhau hỗ trợ nhập xuất.


3. Aggregation

    Nét liền, mũi tên hình thoi trắng, thể hiện quan hệ "là một phần", vòng đời của các đối tượng có thể là độc lập

    Bánh xe *là một phần* của xe (hoặc xe sở hữu bánh xe), và khi xe (whole) không tồn tại thì bánh xe (part) vẫn tồn tại riêng biệt được.

    Wheel -◇ Car

    Quan hệ: **has-a**, **part-whole**

4. Composition

    Nét liền, mũi tên hình thoi đen, có thể coi composition như "hard" aggregation, chặt hơn, vòng đời của part phụ thuộc vào whole

    Một team bóng (whole) khi không có thành viên (part) thì không thể coi là một team được.

    Player -◆ Team

    Quan hệ: **part-whole**


5. Dependeces

    Nét đứt, mũi tên thường. Đối tượng class B có thể sử dụng đối tượng của class A trong method, không phải là một field của Class B. Khi A thay đổi thì B cũng thay đổi, nhưng không có chiều ngược lại.

    Nhà cung cấp các mặt hàng cho các đại lý, nếu nhà cung cấp thay đổi mặt hàng thì đại lý cũng vậy. 

    Client ---> Supplier

    Quan hệ: **use-a**

6. Realization

    Nét đứt, mũi tên tam giác. Quan hệ giữa lớp implement và interface.

    Dog ---ᐅ Animal

# Design Patterns
## Composition
// todo

## Strategy
**Also known as**: *Policy*

Đóng gói một họ các thuật toán lại vào các class, các class này có chung interface. Nhờ tính đa hình, có thể dễ dàng thay đổi giữa các thuật toán kể cả trong run-time (bằng cách gán object interface bằng instance của concrete class nào đó cùng họ). Giúp việc mở rộng, phát triển các thuật toán mới không ảnh hưởng đến client sử dụng nó, giảm sự phụ thuộc lẫn nhau. 

*(Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use)*
### Problem
Giả sử mình muốn viết con game nhập vai, trong game có nhiều loại vũ khí (súng, kiếm gỗ, thần kiếm, đũa phép thuật, blabla...). Và tất nhiên nhân vật có thể sử dụng vũ khí nào tùy ý. Trong quá trình chơi, nhân vật cũng có thể thay đổi vũ khí.

Tất nhiên là trong tương lai (nếu game thành công :3) thì mình sẽ tạo thêm đa dạng vũ khí hơn hoặc nâng cấp cho các vũ khí cũ. Rõ ràng là mình sẽ muốn làm cho sự thay đổi về vũ khí này trở nên dễ dàng và không ảnh hưởng nhiều đến Nhân vật.

### Solution
Đóng gói mỗi loại vũ khí trong một class riêng (Gun, Sword, MagicWand, ...), chúng có chung interface là *Weapon*. Trong class Character mình sẽ lưu một object weapon có kiểu là *Weapon* để reference đến vũ khí nhân vật dùng.

Bằng kiến thức cơ bản về *polymorphism*, object weapon này có thể sẽ là bất kì loại vũ khí gì miễn nó là subclass của *Weapon*, và vì nó là biến nên có thể thay đổi bất kì lúc nào.

```java
class Character {
    Weapon weapon;
    // ... implement Player ....
    void setWeapon(Weapon newWeapon) {
        this.weapon = newWeapon;
    }
}
```
Đổi vũ khí trong lúc chơi:
```java
Character p = new Character();
p.setWeapon(new Gun());
// do something
p.setWeapon(new Sword());
```
Trong tương lai mình có thêm vũ khí Knife, chỉ việc kế thừa interface *Weapon* rồi implement nó. Sau đó Player chỉ việc dùng nó bằng cách gọi hàm ```setWeapon(new Knife())```. Có thể thấy sự phát triển của vũ khí không liên quan đến sự phát triển của nhân vật.

![image-center](/assets/images/post/design_pattern/strategy.PNG){: .align-center}


### Note
Có thể sử dụng *anonymous class* để tạo ra object thay vì phải tạo ra thêm class.

## Decorator
**Also known as**: *Wrapper*

Gắn các trách nhiệm bổ sung cho một đối tượng một cách linh hoạt bằng cách để nó wrap trong một class khác cùng kế thừa một superclass. Cho phép một sự thay thế linh hoạt cho subclassing để mở rộng chức năng

*(Attach additional responsibilities to an object dynamically. Decorators provide a
flexible alternative to subclassing for extending functionality)*

### Problem
Mình cần build app Text Editor, giả sử đã làm xong phần hiển thị văn bản thô sơ. Bây giờ mình muốn trang trí nó như thêm border, thêm scrollbar, blabla...

Ok với cách suy nghĩ inheritance bình thường, bây giờ viết ra subclass Border, ScrollBar kế thừa PlainText, mỗi class sẽ trang trí như tên của nó.

Vấn đề là giờ mình vừa muốn vẽ border vừa muốn thêm scrollbar, như vậy phải viết thêm class BorderScrollBar. Vấn đề sẽ không có gì nếu không có rất nhiều class trang trí khác nhau, với cách kế thừa thông thường này sẽ tạo ra rất nhiều class (trang trí với 2 cái thì sẽ là tổ hợp chập 2, trang trí với 3 cái thì tổ hợp chập 3 của các loại trang trí).

Vô cùng khó khăn khi thêm 1 class trang trí mới (lúc đó phải thêm lần lượt vào các tổ hợp trên kia), rồi lúc thay đổi method bên trong class nào đó thì phải thay đổi các class liên quan rất là khó bảo trì và nâng cấp.

### Solution
Ta có thể sử dụng các biến đối tượng để đặt trong class, và chúng kế thừa cùng một superclass

**Transparent enclosure**:  wrap object class (abstract) này trong class khác và thêm tính năng, lúc này không cần quan tâm object là kiểu gì, và object này không biết nó đã được wrap, các method cũ được dùng như thường bây giờ mở rộng thêm tính năng wrap class vừa thêm. 

Gọi *Glyph* là interface chung, và *Decorator* là class cha của các kiểu trang trí như ScrollBar hay Border. PlainText và *Decorator* cùng kế thừa *Glyph*. Như vậy tất cả các class này đều có chung interface *Glyph*. (mình phân tách ra PlainText 1 nhánh, Decorator 1 nhánh để phân biệt chức năng sau này dễ phát triển, muốn thêm loại trang trí thì kế thừa Decorator, ...)

wrap PlainText trong Border, trong Border chứa object PlainText như vậy chỉ cần delegate cho object PlainText đó tự vẽ ra văn bản thô sơ, rồi Border sẽ vẽ ra khung. Nếu muốn thêm scrollbar, wrap object (Border chứa object PlainText vừa tạo trên) vào ScroolBar, để object đó tự vẽ cái mà nó quản lý, ScroolBar chỉ việc vẽ thêm scrollbar vào (hãy nghĩ đến Đệ quy). Nhờ tính đa hình, ta không cần quan tâm cụ thể object là Border hay PlainText hay gì gì cả, nó chỉ là một biến kiểu interface *Glyph*.

Như vậy Decorator Pattern cho phép lồng các decorators một cách đệ quy, cho phép không giới hạn các chức năng thêm vào

Ví dụ trong Java: BufferedReader -ᐅ InputStreamReader -ᐅ InputStream (abstract class). 

![image-center](/assets/images/post/design_pattern/decorator_example.png){: .align-center}

> Hình ảnh ví dụ cho class DarkRoast wrap trong Mocha wrap trong Whip (một ly DarkRoast kèm Mocha và Whip). *Nguồn*: Head First Design Pattern

Dưới đây là đoạn code ý tưởng
```java
abstract class Decorator {
    private Glyph component;
    Decorator(Glyph component) {
        this.component = component
    }
    void draw() {
        component.draw(); // delegate
    }
}

class Border extends Decorator {
    public Border(Glyph component) {super(component);}

    void draw() {
        super.draw();
        // implement draw border
    }
}

class ScrollBar extends Decorator {
    public ScrollBar(Glyph component) {super(component);}

    void draw() {
        super.draw();
        // implement draw scrollbar
    }
}
```

Bây giờ, hãy thử tạo một PlainText có trang trí scrollbar và cả border
```java
Glyph stack = new PlainText();
stack = new ScrollBar(stack);
stack = new Border(stack);
```
![image-center](/assets/images/post/design_pattern/decorator.png){: .align-center}

## Abstract Factory
**Also known as**: *Kit*

Cung cấp một interface cho phép tạo ra các object liên quan nhau mà không cần quan tâm cụ thể concrete class của nó là gì. Có thể gọi là Factory của các Factory

*(Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes)*


### Problem
GUI cần hỗ trợ hiển thị trên nhiều platform, mỗi platform lại cần hiện một kiểu. Ví dụ trên Mac, Windows, Android, ...

Mỗi Button, DialogBox, Label, ... trên mỗi platform cần thể hiện ra trên màn hình khác nhau để phù hợp với platform đó. Một cách hard-code là với mỗi class viết ra các concrete class cài đặt cho hiển thị trên từng platform. Nếu làm như vậy thì mỗi class Button, Label và vô số class khác đều phải viết rất là nhiều, và để dùng đúng class thì phải if else các kiểu với MỖI object được tạo ra phụ thuộc vào platform.

### Solution

Cách giải quyết là tạo một abstract class GUIFactory, có các subclass như MacFactory, WinFactory, ... Có cài đặt các method như createLabel, createButton để tạo ra object thuộc class tương ứng

Thay vì với MỖI object phải if else dài dòng để tùy với platform nào để tạo ra object thuộc class nào:
```java
Label lbl = new MacLabel();  
```
thì chỉ cần if else một lần ở lúc chọn Factory:
```java
GUIFactory guiFactory = new MacFactory();
// then
Label lbl = guiFactory.createLabel();
```

![image-center](/assets/images/post/design_pattern/abstract_factory.png){: .align-center}


Abstract factory cung cấp interface cho việc tạo ra một bộ sản phẩm (ví dụ như label, button, ...), từ đây tạo được một hoặc nhiều concrete factories sản xuất cùng một sản phẩm nhưng với cách triển khai (cài đặt) khác nhau. Do đó client chỉ cần tương tác thông qua interface của factory hoặc product. Và vì patern này được sử dụng để tạo toàn bộ sản phẩm nên khi thêm sản phẩm mới thì phải thay đổi interface dẫn đến các lớp con thay đổi theo (khác với Factory method chỉ tạo 1 sản phẩm)

**Thắc mắc**: Abstract factory chỉ mới giải quyết được vấn đề tạo chung một factory tránh việc tạo object khó khăn, nhưng chưa tránh được việc tạo ra các concrete class với mỗi widget phải implement mỗi platform một subclass riêng. Để giải quyết -> Bridge pattern

## Factory Method
**Also known as**: *Virtual Constructure*

Định nghĩa một interface để tạo object, nhưng để cho các lớp con quyết định lớp cụ thể nào sẽ được tạo ra. Giao việc khởi tạo một đối tượng cụ thể cho lớp con.

*(Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses)*

### Problem
Làm thế nào mà Microsoft Word hay Android Studio có thể tạo ra những template với nội dung có sẵn theo yêu cầu của người dùng. Word khi New một document thì ở trang New, người dùng sẽ được gợi ý một số template có sẵn như Blank, Cover letter, Report, Certificate, ... ta chỉ việc chọn vào mẫu đó và như vậy là một document đã được tạo ra theo mẫu định sẵn của Word.

Trang New chỉ có nhiệm vụ quản lý các template document (hiển thị các template cho người dùng chọn, tạo ra template theo yêu cầu nếu người dùng click vào đó). Mỗi template sẽ được tạo theo cách riêng khác nhau, và tất nhiên khi code trang New (gọi là class *Application*) mình chỉ biết quá trình chung tạo ra document (tuỳ vào người dùng chọn template nào, load, hiển thị nó lên màn hình, ....), chứ không biết một template được tạo ra, cài đặt cụ thể như thế nào.

Application cũng không thể đoán được người dùng sẽ chọn template nào để tạo ra trước, nó chỉ biết khi nào cần tạo ra document và loại template document nào sẽ được tạo ra (sau khi người dùng click chọn vào template đó).

Vấn đề đặt ra là ở Application, làm sao có thể tạo ra template document theo ý người dùng, khi mà chỉ biết về interface (hoặc abstract class) của các template. Gọi interface chung của các template là *Document*.

### Solution
Tạo một abstract method *createDocument()* ở class Document. Còn việc tạo ra template document nào thì uỷ thác cho class con kế thừa nó làm, hàm này được gọi là *factory method*.

Quá trình tạo mới document theo template sẽ được cài đặt trong method newDocument() như sau:

```java
abstract class Application {
    // factory method
    abstract Document createDocument();
    
    public Document newDocument() {
        Document document = createDocument();
        // prepare, load and show document on screen
        document.load();
        document.show();
        return document;
    }
}
```

Concrete class BlankApplication kế thừa Application sẽ cài đặt factory method *createDocument()* trả về cụ thể object blank template document là văn bản trống

``` java
class BlankApplication extends Application {
    Document createDocument() {
        return new BlankDocument();
    }
}
```
Tương tự để tạo một template Report:
```java
class ReportApplication extends Application {
    Document createDocument() {
        return new ReportDocument();
    }
}
```
Trong quá trình phát triển phần mềm, khi có thêm một template document mới thì chỉ việc thêm class tương ứng vào, như vậy không ảnh hưởng đến các class cũ đã được cài đặt và kiểm thử trước đó.

![image-center](/assets/images/post/design_pattern/factorymethod.png){: .align-center}
> Class diagram cho Factory Method tổng quát (*parallel class hierarchies* Product và Creator)

Có thể bạn sẽ thấy mỗi concrete class chỉ cài hàm *createDocument* có một dòng khá là phí, trên đây chỉ là một ví dụ để thể hiện ý nghĩa của Factory Method là giao việc khởi tạo lại object cụ thể cho class con, ta chỉ cần dùng interface (hay abstract class) giúp loại bỏ sự ràng buộc của các lớp cụ thể vào code, giảm phụ thuộc tăng tính mở rộng, che giấu được việc khởi tạo object, chỉ cần tương tác với interface (hoặc abstract class). Sử dụng Factory Method như một chuẩn để khởi tạo object

Ta cũng có thể làm như sau:
```java
class MyApplication extends Application {
    Document createDocument(DocumentType type) {
        switch (type) {
            case DocumentType.BLANK:
                return new BlankDocument();
            case DocumentType.REPORT:
                return new ReportDocument();
            default:
                return new CertificateDocument(); 
        }
    }
}
```
Phiên bản này được gọi là *Parameterized Factory Method* (theo GoF) khi có truyền tham số vào cho factory method, qua đó cho thấy Factory Method rất linh động.

## Singleton
Singlethon pattern đảm bảo lớp chỉ có thể tạo ra một instance duy nhất và cung cấp một điểm truy cập toàn cục đến nó.

*Ensure a class only has one instance, and provide a global point of access to it*

### Problem
Một số ứng dụng cần tạo ra chính xác một instance, ví dụ như những tài nguyên dùng chung như database để truy xuất, theo dõi trạng thái trong quá trình sử dụng. Hoặc ta cần quản lý số lượng tài nguyên bị giới hạn, ví dụ trong game nào đó, mỗi người chơi chỉ sở hữu duy nhất 1 loại nhân vật, làm thế nào để ngân chặn người chơi sỡ hữu nhiều hơn 1 nhân vật.

### Solution
Ta cần ngăn chặn việc tạo ra instance tự do, không cho *new* ra một đối tượng. Để ngăn chặn tạo ra object ta chỉ cần cho phương phức khởi tạo constructor là **private**.

Bây giờ, ta không thể tự tạo ra object ở ngoài class, bên trong class chính là nơi duy nhất có thể sử dụng *private constructor* này. Tạo một *static method* cho phép tạo instance của class, vì ở bên ngoài class không thể tạo ra object, vì vậy để tạo instance ta cần sử dụng *static method*

Cuối cùng ta cần một biến để lưu lại instance được tạo ra bằng cách sử dụng một static attribute *_instance*

```java
class Singleton {
    private static Singleton _instance = null;
    private Singleton() {}
    public static Singleton getInstance() {
        if (_instance == null) 
            _instance = new Singleton();
        return _instance;
    }
}
```
### Note
Phiên bản Singleton Pattern được cài đặt ở trên được gọi là Lazy Initialization chỉ khởi tạo khi cần thiết, ngoài ra còn có một số biến thể khác. 

Mẫu Singleton đảm bảo chỉ cho phép tạo ra tối đa một instance, tuy nhiên trong môi trường multithread, với cách cài đặt đơn giản trên không đảm bảo rằng duy nhất một instance được tạo ra, giá trị của biến static *_instance* có thể sẽ nhận qua các giá trị khác nhau khi có nhiều thread gọi hàm *getInstance()* cùng một lúc. Cách giải quyết trong Java là sử dụng từ khoá **synchronized** để đồng bộ, chỉ cho phép 1 thread duy nhất vào hàm tại một thời điểm.
```java
public static synchronized Singleton getInstance() {
    if (_instance == null) 
        _instance = new Singleton();
    return _instance;
}
```
> Thread-safe Singleton

Tuy nhiên phương pháp đồng bộ trên là tốn kém, thật ra ta chỉ cần bật đồng bộ hoá ở lần khởi tạo đầu tiên, ở những lần *getInstance()* sau thì câu lệnh *if* luôn trả về false rồi. 

```java
class Singleton {
    private volatile static Singleton _instance; // volatile đọc từ bộ nhớ chính chứ không phải từ cache
    private Singleton() {}
    public static Singleton getInstance() {
        if (_instance == null) {
            synchronized (Singleton.class) {
                if (_instance == null) {
                    _instance = new Singleton();
                }
            }
        }
        return _instance;
    }
}
```
> Double-checked locking Singleton

Một phương pháp khác thường được sử dụng để cài đặt (và được cho là ổn định nhất) là **Bill Pugh Singleton**, sử dụng một *helper inner class*, khi class Singleton được load lên bộ nhớ thì class SingletonHelper vẫn chưa được load, chỉ khi có lời gọi lần đầU đến từ *getInstance()* method nó mới được load và tạo ra instance Singleton


```java
class BillPughSingleton {
    private BillPughSingleton() {}
     private static class SingletonHelper {
        private static final BillPughSingleton _instance = new BillPughSingleton();
    }
    public static BillPughSingleton getInstance() {
        return SingletonHelper._instance;
    }
}
```

## Bridge

### Problem
Ứng dụng đọc và hiển thị nhiều loại ảnh lên màn hình, ứng dụng còn phải tương thích, hỗ trợ trên nhiều hệ điều hành khác nhau.

Có rất nhiều loại file image khác nhau như JPG, PNG, BMP, TIFF, GIF - mỗi loại image đều có một cấu trúc riêng nên cách read cũng khác nhau. Ứng dụng cần hỗ trợ trên các hệ điều hành như Windows, Mac, Linux. Theo tư duy kế thừa thông thường, mình cần phải viết với mỗi loại image thì phải viết 3 concrete class hỗ trợ hiển thị trên từng OS, kiểu như; JPGWindow, PNGWindow, BMPWindow, ..., JPGMac, ... như vậy nó sẽ tăng theo cấp số nhân rất là nhiều subclass phải tạo ra.

### Solution

Phân tách abstraction và implementation ra 2 class riêng. 
Lớp abstract giữ object reference đến class implement, lúc đó chỉ cần delegate cho class implement làm việc.

## Command 
### Problem
Mình muốn tạo ra một Text Editor hỗ trợ các chức năng như Copy, Paste, Open, Save, Undo, Redo, ... cho phép người dùng click vào button của chức năng trên toolbar để sử dụng chức năng đó. 

Một cách tự nhiên, theo OOP, mỗi icon mình sẽ tạo một class tương ứng để nó làm việc mà nó phải làm. Thoạt nhìn rất là ok.

Tuy nhiên, một chức năng có thể có nhiều user interface để tiện cho người dùng (ví dụ như để *copy* thì có thể nhấn vào button Copy, shortcut ctrl + C, hoặc chuột phải -> Copy, ...). 
Nếu hard-code mỗi class khác nhau nhưng đều thực hiện cùng một chức năng thì rất là code duplicate. Một cách khác là tham số hóa chức năng đó vào function để gọi, nhưng nhược điểm là function thì rất khó mở rộng, không linh động trong tham số truyền vào, đặc biệt là không undo/redo được.

### Solution
Hãy đóng gói chức năng đó vào trong class. Thay vì request trực tiếp, thì hãy thông qua trung gian Command object. ....

Ném request đóng gói trong Command object để object này rồi delegate cho server làm điều mà nó phải làm. Như bồi bàn nhận đơn từ khách hàng sau đó đưa cho đầu bếp và bảo ông nấu đi.

Dùng abstract class chung cho subclass chức năng nữa, giúp linh động khi dùng cùng một interface nhưng lại có thể handle các request khác nhau. Trong tương lai dễ bảo trì nâng cấp.


## Iterator

### Problem
Làm sao để duyệt (traversal) qua một cấu trúc dữ liệu bất kì mà không cần quan trọng cấu trúc bên trong nó. Ví dụ: LinkedList, BinarySearchTree, Heap, ... tất cả đều có cấu trúc riêng biệt, ngoài ra đối với cấu trúc BinarySearchTree ta có thể sẽ cần duyệt theo thứ tự khác nhau như inorder - preorder - postorder. 

Trong C++, có thể ta đã từng dùng vòng lặp kiểu này:
```c++
for (auto it = S.begin(); it != S.end(); ++it) {
    // do something
}
```
> Cho dù *S* kiểu gì: vector, set, map, priority_queue, ....

Việc thống nhất cách duyệt cấu trúc dữ liệu như này rất tiện cho người dùng, người dùng thư viện không cần quan tâm cụ thể cấu trúc bên trong và cụ thể cách duyệt, chỉ việc for thôi :v.

### Solution
Áp dụng nguyên lý *encapsulating the concept that varies*, đóng gói các cách duyệt trong class tương ứng.

Tạo một abstract class Iterator với các method như ``` begin(), next(), hasNext()``` để xác định element đầu tiên của CTDL, để biết element tiếp theo phải duyệt, để xem đã duyệt xong chưa.

Tạo các subclass kế thừa Iterator, kiểu như LinkedListIterator, HeapIterator, PreorderIterator, .... để implement cụ thể cách duyệt đối với từng CTDL hoặc cách duyệt. Trong mỗi class sẽ chứa một object để reference đến object CTDL cần duyệt.

Trong tất cả class CTDL, thêm method kiểu như 
```java
class List extends DataStructure {
    // ....
    Iterator<DataStructure> createIterator() {
        return new ListIterator<DataStructure>(this.data);
    }
}
``` 
trả về một object kiểu Iterator ứng với CTDL này. Với DataStructure là abstract class mà tất cả CTDL kế thừa. Mình dùng generic type ở đây chỉ để nó linh động với mọi kiểu dữ liệu khác :v


## Visitor

### Problem


Nói chung là, muốn cùng làm (nhiều gì) gì đó với dữ liệu trên nhiều class cấu trúc khác nhau. Vì các class đã được implement khá hoàn hảo nên chỉ chấp nhận thay đổi rất nhỏ trong class.

Ví nhụ như thêm chức năng save thông tin vào file CSV trên các đối tượng khác nhau Student, Teacher, Professional, ...

### Solution

Tạo abstract class Visitor, các subclass implement những chức năng muốn thực hiện cụ thể như ExportVisitor, BlaBlaVisitor

Trong mỗi class thuộc hierarchical Visitor, implement tất cả method để thực hiện công việc đó cho riêng từng đối tượng.

```java
class ExportVisitor implements Visitor {
    // this class do export to CSV for every type
    public void visitStudent() { 
        // implement export for Student
    };
    public void visitTeacher() { 
        // implement export for Teacher

    };
    public void visitProfessional() { 
        // implement export for Professional
    };
    //...  so forth
}
```
Ở trong các class đối tượng chỉ cần thêm một method chung name
```java
class Student {
    // .....
    public void accept(Visitor visitor) {
        visitor.visitStudent(this);
    }
}
```

Cái đẹp của kế thừa, đa hình ở đây là mình chỉ cần truyền vào hàm *accept* tham số có kiểu abstract Visitor, không quan tâm concrete class thật của nó là gì, điều này giúp mình có thể sử dụng nhiều loại Visitor chức năng khác nhau, mà không cần thay đổi gì nhiều ngoài việc đổi tham số truyền vào. 

Kết hợp cùng *Iterator pattern* hỗ trợ duyệt qua các CTDL sau đó áp dụng chức năng vào hoy.
```java
Visitor exportVisitor = new ExportVisitor();
for (it = S.begin(); it = it.next(); it.hasNext()) {
    it.accept(exportVisitor);
}
```

Giả sử trong tương lai, mình muốn thêm chức năng tính số giờ làm việc cho từng đối tượng. Chỉ cần cài đặt class *HourVisitor*, sau đó thay vì truyền vào hàm ```accept(exportVisitor)``` thì đổi thành ```accept(hourVisitor)```. 

Bằng cách chỉ thêm vào mỗi class đối tượng 1 hàm accept chỉ vài dòng, bằng Visitor ta đã có thể mở rộng thoải mái thêm nhiều chức năng mà không tác động đến cá class đối tượng này nữa. 

## Observer
**Also know as**: Dependents, Publish-Subcribe

Xác định phụ thuộc một - nhiều, khi đối tượng thay đổi trạng thái, các đối tượng phụ thuộc nó sẽ cũng nhận được thông báo thay đổi.

*(Define a one-to-many dependency between objects so that when one object
changes state, all its dependents are notified and updated automatically)*
### Problem
Một nhà xuất bản báo (publisher/subject) bắt đầu kinh doanh, ta (subcriber/observer) đăng ký vào nhà xuất bản này để khi có báo mới họ sẽ gửi cho ta, và khi chán ta có thể hủy đăng ký để không nhận báo từ họ nữa. Trên thực tế, một nhà xuất bản có thể có rất nhiều người đăng ký và hủy đăng ký qua từng ngày.

Hoặc ví dụ về biểu đồ, cùng một data có thể biểu diễn dưới nhiều dạng biểu đồ khác nhau như biểu đồ hình cột, tròn, đường, .... Mỗi biểu đồ có một cách thể hiện khác nhau, nhưng dữ liệu là từ một nguồn.

### Solve
Tạo interface Subject thể hiện cho đối tượng dữ liệu, và interface Observer thể hiện những đối tượng quan sát dữ liệu.

Trong Subject sẽ chứa một List các observer cần nhận dữ liệu từ nó, cùng các hàm addObserver, removeObserver, và notifyObservers để thông báo thay đổi. Vì các observers có chung interface nên nó có kiểu cụ thể là gì cũng được (miễn là chung interface) nên dễ dàng lưu nó trong mảng Observer[] cùng một vòng for để thông báo cho tất cả bằng cách gọi hàm update của observer.

Trong class Observer có phương thức register, unRegister nhận tham số kiểu Subject để đăng ký vào hoặc hủy đăng ký.

### Note
Java hỗ trợ Observer và Observable class trong java.util