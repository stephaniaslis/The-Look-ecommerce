# The-Look-ecommerce

This is a project to create insights to a public data set called The Look E-Commerce hosted on Google Big Query.

## Dataset
Google Big query has many public datasets that can be used, one of them is The look ecomerce that is a fictitious E-Commerce Dataset.
This dataset has the following tables:
- distribution_centers
- events
- inventory_items
- order_items
- orders
- products
- users
  
![image](https://github.com/stephaniaslis/The-Look-ecommerce/assets/82055743/df4f5e77-3976-4f67-842b-af5bb8a5c116)

## Retrieving Data
The data was retrieved via a query on Google Big Query to combine data related to orders and logistic as it follows:

```
-- Query to obtain not Canceled orders
SELECT DISTINCT order_items.order_id AS order_item_order_id,	order_items.id AS order_items_id,	order_items.product_id as item_product_id,	order_items.status AS order_item_status ,	order_items.created_at AS order_items_created_at,	order_items.shipped_at AS order_items_shipped_at,	order_items.delivered_at AS order_items_delivered_at,	order_items.returned_at AS order_items_returned_at ,	order_items.sale_price AS order_items_sale_price,
orders.order_id AS orders_order_id,	orders.status AS orders_status,	orders.gender AS orders_gender,	orders.created_at AS orders_created_at ,	orders.returned_at AS orders_returned_at,	orders.shipped_at AS orders_shipped_at,	orders.delivered_at AS orders_delivered_at,	orders.num_of_item AS orders_num_of_item,	
products.id AS products_id ,	products.cost AS products_cost,	products.category AS products_category,	products.name AS products_name,	products.brand AS products_brand,	products.retail_price AS product_retail_price,	products.department AS product_department,	products.sku AS product_sku,	products.distribution_center_id AS products_distribution_center_id,
distribution_centers.id AS distribution_centers_id,	distribution_centers.name AS distribution_centers_name,	distribution_centers.latitude AS distribution_centers_latitude,	distribution_centers.longitude AS	distribution_centers_longitude
FROM `bigquery-public-data.thelook_ecommerce.orders` orders
LEFT JOIN
`bigquery-public-data.thelook_ecommerce.order_items` order_items
ON orders.order_id = order_items.order_id
LEFT JOIN`bigquery-public-data.thelook_ecommerce.products` products
on order_items.product_id = products.id
LEFT JOIN`bigquery-public-data.thelook_ecommerce.distribution_centers` distribution_centers
ON products.distribution_center_id = distribution_centers.id
WHERE orders.status NOT LIKE "Cancelled";
```

After that the data was downloaded in a csv file.

## Dasboard
There was dashbord creation using Tableau:

![image](https://github.com/stephaniaslis/The-Look-ecommerce/assets/82055743/1103a380-349e-4756-b20b-125f51c33b86)

link : https://public.tableau.com/views/Dashboardthelookecommerce/DashboardTHeLookEcommerce?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link
