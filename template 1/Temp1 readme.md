# 🛍️ Bargenix: E-Commerce Bargaining Scenario Generator Template 1

This repository provides a modular, extensible system for generating **synthetic negotiation datasets** between a user and a virtual assistant (bot) in an e-commerce setting.

The system captures **negotiation dynamics**, calculating product and user profiles, generating conversation turns, and simulating discount rounds.


## 🔧 Features

- 📊 **Score-Based Decision Logic**: Calculates user and product scores based on behavioral and catalog data.
- 💬 **Dynamic Dialogue Simulation**: Mimics realistic single-turn negotiation between a user and a system.
- 💸 **Discount Round Strategy**: Offers context-aware discounts based on predefined bounds and scores.
- 💾 **JSONL Dataset Export**: Generates clean, structured, and ready-to-train data for LLMs or dialogue systems.
- 🔁 **Supports Multiple Scenarios**: Each scenario includes different rounds, product types, user behaviors, and discount outcomes.

## 🧠 Core Concepts

### User Score
Evaluates the user’s profile based on:
- Number of orders
- Total spend vs refunds
- Recency of last purchase
- Email verification status

### Product Score
Determined by:
- Product age
- Inventory levels
- Number of images
- Type (seasonal or regular)
- Tags (e.g., summer, winter)
- Average price

### Bargain Score
A randomized score (30–100) representing how aggressive the bargain is.

## 🔁 Negotiation Dynamics:
### 🔻 Max Rounds
The number of negotiation rounds is dynamically calculated based on:
- User Score
- Product Score
- Bargain Score

#### 📂 Explore the full code and datasets on GitHub
[🔗 Bargenix GitHub Repository](https://github.com/Bargenix/fastapi_llm_backend/blob/2da7d87a4537cf7202238e83f2f98a76306de75c/helper.py)

### 🗣️ Conversation Turn Logic
Each scenario simulates:
- The user's new discount request (based on previous round)
- The bot’s counter-offer (adapted to current round)
- An optional "final offer" if negotiation reaches late rounds

Bot replies vary by context:
- Early Rounds: Bot remains flexible
- Later Rounds (≥3): Bot gives a more assertive "final" offer

## 🧾 Example Output Structure
```json
{
    "Live_data_from_frontend": "User Info:\nuser_name = Rahul, email = rahul@gmail.com, orders = 6, spent = 9577, email_verified = rahul@gmail.com, refunds = 231, days_since_last = 131\n\nProduct Info:\nproduct_name = Health Foods, product_description = Superfoods (chia seeds, goji berries) and supplements like collagen peptides., product_color = Baby Blue, product_size = One Size, product_price = 4530 INR, min_price_client = 3126 INR, avg_inventory = 16, product_tag = spring, product_type = seasonal, images_count = 3, days_since_creation = 247\n\n",
    "user": "User: 10% is less it seems is that all you can offer,ok lets say if you can make it to 34 thats a deal",
    "response": "Bot: You've bargained well, so here's my final offer12% off, final price 3986.4 INR. Deal?",
    "metadata": {
      "user_email_id": "rahul@gmail.com",
      "user_score": 28.294752920432455,
      "bargain_score": 69,
      "product_price": 4530,
      "product_score": 24.953933279718918,
      "admin_max_discount_from_min_price": 31,
      "system_max_discount": 17,
      "max_round_count": 6,
      "current_round": 3,
      "previous_round_discount_given": 10,
      "user_req": 34,
      "current_discount": 12,
      "current_discount_price": 3986.4,
      "round_discounts": {
        "round_count1": 7,
        "round_count2": 10,
        "round_count3": 12,
        "round_count4": 14,
        "round_count5": 15,
        "round_count6": 17
      }
    }
  },
```
#### Below round 3
```json
{
    "Live_data_from_frontend": "User Info:\nuser_name = Dhruv, email = dhruv@gmail.com, orders = 12, spent = 7242, email_verified = dhruv@gmail.com, refunds = 175, days_since_last = 126\n\nProduct Info:\nproduct_name = Hair Dryer, product_description = Ionic hair dryer with ceramic technology and multiple speed/heat settings., product_color = Olive, product_size = One Size, product_price = 1943 INR, min_price_client = 1263 INR, avg_inventory = 53, product_tag = luxury, product_type = regular, images_count = 4, days_since_creation = 281\n\n",
    "user": "User: 9% is less it seems is that all you can offer,ok lets say if you can make it to 38 thats a deal",
    "response": "Bot: Id love to work something outhow about 13% off, making it 1690.41 INR? I'm open to hearing your offer too!",
    "metadata": {
      "user_email_id": "dhruv@gmail.com",
      "user_score": 30.289733953847282,
      "bargain_score": 96,
      "product_price": 1943,
      "product_score": 7.532588722239778,
      "admin_max_discount_from_min_price": 35,
      "system_max_discount": 23,
      "max_round_count": 6,
      "current_round": 2,
      "previous_round_discount_given": 9,
      "user_req": 38,
      "current_discount": 13,
      "current_discount_price": 1690.41,
      "round_discounts": {
        "round_count1": 9,
        "round_count2": 13,
        "round_count3": 17,
        "round_count4": 19,
        "round_count5": 21,
        "round_count6": 23
      }
    }
  },
```

🔗 Bargenix Full Dataset Generator ([Temp2](https://github.com/Bargenix/LLM--S3FT--Dataset-Generation-/tree/07fd97506db260c56fa5da820d433ec09212402b/template%202))