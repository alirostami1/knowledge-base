The Open-Closed Principle requires that **classes should be open for extension and closed to modification.**

Modification means changing the code of an existing class, and extension means adding new functionality.
![[1_0MtFBmm6L2WVM04qCJOZPQ.webp]]

### Code example

Lets try to add store in database to [[S - Single responsibility principle#correct example\|InvoicePersistence]] class.

#### Wrong example
This code violates the open close principle.
#wrongExample 

```java
public class InvoicePersistence {
    Invoice invoice;

    public InvoicePersistence(Invoice invoice) {
        this.invoice = invoice;
    }

    public void saveToFile(String filename) {
        // Creates a file with given name and writes the invoice
    }

    public void saveToDatabase() {
        // Saves the invoice to database
    }
}
```

As you see, there modifying `InvoicePersistence` violates open close principle.

#### Correct example
To fix this example we need to change `InvoicePersistence` type to  interface and add `save`  method. this means each persistence class have to implement `save` method.
#correctExample 
```java
interface InvoicePersistence {

    public void save(Invoice invoice);
}
```
```java
public class DatabasePersistence implements InvoicePersistence {

    @Override
    public void save(Invoice invoice) {
        // Save to DB
    }
}
```
```java
public class FilePersistence implements InvoicePersistence {

    @Override
    public void save(Invoice invoice) {
        // Save to file
    }
}
```

Our class structure now looks like this

![[solid-article-image-1.png]]

As you see we can add any other type of persistence ^[different databases.] easily just by extending.

#### Extra
 We extend our app and have multiple persistence classes like `InvoicePersistence`, `BookPersistence` and we create a `PersistenceManager` class that manages all persistence classes:

```java
public class PersistenceManager {
    InvoicePersistence invoicePersistence;
    BookPersistence bookPersistence;
    
    public PersistenceManager(InvoicePersistence invoicePersistence,
                              BookPersistence bookPersistence) {
        this.invoicePersistence = invoicePersistence;
        this.bookPersistence = bookPersistence;
    }
}
```

We can now pass any class that implements the `InvoicePersistence` interface to this class with the help of [[polymorphism]]. This is the flexibility that interfaces provide.