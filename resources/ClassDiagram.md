<!-- - The program utilizes object-oriented principles with encapsulated classes representing system entities.

- Inheritance creates hierarchies - `Customer` and `Driver` inherit from a base class `User` to share common attributes like `id` and `name`.

- `Order` from `Customer` and `Rating` from `Driver`.

- Lists in the `DataStore` manage `Customer`, `Driver`, `Order`, `Rating`, and `MenuItem` objects for efficient data operations.

- Service classes like `OrderService`, `DeliveryService`, and `RatingService` handle business logic.

## Class Diagram

The class diagram represents the entities in the system and their relationships. 
The diagram shows the classes `Customer`, `Driver`, `MenuItem`, `Order`, `Rating`, `OrderService`, `DeliveryService`, `RatingService`, and `DataStore`, along with their attributes and methods. 
The relationships between the classes are depicted using arrows to show how the entities are related to each other.

 -->
```mermaid
classDiagram
    class Customer {
        -String id
        -String name
        -String address
        -List<Order> orderHistory
        +placeOrder(Order order)
        +rateDriver(Driver driver, Rating rating)
        +getOrderHistory()
    }

    class Driver {
        -String id
        -String name
        -String vehicle
        -List<Rating> ratings
        -boolean isAvailable
        +acceptOrder(Order order)
        +completeDelivery(Order order)
        +updateAvailability(boolean status)
        +getAverageRating()
    }

    class MenuItem {
        -String id
        -String name
        -double price
        -String description
        +getPrice()
        +getName()
    }

    class Order {
        -String id
        -Customer customer
        -List<MenuItem> items
        -Driver assignedDriver
        -OrderStatus status
        -DateTime createdAt
        -DateTime deliveredAt
        +calculateTotal()
        +assignDriver(Driver driver)
        +updateStatus(OrderStatus status)
    }

    class Rating {
        -String id
        -int score
        -String comment
        -Customer customer
        -Driver driver
        -DateTime createdAt
        +getScore()
        +getComment()
    }

    class OrderService {
        +createOrder(Customer customer, List<MenuItem> items)
        +processOrder(Order order)
        +cancelOrder(Order order)
        +getOrderStatus(String orderId)
    }

    class DeliveryService {
        +assignDriver(Order order)
        +updateDeliveryStatus(Order order, OrderStatus status)
        +getAvailableDrivers()
    }

    class RatingService {
        +createRating(Customer customer, Driver driver, int score, String comment)
        +getDriverRatings(String driverId)
        +calculateAverageRating(String driverId)
    }

    class DataStore {
        -List<Customer> customers
        -List<Driver> drivers
        -List<Order> orders
        -List<Rating> ratings
        -List<MenuItem> menuItems
        +saveCustomer(Customer customer)
        +saveDriver(Driver driver)
        +saveOrder(Order order)
        +saveRating(Rating rating)
    }

    Customer "1" --> "*" Order: places
    Order "*" --> "1" Customer: belongs to
    Order "*" --> "1" Driver: assigned to
    Order "*" --> "*" MenuItem: contains
    Driver "1" --> "*" Rating: receives
    Rating "*" --> "1" Customer: given by
    OrderService --> DataStore: uses
    DeliveryService --> DataStore: uses
    RatingService --> DataStore: uses
 ```