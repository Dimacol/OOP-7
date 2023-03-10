## SOLID - это принципы разработки программного обеспечения, следуя которым Вы получите хороший код, который в дальнейшем будет хорошо масштабироваться и поддерживаться в рабочем состоянии.

### S -  Single Responsibility Principle - принцип единственной ответственности. Каждый класс должен иметь только одну зону ответственности.

### O -  Open closed Principle - принцип открытости-закрытости. Классы должны быть открыты для расширения, но закрыты для изменения.

### L -  Liskov substitution Principle - принцип подстановки Барбары Лисков. Должна быть возможность вместо базового (родительского) типа (класса) подставить любой его подтип (класс-наследник), при этом работа программы не должна измениться.

### I -   Interface Segregation Principle - принцип разделения интерфейсов. Данный принцип обозначает, что не нужно заставлять клиента (класс) реализовывать интерфейс, который не имеет к нему отношения.

### D -   Dependency Inversion Principle - принцип инверсии зависимостей. Модули верхнего уровня не должны зависеть от модулей нижнего уровня. И те, и другие должны зависеть от абстракции. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

 ## 1.принцип единственной ответственности на примере.

public abstract class Product {
    protected Integer id;
    protected String name;
    protected Integer price;
    protected static int defaultIndex = 1;

    public Product(String name, int price) {
        this.id = defaultIndex++;
        this.name = name;
        this.price = price;
    }

    @Override
    public String toString() {
        return String.format("%s - %s, стоит %s", id, name, price);
    }

    public Integer getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public Integer getPrice() {
        return price;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(Integer price) {
        this.price = price;
    }
}

## 2. Принцип открытости-закрытости рассмотрим на примере
Проектируя таким образом код мы не будем нарушать принцип открытости-закрытости, так как мы расширяем нашу функциональность, а не изменяем (модифицируем) наш класс.

public class DrinkSnackProduct extends Product {
    public DrinkSnackProduct(String name, Integer price) {
        super(name, price);
    }
}
## 3.принцип подстановки Барбары Лисков
что класс, разработанный путем расширения на основании базового класса, должен переопределять его методы так, чтобы не нарушалась функциональность с точки зрения клиента. То есть, если разработчик расширяет ваш класс и использует его в приложении, он не должен изменять ожидаемое поведение переопределенных методов. 
(Примера в проекте нет вставил чтобы усвоить)
class Rectangle {
    
    private int width;
    private int height;
    
    public int getWidth() {
        return width;
    }
  
    public int getHeight() {
        return height;
    }

    public void setWidth(int width) {
        this.width = width;
    }
  
    public void setHeight(int height) {
        this.height = height;
    }
}

class Square implements Rectangle {
    
    public void setSize(int size) {
        super.setWidth(size);
        super.setHeight(size);
    }
}
Класс Square(Квадрат) наследуется от Rectangle(прямоугольник), а так как у квадрата все стороны равны, в классе Square мы просто задаем ширину и высоту, одну и ту же. В итоге, мы испортили изначальную идею класса Rectangle, в который заложена логика, что стороны могут отличаться. Получается, не меняя базовый класс, мы умудрились нарушить данный принцип.

В этом примере Square должен быть отдельным классом и ни в коем случае не наследоваться от Rectangle. То есть, поведение методов не должно изменяться. Если написано, что метод возвращает ширину, значит он и должен возвращать ширину, а не что-то другое.



## 4.принцип разделения интерфейсов 
вариация принципа открытости/закрытости, о котором говорилось ранее. Его можно описать так: объекты в программе можно заменить их наследниками без изменения свойств программы

public abstract class View implements ViewInterface {
    protected boolean error;
    protected String errorMessage;

    public View(boolean error, String errorMessage) {
        this.error = error;
        this.errorMessage = errorMessage;
    }

    public String getErrorMessage() {
        return errorMessage;
    }

    public boolean getError() {
        return error;
    }
}

public interface ViewInterface {
    void printList();
}


## 5.принцип инверсии зависимостей
зависимости внутри системы строятся на основе абстракций. Модули верхнего уровня не зависят от модулей нижнего уровня. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.
Модули верхних уровней не должны зависеть от модулей нижних уровней. Если по простому, то нужно делать код так, что-бы этот код имел как можно меньше зависимостей и не было круговых зависимостей, например модуль A зависит от модуля B, а модуль B зависит от модуля A.