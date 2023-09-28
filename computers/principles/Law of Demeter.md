Don't talk to strangers.

- Why

	- It usually tightens coupling
	- It might reveal too much implementation details

- How

A method of an object may only call methods of:

1. The object itself.
2. An argument of the method.
3. Any object created within the method.
4. Any direct properties/fields of the object.

# Example

This is an example to explain Law of Demeter in real world. there is `Paperboy` who has to get a payment from a `Customer`. Lets define some code for a Customer, some mechanism for receiving payments from that customer, and a snippet of code that our paperboy will run.

#wrongExample 
simple Customer class with `firstName`, `lastName` and `wallet`:
```C#
public class Customer {
	private String firstName;
	private String lastName;
	private Wallet myWallet;
	
	public String getFirstName(){ return firstName; }
	
	public String getLastName(){ return lastName; }
	
	public Wallet getWallet(){ return myWallet; }
}
```
simple Wallet class with  minimum methods and properties: 
```C#
public class Wallet {
	private float value;
	
	public float getTotalMoney() { return value; }
	
	public void setTotalMoney(float newValue) {
		 value = newValue; 
	}
	
	public void addMoney(float deposit) {
		 value += deposit; 
	}
	
	public void subtractMoney(float debit) {
	value -= debit;
	}
}
```
and finally somewhere in Paperboy class:
```C#
// code from some method inside the Paperboy class
... 
payment = 2.00; // “I want my two dollars!”
Wallet theWallet = myCustomer.getWallet();
if (theWallet.getTotalMoney() > payment) {
	theWallet.subtractMoney(payment); 
} else {
// come back later and get my money 
}
```

why this is bad?
- Paperboy has access to customer wallet!!! think about real world example.
- Paperboy knows customer has a wallet and can manipulate it. so these three class are `tightly coupled`.  if we change the Wallet class, we may have to make changes to both of the other classes.
- what if customer wallet has been stolen (wallet is null in customer class). Paperboy will throw runtime exception.

#correctExample 
customer
```C#
public class Customer {
	private String firstName;
	private String lastName;
	private Wallet myWallet;
	
	public String getFirstName(){ return firstName;}
	
	public String getLastName(){ return lastName; }
	
	public float getPayment(float bill) {
		if (myWallet != null) {
			if (myWallet.getTotalMoney() > bill) {
				theWallet.subtractMoney(bill); return bill;
			}
		}
	}
}
```
paperboy
```C#
// code from some method inside the Paperboy class
... 
payment = 2.00; // “I want my two dollars!” 
paidAmount = myCustomer.getPayment(payment);
if (paidAmount == payment) {
// say thank you and give customer a receipt 
} else {
// come back later and get my money 
}
```
why this is better?
- The first reason that this is better is because it better models the real world scenario…  The Paperboy code is now ‘asking’ the customer for a payment.  The paperboy does not have direct access to the wallet.  

- The second reason that this is better is because the Wallet class can now change, and the paperboy is completely isolated from that change…

- The third, and probably most ‘object-oriented’ answer is that we are now free to change the implementation of ‘getPayment()’.