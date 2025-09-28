package main.java;

// Родительский класс
abstract class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() { return name; }
    public double getPrice() { return price; }

    public abstract void displayInfo();
}

// Наследование
class Electronic extends Product {
    private String brand;

    public Electronic(String name, double price, String brand) {
        super(name, price);
        this.brand = brand;
    }

    @Override
    public void displayInfo() {
        System.out.println("Электроника: " + getName() +
                " | Бренд: " + brand +
                " | Цена: " + getPrice() + " руб.");
    }
}

// Ассоциация
class Category {
    private String title;

    public Category(String title) {
        this.title = title;
    }

    public void assignProduct(Product product) {
        System.out.println("Товар '" + product.getName() + "' отнесён к категории '" + title + "'");
    }
}

// Агрегация
class Cart {
    private java.util.List<Product> products = new java.util.ArrayList<>();

    public void addProduct(Product product) {
        products.add(product);
    }

    public void showCart() {
        System.out.println("Корзина:");
        for (Product p : products) {
            p.displayInfo();
        }
    }

    public java.util.List<Product> getProducts() {
        return products;
    }
}

// Композиция
class Order {
    private Cart cart; // заказ не существует без корзины

    public Order(Cart cart) {
        this.cart = cart;
    }

    public void confirmOrder() {
        System.out.println("Заказ подтверждён. Содержимое:");
        cart.showCart();
    }
}

public class OnlineShop {
    public static void main(String[] args) {
        Product phone = new Electronic("Смартфон", 25000, "Samsung");
        Product laptop = new Electronic("Ноутбук", 55000, "Lenovo");

        Category electronics = new Category("Электроника");
        electronics.assignProduct(phone);
        electronics.assignProduct(laptop);

        Cart cart = new Cart();
        cart.addProduct(phone);
        cart.addProduct(laptop);

        Order order = new Order(cart);
        order.confirmOrder();
    }
    
}

