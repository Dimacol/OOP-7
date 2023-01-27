## SOLID - это принципы разработки программного обеспечения, следуя которым Вы получите хороший код, который в дальнейшем будет хорошо масштабироваться и поддерживаться в рабочем состоянии.

### S -  Single Responsibility Principle - принцип единственной ответственности. Каждый класс должен иметь только одну зону ответственности.

### O -  Open closed Principle - принцип открытости-закрытости. Классы должны быть открыты для расширения, но закрыты для изменения.

### L -  Liskov substitution Principle - принцип подстановки Барбары Лисков. Должна быть возможность вместо базового (родительского) типа (класса) подставить любой его подтип (класс-наследник), при этом работа программы не должна измениться.

### I -   Interface Segregation Principle - принцип разделения интерфейсов. Данный принцип обозначает, что не нужно заставлять клиента (класс) реализовывать интерфейс, который не имеет к нему отношения.

### D -   Dependency Inversion Principle - принцип инверсии зависимостей. Модули верхнего уровня не должны зависеть от модулей нижнего уровня. И те, и другие должны зависеть от абстракции. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

 ## принцип единственной ответственности на примере.
public class AutomatServices {
    private final AutomatRepository automatRepository;

    public AutomatServices(AutomatRepository automatRepository) {
        this.automatRepository = automatRepository;
    }

    public GetAutomatsList GetAutomatsList() {                                                    ==> получение информации о наличии продуктов в магазине
        if (automatRepository.getAutomatsList().isEmpty()) {
            return new GetAutomatsList(true, "Репозиторий торговых аппаратов пустой", null);
        }
        return new GetAutomatsList(false, null, automatRepository.getAutomatsList());
    }

    public GetProductsInAutomat getProductsInAutomat(Automat automat) {                            ==> добавление продуктов в заказ, список продуктов в заказе
        HashMap<Product, Integer> products = automat.getProductsList();

        if (products.isEmpty()) {
            return new GetProductsInAutomat(true, "В заказе нет товаров. Добавьте", null);
        }

        return new GetProductsInAutomat(false, null, products);
    }

    public AutomatRepository getAutomatRepository() {
        return automatRepository;
    }
}