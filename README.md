# Turn14 Shopify Inventory Update
This is a script to update your Shopify Inventory with Turn14.com's inventory every hour (the time interval they use to update their inventory spreadsheet).  

I made this before Turn14.com released their REST API, but I feel this is still useful to those who do not have experience with APIs.

## Dependencies
**Please note that this uses MySQL, make sure you have that installed before installing dependencies but you can use whatever db you are comfortable with.**
1. [Shopify](http://shopify.github.io/shopify_python_api/) **Use `pip install ShopifyAPI` if you aren't using MySQL**
1. MySQL-python  
### Installing Dependencies
Simply run the following command:
```python
pip install -r requirements.txt
```

## Turn14 Credentials
Please be sure to update the following section of config.json where **`"username": "username"`** to your username and **`"password": "password"`** to your password.
```json
"turn14": [
        {
            "username": "your user name",
            "password": "your password"
        }
    ]
```

## Shopify API
**More information on the Shopify Python API can be found here: [Shopify Python API](http://shopify.github.io/shopify_python_api/)**
- You will need to create a private app in your dashboard
  - Follow this tutorial: [Generate private API credentials](https://help.shopify.com/api/getting-started/api-credentials#generate-private-api-credentials)
  - You will need to assign Read and Write access to "read_products, write_products" in your admin dashboard
- You will need to update the the following section of config.json
```json
"shopify": [
        {
            "shop_name": "your shop name",
            "api_key": "your api key",
            "api_pass": "your api password"
        }
    ],
```
  - Change **`shop_name="your shop name"'`** to your shop's name (i.e. yourshopname in yourshopname.myshopify.com)
- Change **`"api_key": "your api key"`** and **`"api_pass": "your api password"`** to your API Key and Password that is generated by your admin dashboard.

## MySQL Setup
Use the following SQL statement to setup your DB exactly how it needs to be setup:
```mysql
CREATE TABLE inv (
  id int NOT NULL AUTO_INCREMENT,
  prod_id varchar(255) NOT NULL,
  sku varchar(255) NOT NULL,
  inventory int NOT NULL,
  PRIMARY KEY (id)
);
```
Replace **inv** with whatever you want your table to be named.
Update the following section of **config.json** to be the credentials of your MySQL DB (or whatever other db you are using)
```json
"database": [
        {
            "server": "your server",
            "username": "your username",
            "password": "your password",
            "table": "your schema"
        }
```
