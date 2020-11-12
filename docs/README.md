# QWQER API Documentation


<br>


## Flow

To make **QWQER** delivery order it's necessary to have a business account, and process these steps:

1. Call login endpoint at: [`/api/xr/mch/login`](api-endpoints?id=authorization)
2. Request estimated delivery price at: [`/api/xr/mch/delivery_price`](api-endpoints?id=check-delivery-price)
3. Create **QWQER** delivery order at: [`/api/xr/mch/delivery`](api-endpoints?id=create-delivery-order)
4. Make a payment for the delivery order at: [`/api/xr/mch/delivery_payment`](api-endpoints?id=delivery-order-payment)

After these steps ** QWQER ** will be place your delivery order and our couriers will process it.


<br>


## API Url

<!-- tabs:start -->

### **Test API url**

[https://test.qwqer.eu/api/](https://test.qwqer.eu/api/)

### **Production API url**

[https://qwqer.eu/api/](https://qwqer.eu/api/)

<!-- tabs:end -->
