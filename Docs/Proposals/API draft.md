# Endpoints
## Users
### Users/Basic
/users
GET - get all users (admin)
POST - add a user (non-authorised, used for sign-on)

/users/login
POST - log in to the system (non-authorised)

/users/:id
GET - get user info (admin, the user)
PUT - update user, JSON, preferably with changed fields only (the user, admin for group change)
DELETE - delete the user (admin only, not really deleted, but marked as such)

### Users/Aggregated Info
/users/info?user=user_query&status=[active | inactive | all]
GET - gets information about users as necessary for admin console. Details to be determined later according to the frontender's demands (admin)

### Traders
### Traders/Assets
/traders/:id/assets
GET - get the trader's assets list (the trader, admin)
POST - add a new asset to the trader's account (clearing house)

/traders/:id/assets/:aid
GET - get amount of asset in trader's posession (the trader, admin)
PUT - change assets amount (clearing house)
DELETE - remove asset from trader's account, only works if amount is zero (admin, not really deleted, but marked as such to be hidden from the trader)

### Traders/Orders
/traders/:id/orders?type=[ask | bid | all]&status=[active | fulfilled | cancelled | all]&period_start=date_from&period_end =date_to&updates_only=[true | false]
GET - gets trader's orders with possible filtering (the trader or admin)
POST - adds new order (parameters should not be used, we send JSON) (the trader)

/traders/:id/orders/:oid
GET - get order details (the trader, admin, clearing house)
PUT - change order (the trader, clearing house)
DELETE - cancel order (the trader, admin, not really deleted, but marked as such)

### Traders/Transactions
/traders/:id/transactions?type=[ask | bid | all]&status=[active | executed | all]&period_start=date_from&period_end =date_to&updates_only=[true | false]
GET - gets trader's past transactions with possible filtering (the trader or admin)
POST - adds new transaction (parameters should not be used, we send JSON) (clearing house)

/traders/:id/transactions/:tid
GET - get transaction details (the trader, admin)

### Traders/Aggregated Info
/traders/info?trader=trader_query&status=[active | inactive | all]
GET - gets information about traders as necessary for admin console. Details to be determined later according to the frontender's demands (admin)

## General info access (statistics, dashboards)
/info
GET - gets all endpoints for general info (all)

### Info/Goods
/info/goods
GET - gets all endpoints for goods info (all)
POST - add new goods type (admin)

/info/goods?list=true&goods=goods_name
GET - get a list of tradable goods with possible filtering by name (all)

/info/goods/:id
GET - get info on the goods type (all)
PUT - change goods type, JSON, preferably with changed fields only (admin)
DELETE - delete goods type (admin, not really deleted, but marked as such)

/info/goods/:id/market_info?transaction_type=[buy | sell | all]&period_start=date_from&period_end =date_to&aggregate=[yes | no]&aggregation_step=[(to be determined later)]&updates_only=[true | false]
GET - get historical data on all transactions with the goods, aggregated is necessary (all, unauthorised users get data excluding current date, Guests get data with some delay)

### Info/Transactions
/info/transactions
GET - get all enpoints for transactions info (all)

/info/transactions?goods=goods_name&transaction_type=[buy | sell | all]&period_start=date_from&period_end =date_to&aggregate=[yes | no]&aggregation_step=[(to be determined later)]&updates_only=[true | false]
GET - get historical data on all transactions with the goods, aggregated is necessary (all, unauthorised users get data excluding current date, Guests get data with some delay)
